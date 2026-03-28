# 📊 Trader Performance vs Market Sentiment Analysis

> **Primetrade.ai — Data Science Intern Assignment (Round 0)**  
> Analyzing how Bitcoin Fear/Greed sentiment affects trader behavior and performance on Hyperliquid.

---

## 🔍 Overview

This project investigates whether market sentiment (Fear, Greed, Extreme Fear, Extreme Greed, Neutral) measurably impacts:

- Trader profitability (Closed PnL)
- Win rate patterns
- Trade frequency and participation
- Risk behavior (leverage, position sizing)

By merging **Bitcoin Fear/Greed Index data** with **Hyperliquid historical trading data** (~211K trades), this analysis uncovers actionable behavioral patterns across different market regimes.

---

## 📁 Project Structure

```
trader-sentiment-analysis/
│
├── data/
│   ├── fear_greed.csv          # Bitcoin sentiment data (Date, Classification)
│   └── historical_data.csv     # Hyperliquid trade data (211,224 rows)
│
├── analysis.ipynb              # Main analysis notebook
└── README.md
```

---

## 🛠️ Setup & How to Run

### 1. Clone the repository
```bash
git clone https://github.com/https://github.com/sritham2k12/trader-sentiment-analysis.git
cd trader-sentiment-analysis
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 3. Add the datasets
Place both CSV files inside the `data/` folder:
- `fear_greed.csv`
- `historical_data.csv`

### 4. Run the notebook
```bash
jupyter notebook analysis.ipynb
```

> **Note:** The datasets are not included in this repo due to size. Download links are provided in the assignment brief.

---

## 📊 Datasets

| Dataset | Rows | Key Columns |
|---|---|---|
| Fear/Greed Index | ~365 days | Date, Classification, Value |
| Hyperliquid Trades | 211,224 | Account, Closed PnL, Side, Size USD, Timestamp IST |

**Sentiment Distribution in Merged Dataset:**

| Sentiment | Trade Count |
|---|---|
| Fear | 61,837 |
| Greed | 50,303 |
| Extreme Greed | 39,992 |
| Neutral | 37,686 |
| Extreme Fear | 21,400 |

---

## 🧹 Part A — Data Preparation

**Steps performed:**
- Loaded both datasets and documented shape, missing values, duplicates
- Converted `Timestamp IST` (DD-MM-YYYY format) and `timestamp` (UNIX) to datetime
- Aligned both datasets on a common `date` column
- Merged using `inner join` on date → 211,218 rows retained

**Key engineered features:**
- `win` — Boolean: True if Closed PnL > 0
- `daily_pnl` — Total PnL per trader per day
- `win_rate` — Fraction of winning trades per account
- `trade_count` — Total trades per account (activity level)
- `total_pnl` — Cumulative PnL per trader
- `type` — Trader classification: Winner / Loser

---

## 🔬 Part B — Analysis

### Q1: Does performance differ between Fear vs Greed days?

**Finding:** Yes, significantly.

- Average PnL is higher during **Greed and Extreme Greed** phases, suggesting favorable trending conditions
- **Fear and Extreme Fear** days show reduced average profitability and higher variance in losses
- The boxplot visualization confirms that PnL spread is widest under Extreme conditions

### Q2: Do traders change behavior based on sentiment?

**Finding:** Yes, clear behavioral shifts observed.

- **Trade frequency is highest during Fear** — traders are reactive, not passive
- **Extreme Fear shows the lowest participation** — traders hesitate or exit
- Long/Short ratio shifts slightly bullish during Greed phases

### Q3: Trader Segmentation

**Segment 1 — Winners vs Losers (by total PnL):**
- A minority of accounts accumulate positive total PnL
- Most traders are net negative, consistent with known crypto trading dynamics

**Segment 2 — Frequent vs Infrequent Traders:**
- High-frequency traders do not automatically outperform
- Some low-frequency traders show higher win rates, suggesting selectivity

**Segment 3 — High vs Low Win Rate:**
- Top trader win rate: **81%** — far above the median (~40–45%)
- Win rate concentration is high — only a few accounts trade consistently profitably

---

## 💡 Key Insights

**Insight 1 — Sentiment Drives Profitability**
Trader PnL is meaningfully higher during Greed and Extreme Greed regimes. Fear-phase trading tends to produce smaller profits and larger losses, indicating that most traders are trend-followers rather than contrarians.

**Insight 2 — Extreme Fear = High Volatility, Low Participation**
Extreme Fear days have the lowest trade count but show some of the widest PnL swings. Traders who do participate take outsized risks, resulting in both the largest single-day gains and losses.

**Insight 3 — Profitability is Concentrated Among Few**
Only a small subset of accounts (~top 10–15%) maintain win rates above 50%. The top trader sustains an 81% win rate, suggesting that consistent profitability requires significant skill or informational edge — not just activity.

**Insight 4 — Fear Does Not Mean Inaction**
Contrary to expectation, Fear days show *more* total trading activity than Extreme Greed. This suggests many traders respond emotionally to fear by trading more frequently, often to their detriment.

---

## 🚀 Part C — Strategy Recommendations

**Strategy 1 — Reduce Exposure During Fear Regimes**
During Fear and Extreme Fear periods, traders should reduce leverage and position sizes. PnL distributions show wider downside during these regimes. Risk-adjusted performance improves by sitting out or trading smaller.

> *"During Fear days, reduce position size by 30–50% and avoid initiating new long positions without confirmation."*

**Strategy 2 — Capitalize on Greed Momentum with Discipline**
Greed and Extreme Greed phases offer higher average PnL. Traders can increase participation during these regimes, but must implement strict stop-losses to avoid being caught in reversals.

> *"During Greed phases, momentum strategies outperform. Increase trade frequency but cap individual trade risk at 1–2% of portfolio."*

**Strategy 3 — Track and Mirror High Win-Rate Traders**
A small group of accounts consistently outperform across all regimes. Identifying and tracking these accounts (e.g., filtering for win rate > 70% over 30+ trades) can serve as a signal for strategy alignment.

> *"Build a leaderboard of high win-rate traders and use their activity as a sentiment-adjusted signal layer."*

---

## 📈 Charts Included in Notebook

- Boxplot: Closed PnL by Sentiment Classification
- Bar chart: Trade Count by Sentiment
- Win Rate distribution across accounts
- Winners vs Losers pie breakdown

---

## 🧠 Methodology Summary

1. **Data ingestion** — Loaded 211K+ trade records and daily sentiment data
2. **Cleaning** — No missing values found; timestamp format corrected (dayfirst=True)
3. **Alignment** — Merged on date key using inner join
4. **Feature engineering** — Created win flags, daily PnL, win rate, trade frequency, trader type
5. **Segmentation** — Classified traders by total PnL, win rate, and activity level
6. **Analysis** — Compared metrics across 5 sentiment regimes
7. **Insight generation** — Derived 4 data-backed insights and 3 actionable strategies

---

## 👤 Author

**N. Manisritham**  
B.Tech — AI & Data Science  
[GitHub](https://github.com/YOUR_USERNAME) | [Portfolio](https://manisritham.netlify.app)

---

*Submitted as part of Primetrade.ai Data Science Intern — Round 0 Assignment*
