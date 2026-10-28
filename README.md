# 📈 Crypto Analytics & Dashboard

## 📌 Project Overview
This interactive Power BI Dashboard provides an end-to-end financial analysis of cryptocurrency market dynamics spanning a 10-year historical dataset (2015–2025). 

Designed with an executive dark-mode layout, this project translates complex financial indicators—such as daily return distributions, price volatility (%), 7-day and 30-day rolling averages, and statistical correlations—into clean, actionable business intelligence.

---

## 📸 Dashboard Preview

---

## 🛠️ Tools & Technologies Used
- **Business Intelligence & Visualization:** Microsoft Power BI
- **Data Transformation & Modeling:** Power Query, DAX (Data Analysis Expressions), & Star Schema Architecture
- **Statistical Analysis:** Pearson Correlation Coefficients & Time-Series Rolling Averages
- **UI/UX Design:** Custom Dark-Themed Dashboard Containers & Interactive Visual Elements

---

## 🔑 Page-by-Page Interactive Features

### 1. Market Overview (`Page 1`)
* **Executive KPI Cards:** Quick summary of Total Symbols tracked (`2,017`), Average Volatility (`20,274.60%`), Average Daily Return (`1.40%`), and Total Trading Volume (`493T`).
* **Market Trend Analysis:** Dual-axis monthly comparison tracking Average Open vs. Average Close prices across the calendar year.
* **Volume Trajectory:** Time-series analysis of average trading volume fluctuations by month.
* **Top 5 Gainers & Losers:** Dynamic ranking bars isolating top performing tokens (e.g., `CAIR-USD`, `EVA33342-USD`) against major loss leaders.

### 2. Individual Asset Deep Dive (`Page 2`)
* **Rolling Averages (7-Day & 30-Day):** Smooth trendlines isolating short-term price momentum from long-term market signals across 2018–2025.
* **Historical Price Trendline:** Granular tracking of daily return percentage variations.
* **Volume vs. Volatility Comparison:** Dual-visual bar and line charts evaluating trading volume against percentage price swings.

### 3. Comparative Asset Analysis (`Page 3`)
* **Multi-Token Price Tradelines:** Comparative overlay of historical price performance across major tokens (e.g., `BNB-USD`, `NVDA`, `TRX-USD`).
* **Performance Ranking Matrix:** Top 10 performance matrix breaking down Average Daily Return (%), Average Volume, and Average Volatility (%).

### 4. Risk & Correlation Analysis (`Page 4`)
* **Risk Monitor:** Portfolio risk profiling assessing price fluctuation boundaries and downside volatility across selected tokens.
* **Cross-Asset Correlation Matrix:** Custom DAX-powered Pearson correlation heatmap evaluating linear price dependencies across key assets (`BTC`, `ETH`, `SOL`, `AVAX`, `BNB`, `DOGE`, `USDT`, `USDC`, `XRP`, `TRX`).

---

## 🕹️ Interactive Navigation
> **Note for Reviewers:** This Power BI report features built-in menu navigation buttons on the left sidebar. Hold **`Ctrl` + Left Click** on any navigation icon or tab button (Overview, Individuals, Comparatives, Risk Analysis, Correlation) to switch between report pages seamlessly.
