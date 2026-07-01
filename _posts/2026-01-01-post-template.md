---
# ─────────────────────────────────────────────────────────────────────────────
# HOW TO USE THIS TEMPLATE
#   1. Copy this file to a new name: _posts/YYYY-MM-DD-your-slug.md
#      e.g. _posts/2026-07-10-fixed-effects-intuition.md
#   2. Edit the fields below and write your post under the second "---".
#   3. Delete the `published: false` line (or set it to true) to make it live.
#   4. Commit and push — the site auto-deploys.
# ─────────────────────────────────────────────────────────────────────────────

layout: post # always "post" — do not change
title: your post title here # shown as the heading and in the blog list
date: 2026-01-01 # should match the date in the filename (YYYY-MM-DD)
description: a one-line summary shown under the title in the blog list # recommended

# --- optional fields (delete any you don't use) ---
tags: econometrics statistics # space-separated; creates /blog/tag/... pages
categories: notes # broader grouping; creates /blog/category/... pages
# featured: true                 # pin this post to the highlighted cards on /blog/
# thumbnail: assets/img/xyz.png  # small image shown beside the post in the list
# related_posts: false           # hide the "related posts" section at the bottom

published: false # KEEP this line on the template; DELETE it on real posts
---

<!--
  Everything below the front matter is your post, written in Markdown.
  Delete these example blocks and write your own content.
-->

Start with a short intro paragraph explaining what this post is about and why
you're writing it.

## A section heading

Use `##` for sections and `###` for subsections. Regular Markdown works
everywhere: **bold**, _italics_, [links](https://example.com), and lists:

- first point
- second point
- third point

### Math

Inline math with single dollars, like $\beta_1$ or $R^2$. Display equations
with double dollars:

$$
\hat{\beta} = (X^\top X)^{-1} X^\top y
$$

### Code

Fence code with triple backticks and a language name for syntax highlighting:

```python
import statsmodels.api as sm

model = sm.OLS(y, X).fit()
print(model.summary())
```

### Images

Put image files in `assets/img/` and reference them like this:

![description of the image](/assets/img/your-image.png)

### Quotes and callouts

> A blockquote is handy for highlighting a key idea or a definition.

Wrap up with a short closing paragraph or a note on what you'll explore next.
