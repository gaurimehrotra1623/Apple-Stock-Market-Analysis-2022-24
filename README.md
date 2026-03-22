# 📈 Apple Inc. (AAPL) — Stock Market Analysis
### A Python-based Exploratory Data Analysis of 3 Years of Real Market Data (2022–2024)

---

## 🧠 Overview

This project performs an **end-to-end financial data analysis** of Apple Inc.'s stock performance across 2022, 2023, and 2024 — covering a full market cycle from a Fed-driven bear market to recovery and stabilization.

The goal was not just to plot charts, but to **think like an analyst** — connecting patterns in the data to real-world macroeconomic events, quantifying risk with industry-standard metrics, and presenting findings as a coherent story.

---

## 📊 Key Findings at a Glance

| Metric | Value | Interpretation |
|---|---|---|
| **Trading Days Analyzed** | 752 | Jan 2022 — Dec 2024 |
| **Max Drawdown** | -30.91% | Peak-to-trough loss in 2022 |
| **Sharpe Ratio** | 0.37 | Risk-adjusted return (suppressed by 2022) |
| **Volume–Price Correlation** | 0.49 | Moderate: high volume → bigger moves |
| **Best Month** | Jul 2022 (+18%) | Q3 earnings beat defied bear market |
| **Worst Month** | Sep 2022 (-12%) | September Effect confirmed |

---

## 🗂️ Project Structure

```
apple-stock-analysis/
│
├── Apple_inc.ipynb          
├── aapl_price_ma.png        
├── aapl_returns_dist.png    
├── aapl_volatility.png   
├── aapl_heatmap.png 
├── aapl_drawdown.png 
├── aapl_vol_vs_abs_dr.png 
├── AAPL_Stock_Analysis_Report.docx
└── README.md
```

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `yfinance` | Fetch real historical stock data from Yahoo Finance |
| `pandas` | Data cleaning, transformation, feature engineering |
| `numpy` | Numerical operations and statistical calculations |
| `matplotlib` | Line charts, area plots, scatter plots |
| `seaborn` | Heatmaps, histogram with KDE overlay |

---

## ⚙️ Setup & Usage

```bash
# 1. Clone the repo
git clone https://github.com/yourusername/aapl-stock-analysis.git
cd aapl-stock-analysis

# 2. Install dependencies
pip install yfinance pandas numpy matplotlib seaborn jupyter

# 3. Launch the notebook
jupyter notebook Apple_inc.ipynb
```

> **Note:** Running the first cell will fetch fresh data from Yahoo Finance and save it as `aapl_stock.csv`. An internet connection is required for the first run only.

---

## 📓 Notebook Walkthrough

### 1. 📥 Data Collection & Cleaning
- Fetched 752 trading days of AAPL OHLCV data via `yfinance`
- Flattened multi-level column headers
- Verified zero null values — clean dataset, no imputation needed
- Data types validated: prices as `float64`, volume as `int64`

### 2. 🔧 Feature Engineering
Four analytical features derived from raw price data:

```python
df["Daily_Return"]   = df["Close"].pct_change()           # % change day-over-day
df["MA_7"]           = df["Close"].rolling(7).mean()       # Short-term trend
df["MA_30"]          = df["Close"].rolling(30).mean()      # Medium-term trend
df["Volatility_30"]  = df["Daily_Return"].rolling(30).std() # 30-day risk measure
```

### 3. 📉 Plot 1 — Price Trend with Moving Averages
Shows AAPL's full price journey with 7-Day and 30-Day moving averages overlaid.

**Key Insight:** The 7-Day MA crossing above the 30-Day MA (Golden Cross) in early 2023 signalled the beginning of the recovery rally — months before it was obvious from price alone.

### 4. 📊 Plot 2 — Daily Returns Distribution
Histogram + KDE of all 751 daily return values.

**Key Insight:** Near-normal but with fat tails — extreme return days occur more often than a perfect bell curve would predict. These outliers map directly to earnings announcements and Fed decisions.

### 5. 🌊 Plot 3 — Rolling 30-Day Volatility
Time-series area chart of rolling risk over the full period.

**Key Insight:** Volatility spiked sharply in early 2022 (Fed rate hike panic) then progressively compressed into 2024 — a classic pattern of volatility clustering and mean reversion.

### 6. 🗓️ Monthly Returns Heatmap
Calendar-style grid of monthly returns — red for negative, green for positive.

**Key Insights:**
- 2022: 8/12 months negative — broad macro selloff
- **September Effect confirmed**: negative in both 2022 (-12%) and 2023 (-9%)
- July 2022 (+18%): earnings beat defied the bear market

### 7. 📐 Sharpe Ratio — Risk-Adjusted Return
```python
risk_free_rate = 0.05 / 252
sharpe = (excess_returns.mean() / excess_returns.std()) * (252 ** 0.5)
# Result: 0.37
```
**Key Insight:** Below 1.0 — the 2022 bear market dragged the 3-year average down. In isolation, 2023–2024 would score significantly higher.

### 8. 📉 Drawdown Analysis
```python
rolling_max = df["Close"].cummax()
drawdown = (df["Close"] - rolling_max) / rolling_max
# Max Drawdown: -30.91%
```
**Key Insight:** An investor who bought at the Jan 2022 peak faced a ~31% paper loss at the worst point — fully recovered by 2023. Context: TSLA and GOOGL both fell 50–70%+ in the same period.

### 9. 📦 Volume vs. Price Movement
```python
corr = df["Volume"].corr(df["Abs_Return"])
# Result: 0.49
```
**Key Insight:** Moderate positive correlation — high volume days tend to be high movement days. This supports using volume as a confirmation signal for price breakouts.

---

## 💡 The Big Picture

> **2022** was a macro-driven bear market. AAPL fell ~31% — not because Apple's business weakened, but because rising interest rates repriced all growth assets downward.
>
> **2023** was a structural recovery. As Fed rate hike fears peaked and a pause was signalled, tech rebounded sharply. 9 of 12 months were positive.
>
> **2024** showed stabilization. Volatility compressed, monthly swings became more moderate — consistent with a maturing rally reaching fair value.

---

## 🚀 Potential Extensions

- [ ] Add multi-stock comparison (TSLA, GOOGL, MSFT, AMZN) with correlation heatmap
- [ ] Build an interactive Plotly/Dash dashboard with stock selector and date slider
- [ ] Add a simple moving average crossover trading signal
- [ ] Pull news sentiment data and correlate with price drops
- [ ] Deploy dashboard on Render or Hugging Face Spaces

---

## 📁 Data Source

All data sourced from **Yahoo Finance** via the `yfinance` Python library. No API key required. Data is auto-adjusted for stock splits and dividends.

---

## 👤 Author

**Your Name**
[LinkedIn](https://linkedin.com/in/yourprofile) · [GitHub](https://github.com/yourusername)

---

*Built as a portfolio project to demonstrate real-world financial data analysis using Python.*