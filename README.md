# Financial Returns Analysis 📈

A Python data analysis project exploring stock market data, built as part of a data analytics coursework challenge. The project walks through the full lifecycle of working with financial time series data — from initial exploration to advanced visualization — using `pandas`, `numpy`, and `plotly`.

## 📋 Project Overview

This project analyzes historical stock price data (starting with Apple, then expanding to multiple tech companies: Google, Apple, Amazon, Facebook, Netflix, and Microsoft) to uncover trends, calculate returns, and build interactive financial visualizations commonly used by analysts and investors.

## 🛠️ Tools & Libraries

- **pandas** — data manipulation and analysis
- **numpy** — numerical computations
- **plotly.express** & **plotly.graph_objects** — interactive data visualization

## 🔍 What This Project Covers

### 1. Data Exploration
- Loading financial data into a `pandas` DataFrame
- Inspecting data types and structure with `.info()`
- Generating summary statistics with `.describe()`
- Converting string dates into proper `datetime` objects
- Extracting day-of-week and ISO calendar information
- Filtering data by specific time periods (e.g., January & December)

### 2. Resampling & Returns
- Setting a datetime column as the DataFrame index
- Resampling data into quarterly periods with `.resample()`
- Calculating custom aggregations (min, median) per period
- Computing daily percentage returns with `.pct_change()`
- Calculating year-over-year growth using quarterly resampling

### 3. Window Functions
- Calculating rolling (moving) averages over a fixed number of rows
- Calculating rolling averages over a fixed time window (e.g., `"30D"`)
- Comparing short-term vs. long-term moving averages

### 4. Handling Missing Values
- Identifying gaps in time series data (e.g., missing weekends)
- Filling missing dates using `.asfreq()`
- Filling missing values with backward fill (`.bfill()`)
- Filling missing values using linear interpolation (`.interpolate()`)

### 5. Financial Charts & Visualization
- Plotting stock performance over time with `px.line()`
- Visualizing cumulative maximum and minimum values alongside actual price
- Comparing multiple moving averages (10-day vs. 30-day) on a single chart
- Reshaping wide-format data into long-format using `pd.melt()`
- Creating faceted area charts to compare multiple stocks side-by-side with `px.area()`

## 🔎 Key Findings

### Apple (AAPL) Stock Analysis
- The dataset covers **506 trading days** (Feb 2015 – Feb 2017) with **no missing values** in the original columns.
- Trading only occurs on **weekdays**: Tuesday and Wednesday had the most observations (105 each), while Monday had the fewest (94) — likely due to public holidays falling on Mondays.
- Over the full period, `AAPL.Close` ranged from a **minimum of ~$90** to a **maximum of ~$135.5**, with an average closing price of **~$113**.
- Daily returns (`.pct_change()`) fluctuated mostly within **±1–3%**, reflecting typical single-stock volatility.
- Quarterly analysis showed a clear **downturn through 2015–2016** (year-over-year open price dropped as much as **-24.8%** in Q3 2016) followed by a **strong recovery in late 2016 into 2017** (+12.9% year-over-year by Q1 2017).
- When gaps from weekends were introduced with `.asfreq('D')`, **interpolation** produced smoother, more realistic estimates for non-trading days than simple backward-fill, since it accounts for the gradual transition between Friday's close and Monday's open — except for categorical columns (`direction`, `Day_Name`), which cannot be interpolated.

### Multi-Stock Comparison (2018–2019)
Using Plotly's built-in dataset (Google, Apple, Amazon, Facebook, Netflix, Microsoft), all values were **rebased to 1.0** on the first day, allowing a fair side-by-side comparison regardless of each stock's original price level.
- **Microsoft (MSFT), Apple (AAPL), and Amazon (AMZN)** showed the strongest growth, each approaching or exceeding **1.7–1.8x** their starting value by the end of 2019.
- **Google (GOOG) and Facebook (FB)** were comparatively flatter, ending the period only modestly above their starting value.
- **Netflix (NFLX)** was the most volatile stock, with sharp swings but an overall upward trajectory.
- Comparing the **10-day vs. 30-day moving averages** for GOOG revealed several short-term/long-term crossover points (e.g., around April 2019), which in technical analysis are often read as potential trend-reversal signals ("golden cross" / "death cross").
- Tracking the **cumulative maximum and minimum** of GOOG highlighted how far the stock pulled back from its all-time high at any given point — a simple way to visualize drawdown risk.

## 📊 Key Concepts Used

| Concept | Method Used | Purpose |
|---|---|---|
| Data type conversion | `pd.to_datetime()` | Convert strings to real dates for time-based operations |
| Aggregation | `.resample()` + `.agg()` | Summarize data over custom time periods |
| Daily returns | `.pct_change()` | Measure day-over-day percentage change |
| Trend smoothing | `.rolling()` | Reduce noise and reveal underlying trends |
| Missing data | `.asfreq()`, `.bfill()`, `.interpolate()` | Handle gaps in time series data |
| Data reshaping | `pd.melt()` | Convert wide data into long format for faceted plotting |
| Visualization | `plotly.express`, `plotly.graph_objects` | Build interactive, presentation-ready charts |


## 📁 Repository Structure

```
financial-returns-analysis/
│
├── Financial_returns_Challenge.ipynb   # Main analysis notebook
└── README.md                           # Project documentation
```

## 📌 Notes

- The dataset used includes historical Apple stock prices as well as Plotly's built-in sample dataset (`px.data.stocks()`), which contains normalized (rebased) returns for six major tech companies.
- Values in the multi-stock dataset are **normalized returns**, not raw ticker prices — each stock's value is scaled relative to its price on the first day of the dataset.

## 🎓 Purpose

This project was completed as a hands-on exercise to strengthen practical skills in:
- Time series data manipulation with `pandas`
- Financial data analysis techniques
- Interactive data visualization with `plotly`

---
