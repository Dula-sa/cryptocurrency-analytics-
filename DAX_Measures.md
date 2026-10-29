# 📐 DAX Measures – Crypto Analytics & Dashboard

All DAX used in the Power BI dashboard, organised by purpose. Each entry shows **what it does**, **the code**, and **where it is used**.

**Source table:** `1000_cryptos` (`symbol`, `DATE`, `open`, `high`, `low`, `close`, `volume`)

---

## 📑 Contents

1. [Calculated Columns](#1-calculated-columns)
2. [Date Table](#2-date-table)
3. [KPI Measures](#3-kpi-measures)
4. [Rolling Averages](#4-rolling-averages)
5. [Correlation](#5-correlation)
6. [Data Model](#6-data-model)

---

## 1. Calculated Columns

Created on the `1000_cryptos` table (*New column*).

| Column | Purpose | Used in |
|--------|---------|---------|
| `Daily_Return(%)` | % change from open to close | Avg % Return, rolling averages, correlation |
| `Price_Change` | Absolute open–close move | Individuals page |
| `Range` | High minus low | Risk analysis |
| `Volatility(%)` | Intraday swing relative to low | Avg % Volatility card |

```dax
Daily_Return(%) =
DIVIDE ( [close] - [open], [open] ) * 100

Price_Change =
ABS ( [close] - [open] )

Range =
[high] - [low]

Volatility(%) =
IF (
    [low] > 0,
    DIVIDE ( [high] - [low], [low] ) * 100
)
```

> 💡 `Volatility(%)` ignores rows where `low <= 0`, which would otherwise produce extreme values.

---

## 2. Date Table

*New table*, then: sort `Month` by `Month No`, create the relationship, and **Mark as date table → `DATE`**.

```dax
DateTable =
ADDCOLUMNS (
    CALENDAR (
        MIN ( '1000_cryptos'[DATE] ),
        MAX ( '1000_cryptos'[DATE] )
    ),
    "YEAR",     YEAR ( [Date] ),
    "Month No", MONTH ( [Date] ),
    "Month",    FORMAT ( [Date], "MMMM" )
)
```

---

## 3. KPI Measures

Overview page cards, Top 5 Gainers and Top 5 Losers.

| Measure | Used in |
|---------|---------|
| `Total Symbols` | Total Symbol card |
| `Avg % Volatility` | Avg % Volatility card |
| `Avg % Return` | Avg % Return card, Top 5 Gainers / Losers |
| `Total_Volume` | Total Volume card, Trading Volume Over Time |
| `Top Volume Symbol` | Top Traded Symbol card |

```dax
Total Symbols =
DISTINCTCOUNT ( '1000_cryptos'[symbol] )

Avg % Volatility =
AVERAGE ( '1000_cryptos'[Volatility(%)] )

Avg % Return =
AVERAGE ( '1000_cryptos'[Daily_Return(%)] )

Total_Volume =
SUM ( '1000_cryptos'[volume] )

Top Volume Symbol =
VAR SymbolVolumes =
    SUMMARIZE (
        ALLSELECTED ( '1000_cryptos' ),
        '1000_cryptos'[symbol],
        "@Vol", SUM ( '1000_cryptos'[volume] )
    )
VAR TopOne =
    TOPN ( 1, SymbolVolumes, [@Vol], DESC )
RETURN
    MAXX ( TopOne, '1000_cryptos'[symbol] )
```

**Top 5 Gainers / Losers:** use `[Avg % Return]` as the value, then in the filter pane set `symbol → Top N → 5 → by Avg % Return` (*Top* for gainers, *Bottom* for losers).

---

## 4. Rolling Averages

Rolling average of daily return. Use `DateTable[DATE]` on the axis.

```dax
7days rolling average =
VAR LastDate = MAX ( DateTable[DATE] )
RETURN
    AVERAGEX (
        DATESINPERIOD ( DateTable[DATE], LastDate, -7, DAY ),
        CALCULATE ( AVERAGE ( '1000_cryptos'[Daily_Return(%)] ) )
    )

30days rolling average =
VAR LastDate = MAX ( DateTable[DATE] )
RETURN
    AVERAGEX (
        DATESINPERIOD ( DateTable[DATE], LastDate, -30, DAY ),
        CALCULATE ( AVERAGE ( '1000_cryptos'[Daily_Return(%)] ) )
    )
```

---

## 5. Correlation

Pearson correlation of daily returns between two symbols picked from two slicers.

**Slicer tables** (keep them disconnected, with no relationships):

```dax
Symbolist =
DISTINCT ( '1000_cryptos'[symbol] )

Symbolist 2 =
DISTINCT ( '1000_cryptos'[symbol] )
```

**Formula:**

```
r = (n·Σxy − Σx·Σy) / √[ (n·Σx² − (Σx)²) · (n·Σy² − (Σy)²) ]
```

`n` is the number of dates where **both** symbols have data. The result is between **−1** and **+1**.

```dax
Correlation Coeff =
VAR SymX = SELECTEDVALUE ( Symbolist[symbol] )
VAR SymY = SELECTEDVALUE ( 'Symbolist 2'[symbol] )
VAR Pairs =
    FILTER (
        ADDCOLUMNS (
            VALUES ( DateTable[DATE] ),
            "@X", CALCULATE (
                    AVERAGE ( '1000_cryptos'[Daily_Return(%)] ),
                    '1000_cryptos'[symbol] = SymX
                  ),
            "@Y", CALCULATE (
                    AVERAGE ( '1000_cryptos'[Daily_Return(%)] ),
                    '1000_cryptos'[symbol] = SymY
                  )
        ),
        NOT ISBLANK ( [@X] ) && NOT ISBLANK ( [@Y] )
    )
VAR N     = COUNTROWS ( Pairs )
VAR SumX  = SUMX ( Pairs, [@X] )
VAR SumY  = SUMX ( Pairs, [@Y] )
VAR SumXY = SUMX ( Pairs, [@X] * [@Y] )
VAR SumX2 = SUMX ( Pairs, [@X] ^ 2 )
VAR SumY2 = SUMX ( Pairs, [@Y] ^ 2 )
VAR Numer = N * SumXY - SumX * SumY
VAR Denom = SQRT ( ( N * SumX2 - SumX ^ 2 ) * ( N * SumY2 - SumY ^ 2 ) )
RETURN
    IF (
        ISBLANK ( SymX ) || ISBLANK ( SymY ) || N < 2,
        BLANK (),
        DIVIDE ( Numer, Denom )
    )
```

---

## 6. Data Model

| Relationship | Type |
|--------------|------|
| `DateTable[DATE]` → `1000_cryptos[DATE]` | One-to-many |
| `Symbolist` | Disconnected (slicer only) |
| `Symbolist 2` | Disconnected (slicer only) |
