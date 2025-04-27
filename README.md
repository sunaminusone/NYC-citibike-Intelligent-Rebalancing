# 🚴 NYC CitiBike Intelligent Rebalancing System

This project develops a complete pipeline to analyze, forecast, and optimize CitiBike station demand in New York City.  
We use time series forecasting, queueing simulation, and vehicle routing optimization to create an intelligent rebalancing decision support system.

---

## 📦 Project Workflow

### 1. Data Preparation and Cleaning
- Import 2023 Citi Bike user trip data (January to December).
- Clean the data: remove trips with the same start and end station, trips shorter than 1 minute, and trips with missing coordinates.
- Standardize timestamps, extract date and hour fields.
- Calculate hourly inflow, outflow, and net_flow for each station.

✅ **Output:** Cleaned, hourly-aggregated station flow dataset.

---

### 2. Time Series Forecasting
- Split the dataset into training set (January–September) and testing set (October–December).
- Build time series models (Prophet / ARIMA) to forecast:
  - λ(t): Borrow arrival rate
  - μ(t): Return arrival rate
- Predict future hourly station demand and net flow.

✅ **Output:** Hourly net flow forecasts per station.

---

### 3. Queueing Simulation (Inventory Dynamics)
- Assume initial bike inventory at each station.
- Simulate inventory trajectories over time based on predicted net flow.
- Define safe inventory thresholds (e.g., minimum 10 bikes, maximum 90% full).
- Identify rebalancing needs:
  - Stations needing pickups (overflow)
  - Stations needing deliveries (shortage)

✅ **Output:** Rebalancing demand table (pickup/drop-off per station per hour).

---

### 4. Routing Optimization (VRP)
- Build rebalancing requests based on simulation results.
- Calculate station-to-station distance matrix (using Haversine formula or Google Maps API).
- Solve the Vehicle Routing Problem (VRP) using Google OR-Tools.
- Generate optimized dispatch routes for rebalancing vehicles.

✅ **Output:** Daily optimized rebalancing routes for trucks.

---

### 5. Interactive Dashboard
- Build a web dashboard (Streamlit) to visualize:
  - Station inventory forecast curves
  - Rebalancing demand table
  - Optimized dispatch routes (interactive map)

✅ **Output:** An operational decision support dashboard for rebalancing management.

---

## 📂 Repository Structure

```
citibike-intelligent-rebalancing/
├── notebooks/               # Main notebooks for each step
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_time_series_forecasting.ipynb
│   ├── 03_queueing_simulation.ipynb
│   ├── 04_vrp_optimization.ipynb
│   └── 05_dashboard_visualization.ipynb
├── scripts/                  # Python modules for data processing, modeling, and optimization
├── data/                     # Sample datasets or processed outputs
├── figures/                  # Generated plots and visualization outputs
├── docs/                     # (Optional) Project documentation
├── README.md                  # Project overview and instructions
├── requirements.txt           # Python environment dependencies
└── .gitignore                 # Files and folders to exclude from Git
```

---

## 🛠 Technologies Used

- **Data Processing:** Python (Pandas, PySpark), Delta Lake
- **Time Series Modeling:** Prophet, ARIMA (Statsmodels)
- **Queueing Theory Simulation:** Custom discrete-event simulation
- **Routing Optimization:** Google OR-Tools (VRP Solver)
- **Visualization:** Folium, Plotly, Matplotlib, Seaborn
- **Dashboard Deployment:** Streamlit
- **Geospatial Distance Calculation:** Haversine Formula

---

## 🚀 Future Enhancements
- Integrate real-time weather and event data into demand forecasts.
- Extend VRP models to support multiple vehicle types and capacities.
- Deploy the dashboard online (e.g., Streamlit Sharing, AWS, or GCP).
- Implement real-time rebalancing recommendation systems.

---

## 🤝 Contributions
Contributions, ideas, and feedback are welcome!  
Feel free to submit pull requests or raise issues.

---

## 📜 License
This project is licensed under the **MIT License**.
