---
layout: post # always "post" — do not change
title: Monte Carlo Integration # shown as the heading and in the blog list
date: 2026-07-02 # should match the date in the filename (YYYY-MM-DD)
description: a one-line summary shown under the title in the blog list # recommended

# --- optional fields (delete any you don't use) ---
tags: statistics # space-separated; creates /blog/tag/... pages
categories: notes # broader grouping; creates /blog/category/... pages
# featured: true                 # pin this post to the highlighted cards on /blog/
# thumbnail: assets/img/xyz.png  # small image shown beside the post in the list
# related_posts: false           # hide the "related posts" section at the bottom

published: false # KEEP this line on the template; DELETE it on real posts

# Monte Carlo Integration

*Monte Carlo integration approximates an integral by averaging random evaluations of the integrand. I derive the estimator from scratch, show why its error shrinks like $1/\sqrt{N}$, and verify everything with a worked example.*


Suppose we want to compute a definite integral,

$$
I = \int_a^b f(x)\, dx. \tag{1}
$$

If $f$ has a closed-form antiderivative, we are done. But many interesting functions do not. A classic example is

$$
f(x) = e^{-x^2}, \tag{2}
$$

whose antiderivative cannot be written in terms of elementary functions. The standard workaround is deterministic numerical integration, such as the [trapezoidal rule](https://en.wikipedia.org/wiki/Trapezoidal_rule), where we evaluate $f$ on a fixed grid. This works well in one dimension but degrades quickly as the dimension of the problem grows, a phenomenon known as the [curse of dimensionality](https://en.wikipedia.org/wiki/Curse_of_dimensionality).

Monte Carlo integration takes a different approach. Rather than evaluating $f$ on a grid, we evaluate it at *random* points and average. At first glance this sounds like it should be worse. Why would randomness help? The answer, at least in my mind, is one of the most elegant ideas in computational statistics, so let's derive it.

## Integrals are expectations

The key trick is to rewrite the integral in Equation 1 as an expectation. Multiply and divide the integrand by $b - a$:

$$
I = \int_a^b f(x)\, dx = (b-a) \int_a^b f(x)\, \frac{1}{b-a}\, dx. \tag{3}
$$

This looks like a pointless manipulation until we notice that $\frac{1}{b-a}$ is exactly the probability density function of a [uniform random variable](https://en.wikipedia.org/wiki/Continuous_uniform_distribution) $U$ on $[a, b]$. So Equation 3 is really

$$
I = (b-a)\, \mathbb{E}[f(U)], \qquad U \sim \text{Uniform}(a, b). \tag{4}
$$

In words, the integral of $f$ is just the average value of $f$ under uniform sampling, scaled by the length of the interval. This reframing is the entire idea. Once an integral is an expectation, we can estimate it the way we estimate any expectation, with a sample mean.

So draw $N$ [independent and identically distributed](https://en.wikipedia.org/wiki/Independent_and_identically_distributed_random_variables) samples $U_1, \dots, U_N$ from $\text{Uniform}(a, b)$ and define the Monte Carlo estimator as

$$
\hat{I}_N = \frac{b-a}{N} \sum_{i=1}^N f(U_i). \tag{5}
$$

## Why it works

The first thing to check is that the estimator is [unbiased](https://en.wikipedia.org/wiki/Bias_of_an_estimator), meaning it is correct on average. By linearity of expectation,

$$
\mathbb{E}[\hat{I}_N]
= \frac{b-a}{N} \sum_{i=1}^N \mathbb{E}[f(U_i)]
= (b-a)\, \mathbb{E}[f(U)]
= I. \tag{6}
$$

Furthermore, the [law of large numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers) tells us that a sample mean converges to its expectation, so $\hat{I}_N \to I$ as $N \to \infty$. Unbiasedness says we are right on average, and the law of large numbers says we get closer with more samples. But how fast?

Since the $U_i$ are independent, the variance of the estimator is

$$
\mathbb{V}[\hat{I}_N]
= \frac{(b-a)^2}{N^2} \sum_{i=1}^N \mathbb{V}[f(U_i)]
= \frac{(b-a)^2 \sigma_f^2}{N}, \tag{7}
$$

where $\sigma_f^2 = \mathbb{V}[f(U)]$ is the variance of the integrand under uniform sampling. Taking a square root, the standard error is

$$
\text{se}(\hat{I}_N) = \frac{(b-a)\, \sigma_f}{\sqrt{N}}. \tag{8}
$$

This is the famous $1/\sqrt{N}$ convergence rate of Monte Carlo methods. Two things about Equation 8 are worth pausing on.

First, notice what is *not* in the formula. The rate does not depend on the dimension of the problem. If we integrate over a region in $\mathbb{R}^{100}$ rather than an interval, the error still shrinks like $1/\sqrt{N}$. Deterministic grid methods cannot say the same, since covering a high-dimensional space with a grid requires exponentially many points. This is why Monte Carlo dominates in high dimensions.

Second, we can estimate $\sigma_f$ from the same samples we already drew, using the sample standard deviation of the $f(U_i)$ values. Combined with the [central limit theorem](https://en.wikipedia.org/wiki/Central_limit_theorem), which tells us $\hat{I}_N$ is approximately normal for large $N$, this gives a confidence interval essentially for free:

$$
\hat{I}_N \pm 1.96 \cdot \frac{(b-a)\, \hat{\sigma}_f}{\sqrt{N}}. \tag{9}
$$

So the method not only estimates the integral, it also tells us how much to trust the estimate.

## An example

Let's verify all of this on Equation 2, integrating $e^{-x^2}$ over $[0, 1]$. The true value can be written using the [error function](https://en.wikipedia.org/wiki/Error_function),

$$
I = \int_0^1 e^{-x^2}\, dx = \frac{\sqrt{\pi}}{2}\, \text{erf}(1) \approx 0.746824, \tag{10}
$$

which gives us a ground truth to compare against. The estimator in Equation 5, along with the standard error in Equation 8, takes only a few lines of code:

```python
import numpy as np

rng = np.random.default_rng(0)

def mc_integrate(f, a, b, n, rng):
    u = rng.uniform(a, b, size=n)
    fx = f(u)
    est = (b - a) * fx.mean()
    se = (b - a) * fx.std(ddof=1) / np.sqrt(n)
    return est, se
```

Running it on our integrand,

```python
from scipy import special

f = lambda x: np.exp(-x**2)
truth = np.sqrt(np.pi) / 2 * special.erf(1.0)

est, se = mc_integrate(f, 0, 1, n=10_000, rng=rng)
print(f"estimate: {est:.6f} +/- {1.96 * se:.6f}")
print(f"truth:    {truth:.6f}")
```

```
estimate: 0.747045 +/- 0.003939
truth:    0.746824
```

The estimate is within its own confidence interval of the truth, exactly as Equation 9 promised. We can also check the convergence rate empirically by computing the average absolute error across many repetitions for increasing $N$:

```python
Ns = np.unique(np.logspace(1, 6, 30).astype(int))
errors = []
for n in Ns:
    errs = [abs(mc_integrate(f, 0, 1, n, rng)[0] - truth)
            for _ in range(50)]
    errors.append(np.mean(errs))
```

Plotting the errors on a log-log scale gives Figure 1.

![Figure 1](fig1_mc.png)

**Figure 1.** (Left) The integrand $f(x) = e^{-x^2}$ evaluated at $40$ uniform draws on $[0, 1]$. The Monte Carlo estimate is the average height of the blue points, scaled by the interval length. (Right) Mean absolute error of the estimator as a function of $N$, averaged over $50$ repetitions, with an $N^{-1/2}$ reference line (green). The empirical error tracks the theoretical rate almost perfectly.

The empirical errors fall along the $N^{-1/2}$ reference line, confirming Equation 8. Note what the log-log slope of $-1/2$ implies in practice. To get one extra digit of accuracy, we need $100$ times more samples. Monte Carlo converges reliably, but slowly.

## Conclusion

Monte Carlo integration rests on a single reframing, which is that an integral is an expectation in disguise, and expectations can be estimated by sample means. Everything else follows from standard results. Unbiasedness follows from linearity, consistency from the law of large numbers, and the $1/\sqrt{N}$ error rate from the variance of a sample mean. The rate is slow but dimension-free, which is precisely why these methods power so much of modern statistics.

The slow rate also raises a natural question. If the error depends on $\sigma_f$ through Equation 8, can we make $\sigma_f$ smaller by sampling more cleverly than uniformly? The answer is yes, and it leads to [importance sampling](https://en.wikipedia.org/wiki/Importance_sampling), which I plan to cover in a future post.

---

**References**

Metropolis, N., & Ulam, S. (1949). The Monte Carlo method. *Journal of the American Statistical Association*, 44(247), 335-341.

Robert, C. P., & Casella, G. (2004). *Monte Carlo Statistical Methods*. Springer.
