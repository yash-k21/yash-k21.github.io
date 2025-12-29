---
layout: page
title: Portfolio Optimization Dashboard
description: Interactive portfolio optimization using modern risk metrics
img: assets/img/EfficientFrontier.png
importance: 1
category: work
---

## Overview

This project is an **interactive stock portfolio optimization dashboard** built using **Python and Streamlit**.  
It allows users to construct and analyze optimal portfolios using multiple risk-adjusted performance metrics and visualize the **efficient frontier** through large-scale Monte Carlo simulations.

🔗 **Live App:** https://portfolio-optimization.streamlit.app/  
🔗 **GitHub Repository:** https://github.com/yash-k21/Portfolio-Optimization-Dashboard

---

## Core Visualizations

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/EfficientFrontier.png"
       title="Efficient Frontier" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/example.png"
       title="Portfolio Metrics Dashboard" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

<div class="caption">
Efficient frontier generated from 10,000 simulated portfolios alongside interactive portfolio performance metrics.
</div>

---

## Optimization Strategies Implemented

- **Sharpe Ratio** – Risk-adjusted return using total volatility  
- **Sortino Ratio** – Downside-risk focused performance metric  
- **Minimum Volatility** – Portfolios with lowest overall risk  
- **Information Ratio** – Excess return per unit of tracking error  
- **Tracking Error Minimization** – Benchmark deviation control  
- **Conditional Value-at-Risk (CVaR)** – Tail-risk focused optimization  

Each strategy leads to materially different portfolio allocations, highlighting trade-offs between risk, return, and downside exposure.

---

## Efficient Frontier Construction

The efficient frontier is computed using **10,000 Monte Carlo portfolio simulations** with random asset weights under full-investment constraints.  
Each point represents a feasible portfolio, enabling users to visually identify **optimal risk–return combinations** and compare them against their selected optimization objective.

---

## Key Features

- **Interactive UI (Streamlit)** – Real-time portfolio recomputation  
- **Dynamic Efficient Frontier** – Visual risk–return trade-offs  
- **Benchmark Comparison** – Relative performance evaluation  
- **Advanced Risk Metrics** – CVaR, skewness, kurtosis  
- **Modular Architecture** – Clean separation of optimization, metrics, and risk logic  

---

## Model Assumptions

- Historical returns proxy future expectations  
- Asset returns assumed normally distributed  
- No transaction costs or taxes  
- Fully invested portfolios (no cash)  
- Fixed investment horizon  

These assumptions keep the model transparent while allowing scope for future extensions.

---

## Tech Stack

- **Python**
- **NumPy / Pandas**
- **Streamlit**
- **Matplotlib**
- **Financial risk modeling & simulation**

---

## Usage

1. Open the web app  
2. Enter asset tickers, date range, and risk-free rate  
3. Select an optimization strategy  
4. Generate optimized portfolios and explore metrics  

---

## Future Extensions

- Bayesian expected return estimation  
- Regime-dependent risk modeling  
- Transaction cost modeling  
- Rolling-window backtesting  
- Factor-based portfolio construction  

---
