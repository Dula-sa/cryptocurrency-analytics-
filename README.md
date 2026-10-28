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
* **Executive KPI Cards:** Quick summary of Total Symbols tracked (`2,017`), Average Volatility (`20,274.60%`), Average Daily Return (`1.40%`), Total Trading Volume (`493T`), and Top Traded Symbol (`USDC-USD`).
* **Market Trend Analysis:** Dual-axis monthly comparison tracking Average Open vs. Average Close prices across the calendar year.
* **Volume Trajectory:** Time-series analysis of average trading volume fluctuations by month.
* **Top 5 Gainers & Losers:** Dynamic ranking bars isolating top performing tokens against major loss leaders.

### 2. Individual Asset Deep Dive (`Page 2`)
* **Rolling Averages (7-Day & 30-Day):** Smooth trendlines isolating short-term price momentum from long-term market signals across 2018–2025.
* **Historical Price Trendline:** Granular tracking of daily return percentage variations month-by-month.
* **Volume vs. Volatility Comparison:** Dual-visual bar and line charts evaluating monthly trading volume against percentage price swings.

### 3. Comparative Asset Analysis (`Page 3`)
* **Multi-Token Price Tradelines:** Comparative overlay of historical price performance across selected tokens (`BNB-USD`, `NVDA`, `TRX-USD`).
* **Top 10 Performance Ranking Matrix:** Multi-metric breakdown evaluating Average Daily Return (%), Average Volume, and Average Volatility (%).
* **Volume VS Volatility Bar Chart:** Volume-volatility comparative analysis across key selected assets.

### 4. Risk Analysis (`Page 4`)
* **Crypto Risk Map:** Scatter plot mapping Average Daily Return (%) against Average Volatility (%) to identify high-risk vs. high-return assets.
* **Top 10 Most Volatile Coins:** Bar chart isolating the most volatile assets led by `PXC-USD` (19.35%) and `FTC-USD` (15.65%).

### 5. Cross-Asset Crypto Correlation (`Page 5`)
* **Pearson Correlation Heatmap:** DAX-powered matrix analyzing linear price dependencies and directional co-movements across major assets (`AVAX`, `BNB`, `BTC`, `DOGE`, `ETH`, `SOL`, `TONIC`, `TRX`, `USDC`, `USDT`, `XRP`).
* **Color-Coded Heatmap Scale:** Green highlights strong positive correlations (e.g., `ETH` & `BTC` at 0.66), while red highlights weak or negative price relationships.

---

---

## 🕹️ Interactive Navigation
> **Note for Reviewers:** This Power BI report features built-in menu navigation buttons on the left sidebar. Hold **`Ctrl` + Left Click** on any navigation icon or tab button (Overview, Individuals, Comparatives, Risk Analysis, Correlation) to switch between report pages seamlessly.
