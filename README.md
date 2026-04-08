# ✈️ AeroToolCast

> Forecasting aircraft maintenance tool demand and optimizing station-level allocation using historical flight data and machine learning.

---

## 📌 Problem Statement

Airlines operate maintenance stations across dozens of airports. Each station requires physical maintenance tools — and running out of a critical tool (an Out-of-Stock or OOS event) can ground aircraft and cost millions.

**AeroToolCast** predicts how many units of each maintenance tool a station will need over the next 30/60/90 days — based on fleet departure schedules and historical usage patterns — and generates allocation recommendations to prevent OOS events.

---

## 🎯 Key Features

- 📊 **Demand Forecasting** — Predicts tool demand per station using Moving Average, Prophet, and XGBoost
- 🏭 **Station-Level Allocation** — Recommends how many tool units each station needs based on forecast + current stock
- 🚨 **OOS Risk Flagging** — Identifies stations at risk of running out before next replenishment
- 📈 **Interactive Dashboard** — Built with Streamlit to visualize forecasts, allocation gaps, and risk levels

---

## 🗂️ Project Structure

```
AeroToolCast/
│
├── data/
│   ├── raw/                  # Raw BTS flight data
│   ├── processed/            # Cleaned and transformed data
│   └── simulated/            # Simulated tool usage data
│
├── notebooks/
│   ├── 01_eda.ipynb          # Exploratory Data Analysis
│   ├── 02_simulation.ipynb   # Tool usage simulation
│   ├── 03_forecasting.ipynb  # Model building and comparison
│   └── 04_allocation.ipynb   # Allocation logic
│
├── src/
│   ├── simulate.py           # Tool usage simulation logic
│   ├── forecast.py           # Forecasting models
│   ├── allocate.py           # Allocation recommendation engine
│   └── utils.py              # Helper functions
│
├── dashboard/
│   └── app.py                # Streamlit dashboard
│
├── requirements.txt
└── README.md
```

---

## 📦 Dataset

Flight data sourced from the **Bureau of Transportation Statistics (BTS)** — [On-Time Performance Dataset](https://www.transtats.bts.gov/).

- Airports: Selected 3 major US maintenance hubs
- Aircraft types: Narrow-body and wide-body
- Time range: 1 year of historical departures

Tool usage is **simulated** on top of flight data using domain-informed assumptions:
- Each departure triggers a maintenance check requiring tools
- Tool demand varies by aircraft type and check type
- Random noise added to reflect real-world variability

---

## 🤖 Models

| Model | Type | Notes |
|---|---|---|
| Moving Average | Baseline | 7-day rolling window |
| Prophet | Time Series | Handles seasonality and holidays |
| XGBoost | ML | Uses lag features, aircraft type, station |

Models are compared using **MAE** and **RMSE** on a held-out test set.

---

## 📐 Allocation Logic

```
Required Units = Forecasted Demand - Current Stock
OOS Risk = True if Required Units > Replenishment Lead Time Buffer
```

Output: per-station allocation recommendation table with OOS risk flag.

---

## 🖥️ Dashboard

Run locally:

```bash
pip install -r requirements.txt
streamlit run dashboard/app.py
```

Dashboard shows:
- Forecast vs Actual demand per station
- OOS risk heatmap by station
- Allocation gap table
- Model comparison chart

---

## 🛠️ Tech Stack

- **Python** — pandas, scikit-learn, Prophet, XGBoost, statsmodels
- **SQL** — Data extraction and transformation
- **Streamlit** — Dashboard
- **GitHub** — Version control

---

## 💡 Motivation

Built as a self-directed project to understand demand forecasting and resource allocation in airline Technical Operations — mirroring real-world tooling planning challenges in MRO (Maintenance, Repair & Overhaul) environments.

---

## 🚀 Future Scope

- Integrate real inventory/stock data
- Add procurement cost optimization layer
- Deploy dashboard on Streamlit Cloud
- Extend to multi-tool, multi-station optimization

---

## 👩‍💻 Author

**Prachi**  
B.Tech, MNNIT Allahabad  
Incoming Associate Analyst — United Airlines
