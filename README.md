# 🚗 Dynamic Pricing for Urban Parking Lots  
*Capstone Project Submission — Summer Analytics 2025*  
by [Priyanshu Sharma](mailto:priyanshusharmajnv07@gmail.com)

---

## 📌 Project Overview

Urban parking lots face a critical challenge: static pricing leads to overcrowding in some lots and underutilization in others. This project builds a real-time, dynamic pricing system for 14 parking lots using historical patterns, live congestion data, vehicle types, and competitive pricing.

The solution includes:

- A **baseline linear model** using occupancy
- A **demand-based model** using multi-feature elasticity
- A **competitive pricing model** using geographic proximity & rerouting logic
- A real-time simulation architecture using **Pathway**
- Beautiful **Bokeh visualizations** of price fluctuations
- A complete, well-commented, and reproducible codebase

---

## 🧠 Model Formulas Used

### 📈 Model 1 – Linear Pricing
A basic pricing strategy using occupancy:

Price_t+1 = Price_t + α × (Occupancy / Capacity) × 10


- Starts at base price of $10
- α = 0.05 (tunable hyperparameter)

---

### 📊 Model 2 – Demand-Based Pricing
A more intelligent pricing model combining multiple demand-driving factors:

Demand Score = α × (Occupancy / Capacity)
+ β × QueueLength
- γ × Traffic
+ δ × SpecialDay
+ ε × VehicleTypeWeight


Then the price is updated as:

Price = BasePrice × (1 + λ × NormalizedDemand)


- NormalizedDemand ∈ [0, 1]
- Bounded: $5 ≤ Price ≤ $20  
- VehicleTypeWeight:  
   - car: 1.0  
   - bike: 0.5  
   - truck: 1.5  

---

### ⚔️ Model 3 – Competitive Pricing
Simulates market-like behaviour using competitor prices and location intelligence.

Steps:
1. Calculate distance to nearby parking lots using the Haversine formula:
Distance = 2 × R × arcsin(√(sin²((Δlat)/2) + cos(lat1) × cos(lat2) × sin²((Δlon)/2)))
2. Logic:
   - If current lot is full & competitor nearby is cheaper → **suggest rerouting / reduce price**
   - If competitor is more expensive → **increase own price slightly**

New price after competition adjustment:

If Full & Cheaper Nearby:
Price = Price_Model2 × 0.9

If Competitor Expensive:
Price = Price_Model2 × 1.1

Bound: $5 ≤ Price ≤ $25


---

## 🧰 Tech Stack Used

| Component         | Technology             |
|------------------|------------------------|
| Programming       | Python (NumPy, Pandas) |
| Real-Time Engine  | [Pathway](https://pathway.com) |
| Visualization     | Bokeh                 |
| Data Manipulation | pandas, numpy         |
| Deployment Ready  | Google Colab          |

---

## 📊 Architecture Diagram


---

## 🔧 Project Workflow
Data Ingestion: Real-world simulated parking data with timestamp, occupancy, vehicle type, etc.

Preprocessing: Merged time columns, encoded traffic, cleaned strings, and mapped weights.

Model 1 - Linear:

Price increases linearly with occupancy.

Model 2 - Demand-Based:

Price is based on occupancy, traffic, queue, special day, and vehicle type.

Demand normalized to ensure smooth, explainable pricing.

Model 3 - Competitive Pricing:

Calculates geographic proximity (Haversine distance).

Adjusts price based on competitor's price and rerouting conditions.

Visualization:

Uses Bokeh to generate interactive line charts of pricing evolution across lots.

Real-Time Simulation (optional):

Template included using Pathway for real-time data streaming.

## 📁 Repository Structure
| File/Folder                      | Description                                                            |
| -------------------------------- | ---------------------------------------------------------------------- |
| `README.md`                      | 📘 Full project documentation and submission guidelines                |
| `dynamic_pricing_notebook.ipynb` | 📓 Google Colab notebook with all models, visualizations, and logic    |
| `dataset (1).csv`                | 📊 The dataset provided (73 days × 14 parking spaces × 18 time points) |
| `report_summary.pdf`             | 📝 Optional report with detailed explanation and formulas (if added)   |
| `bokeh_dynamic_pricing.html`     | 📈 Optional HTML export of all Bokeh plots                             |
| `images/`                        | 📁 Folder containing starred repo screenshots for submission           |
| ┗ `star_repo_1.png`              | ⭐ Screenshot after starring `pathway com/pathway` repo                  |
| ┗ `star_repo_2.png`              | ⭐ Screenshot after starring `pathway com/llm-app` repo                  |


## 🚦 How to Run
Upload dataset (1).csv to your Colab environment.

Open and run dynamic_pricing_notebook.ipynb.

View the pricing output and Bokeh visualizations in real-time.

(Optional) Customize Pathway hooks to ingest streaming data.

## 🔗 Required Repositories Starred ✅
✅ https://github.com/pathwaycom/pathway

✅ https://github.com/pathwaycom/llm-app



## 📄 Optional Report
A detailed project explanation is available in report_summary.pdf (if added).

## 📫 Contact
👨‍💻 Name: Priyanshu Sharma

📧 Email: priyanshusharmajnv07@gmail.com

📍 Institute: International Institute for Population Sciences (IIPS), Mumbai

🧑‍💻 GitHub Username: priyanshusharmajnv07

---

## 🧾 Conclusion

This capstone project successfully demonstrates the power of data-driven decision-making in urban infrastructure management. By integrating:

- Real-time data ingestion,
- Demand elasticity modelling,
- Competitive pricing logic based on geospatial intelligence, and
- Smooth, bounded dynamic pricing updates,

we built a system that can realistically optimize parking lot utilization, reduce traffic congestion, and improve user satisfaction.

The project also offered valuable experience in:

- Feature engineering and model design without black-box ML tools,
- Real-time simulation using Pathway,
- Interactive data visualization using Bokeh,
- Optimizing performance for large-scale time-series data.

This dynamic pricing engine is not only relevant for smart parking but its architecture can be extended to:
- Smart toll pricing
- Ride-hailing surge models
- EV charging stations
- Public transit optimization

> 📌 The project showcases how classical data science principles, when applied thoughtfully with real-time pipelines and urban intelligence, can shape smart cities of tomorrow.

---


“Great cities deserve great parking systems — and this project is one small step toward that smarter future.” 🚗📈

