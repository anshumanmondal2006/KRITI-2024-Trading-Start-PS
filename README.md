
# 📊 BANKNIFTY Trading Strategy – Options Data Driven
## Kriti'24 PS- Trading Strategy Challenge with Options Data (Stood 3rd in Inter-Hostel at IITG)

## 📂 Dataset Description

- **Underlying Index Data**:  
  - BANKNIFTY index data 
  - Columns: `Date`, `Open`, `High`, `Low`, `Close`, `Volume`

- **Options Data Used**:  
  - **Put & Call Options** (ATM + relevant OTM strike prices)  
  - Columns include: `Date`, `Expiry`, `Strike Price`, `Option Type`, `Open`, `Close`, `Open Interest`, etc.

- **Preprocessing Summary**:  
  - Date formatting  
  - Weighted moving averages for price (`7-day` and `21-day`)  
  - Volume moving average (`21-day`)  
  - Computed **Put/Call Ratio (PCR)** using filtered Open Interest  
  - Removed far OTM/ITM options to reduce noise

---
## 📁 Project Directory Structure

```
KRITI-2024-Trading-start-/
├── LICENSE               (License file)
├── Quant_PS.pdf          (Problem Statement PDF for the challenge)
├── README.md             (Project summary!)
├── Report.pdf            (Final report detailing strategy, analysis, and results that was submitted to the TechBoard-IITG)
├── code.ipynb            (Jupyter notebook containing complete implementation)
```

## ⚙️ Strategy Logic (With Thresholds)

### ✅ Entry Conditions (Go Long):
- `Close(i-1) ≥ 21-day Weighted Moving Average`
- `Put/Call Open Interest Ratio (PCR) > 2.0` (market fear = contrarian bullish)
- `Volume(i-1) < 21-day Volume Moving Average` (low crowd activity)

### ❌ Exit Conditions (Close Position or Avoid):
- `Close(i-1) < 21-day Weighted Moving Average`
- `PCR < 0.3` (over-optimism = contrarian bearish)
- `Volume(i-1) < 0.8 × Volume_MA(i-1)`
- Daily portfolio drop > 1% → `res_port[i] < 0.99 × res_port[i-1]`

---

## 📈 Backtest Performance (Jul–Dec 2023)

| Metric                          | Value      |
|---------------------------------|------------|
| **Total Return (Strategy)**     | **+9.17%** |
| **Total Return (Buy & Hold)**   | +6.26%     |
| **Annualized Sharpe Ratio**     | **1.33**   |
| **Maximum Drawdown**            | **1.31%**  |
| **Initial Capital**             | ₹1,00,000  |

- The strategy **outperformed** buy-and-hold in returns and risk-adjusted metrics
- Maintained **lower drawdown**, offering better downside protection

---

## 🔍 Observations & Insights

- **21-day WMA** effectively captures mid-term trend direction
- **PCR as a contrarian sentiment filter** helps identify reversal opportunities
- **Low volume filter** avoids crowded or low-confidence trades
- **Stop-loss rule (1% drop)** keeps risk under control

---

## ✅ Conclusion

This rule-based trading system combines **trend-following**, **options sentiment**, and **volume analysis** to make tactical long-only decisions on the BANKNIFTY index. The model shows **improved returns and lower drawdowns** versus passive strategies and can be further enhanced with real-time data feeds or intraday refinements.
