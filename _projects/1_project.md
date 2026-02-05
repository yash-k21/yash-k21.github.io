---
layout: page
title: Portfolio Optimization Dashboard
description: Interactive portfolio optimization using modern risk metrics
img: assets/img/EfficientFrontier.png
importance: 1
category: work
giscus_comments: true
---

# Portfolio Optimization Dashboard

> **An interactive web app for constructing, analyzing, and visualizing optimal stock portfolios using modern risk metrics.**

[![Live App](https://img.shields.io/badge/Live%20App-Streamlit-green?logo=streamlit)](https://portfolio-optimization.streamlit.app/) [![GitHub](https://img.shields.io/badge/GitHub-Repository-blue?logo=github)](https://github.com/yash-k21/Portfolio-Optimization-Dashboard)

---

## Overview

The Portfolio Optimization Dashboard is a Python and Streamlit-based web application that empowers users to:
- Build custom portfolios from any set of stocks
- Optimize allocations using multiple risk-adjusted performance metrics
- Visualize the efficient frontier and explore risk–return trade-offs interactively
- Compare portfolio performance against benchmarks
- Analyze advanced risk metrics and portfolio statistics
- Experiment with different optimization strategies and constraints

This project is designed for both individual investors and finance professionals who want to explore modern portfolio theory, risk management, and quantitative investing in an intuitive, interactive way.

---

## Motivation & Goals

Traditional portfolio optimization tools often focus solely on mean-variance analysis and the Sharpe ratio. This dashboard aims to provide a more comprehensive and flexible platform by:
- Incorporating advanced risk metrics (CVaR, skewness, kurtosis)
- Allowing users to compare multiple optimization objectives
- Enabling hands-on exploration of the efficient frontier and risk–return trade-offs
- Providing a modular, extensible codebase for further research and experimentation

---

## Key Features

- ⚡ **Interactive UI**: Real-time portfolio recomputation and visualization
- 📈 **Efficient Frontier**: 10,000+ Monte Carlo simulated portfolios
- 🏆 **Multiple Optimization Strategies**: Sharpe, Sortino, Minimum Volatility, Information Ratio, Tracking Error, CVaR
- 📊 **Advanced Risk Metrics**: CVaR, skewness, kurtosis, tracking error
- 🔄 **Benchmark Comparison**: Evaluate portfolios relative to a chosen benchmark
- 🧩 **Modular Architecture**: Clean separation of optimization, metrics, and risk logic
- 🛠️ **Custom Constraints**: Full-investment, no shorting, and more
- 📅 **Flexible Data Input**: Choose any asset tickers and date ranges

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

- **Efficient Frontier Plot**: Visualizes the risk–return spectrum of simulated portfolios, highlighting optimal points for each strategy.
- **Portfolio Metrics Dashboard**: Displays key statistics (expected return, volatility, Sharpe/Sortino ratios, CVaR, skewness, kurtosis, tracking error, etc.) for selected portfolios.
- **Allocation Pie Charts**: Instantly see how weights shift across strategies.
- **Benchmark Comparison**: Overlay your portfolio against a benchmark (e.g., S&P 500) for context.

---

## Optimization Strategies

- **Sharpe Ratio** – Maximize risk-adjusted return
- **Sortino Ratio** – Focus on downside risk
- **Minimum Volatility** – Lowest overall risk
- **Information Ratio** – Excess return per unit of tracking error
- **Tracking Error Minimization** – Control deviation from benchmark
- **Conditional Value-at-Risk (CVaR)** – Minimize tail risk

Each strategy produces distinct portfolio allocations, highlighting trade-offs between risk, return, and downside exposure. The dashboard allows you to compare these allocations side-by-side and understand the impact of each optimization objective.

---

## How It Works

1. **Input**: Enter asset tickers, date range, and risk-free rate
2. **Select**: Choose an optimization strategy
3. **Simulate**: App generates 10,000+ random portfolios under full-investment constraints
4. **Visualize**: Explore the efficient frontier and portfolio metrics
5. **Compare**: Benchmark your portfolio against market indices
6. **Analyze**: Dive into advanced risk metrics and allocation breakdowns

---

## Under the Hood: Architecture & Methods

- **Data Handling**: Uses Pandas and yfinance to fetch and process historical price data for any set of tickers.
- **Monte Carlo Simulation**: Generates thousands of random portfolios by sampling asset weights, ensuring full investment and no shorting (unless enabled).
- **Risk & Performance Metrics**: Calculates expected return, volatility, Sharpe/Sortino ratios, CVaR, skewness, kurtosis, tracking error, and more for each portfolio.
- **Optimization Logic**: Modular design allows easy addition of new strategies or constraints. Each optimization method is implemented as a separate function/class.
- **Visualization**: Matplotlib and Streamlit are used for interactive, high-quality plots and dashboards.
- **Extensibility**: The codebase is organized for easy extension—add new metrics, strategies, or UI components with minimal changes.

---

## Model Assumptions

- Historical returns proxy future expectations
- Asset returns are normally distributed
- No transaction costs or taxes
- Fully invested portfolios (no cash)
- Fixed investment horizon

These assumptions keep the model transparent and extensible. Advanced users can modify these in the codebase for more realistic scenarios.

---

## Tech Stack

- **Python** (core logic, data processing)
- **NumPy / Pandas** (numerical and data analysis)
- **Streamlit** (web app framework)
- **Matplotlib** (visualizations)
- **yfinance** (data acquisition)
- **Financial risk modeling & simulation**

---

## Usage

1. Open the [Live App](https://portfolio-optimization.streamlit.app/)
2. Enter your desired asset tickers, date range, and risk-free rate
3. Select an optimization strategy (Sharpe, Sortino, etc.)
4. Generate and explore optimized portfolios, metrics, and visualizations
5. Download results or screenshots for further analysis

---

## Example Use Cases

- **Compare different risk-based portfolio allocations for your favorite stocks**
- **Visualize how adding or removing an asset changes the efficient frontier**
- **Assess the impact of downside risk (Sortino, CVaR) vs. traditional metrics (Sharpe)**
- **Benchmark your custom portfolio against the S&P 500 or other indices**
- **Experiment with new optimization strategies by extending the codebase**

---

## Future Extensions

- Bayesian expected return estimation
- Regime-dependent risk modeling
- Transaction cost modeling
- Rolling-window backtesting
- Factor-based portfolio construction
- User-defined constraints (sector, ESG, etc.)
- Enhanced reporting and export options

---

## Try It Out!

- [Live App](https://portfolio-optimization.streamlit.app/)
- [GitHub Repository](https://github.com/yash-k21/Portfolio-Optimization-Dashboard)

For questions or feedback, feel free to open an issue on GitHub or contact me directly.
