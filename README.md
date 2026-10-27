# ⚡ Indian Power Market Analysis: DAM vs. RTM Financial MIS & Working Capital Simulation

## 📌 Project Overview
A quantitative finance model simulating an Open-Access Power Trader operating across the **Indian Energy Exchange (IEX)** in both the **Day-Ahead Market (DAM)** and **Real-Time Market (RTM)**. 

The project evaluates 30 days of actual market clearing data, models transactional landed costs, applies CERC statutory margin caps (₹0.04 to ₹0.07/unit), creates an executive Financial MIS with Budget vs. Actual variance, and forecasts working capital liquidity strain.

---

## 📊 Portfolio Financial Performance Summary

| Metric | Day-Ahead Market (DAM) | Real-Time Market (RTM) | Total Combined Portfolio |
| :--- | :---: | :---: | :---: |
| **Counterparty** | UPPCL (State DISCOM) | Tata Steel (C&I Industrial) | Multi-Client Portfolio |
| **Volume Cleared** | 15.00 MUs | 4.50 MUs | **19.50 MUs** |
| **Gross Invoiced Revenue** | ₹11.26 Cr | ₹2.97 Cr | **₹14.23 Cr** |
| **Power Purchase & Wheeling Cost** | ₹11.20 Cr | ₹2.94 Cr | **₹14.14 Cr** |
| **Net Trading Margin** | ₹6.00 Lakhs | ₹3.15 Lakhs | **₹9.15 Lakhs** |
| **Realized Margin per Unit** | 4.00 paise/kWh | 7.00 paise/kWh | **4.69 paise/kWh** |

---

## 📈 Visual Analytics

### 1. Market Clearing Price Volatility: DAM vs. RTM
Analysis of 30-day clearing price spreads indicating high evening peak volatility in RTM spot balancing:
![DAM vs RTM Prices](dam_vs_rtm_prices.png)

### 2. 60-Day Treasury Cash Flow & Working Capital Deficit
Demonstrating the liquidity gap caused by strict **T+1 exchange settlement obligations** versus **15–45 day off-taker collection cycles**:
![Working Capital Deficit](working_capital_deficit.png)

---

## 💡 Core Treasury Finding & Management Commentary
* **The Liquidity Gap**: The trading desk incurs a **peak cash deficit of -₹12.41 Cr to -₹12.56 Cr on Day 31** before DISCOM collections start.
* **Financing Drag**: At a standard 9.0% p.a. working capital borrowing rate, daily interest costs accumulate to **₹12.59 Lakhs**, eroding the **₹9.15 Lakhs** gross margin.
* **Strategic Takeaway**: In power trading finance, managing Bank Guarantees (BGs), Letter of Credit (LC) discounting, and receivable collection windows is just as critical to solvency as power purchase pricing.

---

## 📂 Repository File Structure
```text
├── Power_Trading_Model.xlsx   # Complete 5-sheet financial model & executive dashboard
├── dam_vs_rtm_prices.png      # IEX clearing price volatility plot
├── working_capital_deficit.png # 60-day treasury liquidity trajectory
└── README.md                  # Executive report and project documentation
