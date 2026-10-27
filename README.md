# Power Trading Financial MIS & 60-Day Working Capital Simulation
### Indian Electricity Market Analysis: Day-Ahead (DAM) vs. Real-Time (RTM)

Most finance case studies assume that if an operation makes a positive gross margin, the business is financially healthy. In India's power trading sector, that assumption can break a company.

Because trading margins are legally capped at just a few paise per unit, profitability doesn't depend only on getting the purchase price right—it hinges almost entirely on treasury management and working capital lines.

This project models a 30-day trading book using actual clearing data from the **Indian Energy Exchange (IEX)** to simulate trade economics, track Budget vs. Actual variances, and expose the massive cash flow mismatch caused by exchange rules versus off-taker collection realities.

---

## The Core Problem Modeled

A power trader operating on power exchanges faces a severe cash flow contradiction:
1. **The Exchange Mandate (T+1 Outflow):** Power purchased on IEX must be settled in cash the very next morning. If you don't pay, the exchange revokes market participation and calls your bank guarantees.
2. **The Off-Taker Lag (T+15 to T+45 Inflow):** Private industrial clients typically take 15 days to pay, while state power distribution companies (DISCOMs) often take 45 to 60 days to clear bulk energy invoices.

When your margin is only 4 to 7 paise per kilowatt-hour, financing this cash deficit with borrowed bank capital can completely erase your trading profits.

---

## Market Clearing Price Volatility (DAM vs. RTM)

Using 30 days of actual continuous clearing data from IEX (September 26 to October 25, 2026), I mapped clearing prices and volumes across both market segments.

![DAM vs RTM Prices](dam_vs_rtm_prices.png)

### Key Observations from the Data:
* **Baseline vs. Balancing:** DAM cleared at an average of **₹7.02/kWh**, providing a relatively predictable baseline. RTM was much more volatile, averaging **₹6.08/kWh** but swinging wildly between **₹2.03/kWh** and **₹8.45/kWh**.
* **Price Inversion & Penalties:** During solar/off-peak generation hours, sudden surplus drove RTM clearing down, making spot balancing cheaper than day-ahead contracts. However, during evening peak hours, sudden demand spikes caused RTM prices to surge past ₹8.00/kWh, creating heavy cost deviations for utilities that failed to lock in their baseline power 24 hours prior.

---

## Transaction Ledger & Portfolio Economics

I structured a 60-transaction ledger simulating a mid-sized power trading book across two standard off-takers:
* **UPPCL (State DISCOM):** 500 MWh daily via DAM at a regulated CERC margin cap of **₹0.04/kWh** (4 paise).
* **Tata Steel (Industrial Open Access):** 150 MWh daily via RTM at a CERC benchmark margin of **₹0.07/kWh** (7 paise).
* **Open Access Charges:** Factored in a realistic **₹0.45/kWh** benchmark covering CTU/STU wheeling, transmission losses, and POSOCO/Grid-Controller scheduling fees.

### Portfolio Performance Summary

| Metric | Day-Ahead Market (DAM) | Real-Time Market (RTM) | Total Portfolio | Notes |
| :--- | :---: | :---: | :---: | :--- |
| **Off-Taker** | UPPCL (State Utility) | Tata Steel (C&I Client) | 2 Clients | Daily execution over 30 days |
| **Volume Cleared** | 15.00 MUs | 4.50 MUs | **19.50 MUs** | $1\text{ MU} = 1,000,000\text{ kWh}$ |
| **Gross Invoiced Revenue** | ₹11.26 Cr | ₹2.97 Cr | **₹14.23 Cr** | Billed tariff to clients |
| **Power Purchase & Wheeling Cost** | ₹11.20 Cr | ₹2.94 Cr | **₹14.14 Cr** | Direct landed power cost |
| **Net Gross Fee Margin** | ₹6.00 Lakhs | ₹3.15 Lakhs | **₹9.15 Lakhs** | Trading fee revenue |
| **Realized Margin per Unit** | 4.00 paise/kWh | 7.00 paise/kWh | **4.69 paise/kWh** | Volume-weighted average |

---

## The Treasury Risk: 60-Day Working Capital Simulation

To evaluate what happens to that ₹9.15 Lakhs gross margin in the real world, I built a daily cash flow model running over a 60-day horizon:
* Daily cash outflow to IEX for clearing obligations (T+1).
* Cash collections from Tata Steel starting on Day 16 (T+15).
* Cash collections from UPPCL starting on Day 46 (T+45).

![Working Capital Deficit](working_capital_deficit.png)

### The Numbers:
* **The Liquidity Trough:** Because the desk had to fund daily power purchases upfront, the cumulative cash position dropped continuously, reaching a **peak deficit of -₹12.56 Crore on Day 31**.
* **Financing Drag:** At a standard **9.0% p.a.** working capital borrowing rate (cash credit / overdraft limit), interest costs on the negative balance accumulated to **₹12.59 Lakhs** over the cycle.
* **The Bottom Line:**
  $$\text{Gross Fee Margin (₹9.15 L)} - \text{Financing Interest (₹12.59 L)} = \mathbf{-₹3.44\text{ Lakhs (Net Loss)}}$$

Despite running an operationally disciplined, fully matched trading book, the trade became unprofitable solely because of the receivable credit lag.

---

## Actionable Takeaways for a Trading Finance Desk

1. **Letter of Credit (LC) Discounting is Mandatory:** For 45-day DISCOM contracts, trading finance desks must insist on non-recourse LC discounting. Turning 45-day paper into T+3 cash removes the balance-sheet drag that wipes out narrow trading margins.
2. **Dynamic Financing Surcharges:** Standard power supply agreements must explicitly bundle the carrying cost of capital (around 8–10 paise/kWh) into the contract terms if extended credit periods are requested by the buyer.
3. **Portfolio Balancing:** Relying too heavily on state utilities introduces structural cash bottlenecks. Trading desks need a healthy ratio of 15-day C&I industrial off-takers to maintain liquidity without burning bank credit lines.

---

## What’s Inside the Excel Model (`Power_Trading_Model.xlsx`)

The accompanying Excel file contains 5 linked worksheets built using native formulas (`SUMIF`, `AVERAGE`, `MATCH`, `OFFSET`):
1. **`05_Executive_Dashboard`**: A clean, C-suite front page with KPI summary cards, embedded price volatility charts, and liquidity trajectory curves.
2. **`01_Daily_Market_Data`**: 30-day IEX price and volume normalization, converting ₹/MWh to ₹/kWh and calculating daily market spreads.
3. **`02_Trading_Ledger`**: A 60-transaction ledger tracking volume, landed purchase costs, transmission charges, and client billings.
4. **`03_Financial_MIS`**: Segment profitability tables and Budget vs. Actual variance analysis isolating volume variance and price deviations.
5. **`04_Working_Capital`**: A 60-day day-by-day cash flow schedule tracking daily liquidity requirements and 9% overdraft interest drag.

---

## Data Sources
* **Indian Energy Exchange (IEX):** Daily Market Clearing Prices (MCP) and Cleared Volumes (MCV) across DAM and RTM segments.
* **Central Electricity Regulatory Commission (CERC):** Monthly Market Monitoring Cell reports (January–March 2026) for statutory margin ceiling benchmarks and trading licensee market share structures.
