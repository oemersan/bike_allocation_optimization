#  Optimization of Bicycle Allocation in Urban Rental Systems

###  Team Members
- **Ömer Faruk San**  `san22@itu.edu.tr`
- **Mustafa Kerem Bulut**  `bulut22@itu.edu.tr`
- **Abdullah Vefa Yankın** `yankin22@itu.edu.tr`

---

##  Project Description

This project focuses on optimizing the **initial allocation of bicycles** in a bike-sharing system to **minimize customer dissatisfaction** caused by station overflows and underflows. We use **real-world data** from the Konya Metropolitan Municipality's bike-sharing network and formulate **Linear Programming (LP)** models to determine optimal allocations across docking stations.

The solution can also be adapted for other shared mobility systems such as e-scooters or portable battery rentals.

---

##  Problem Definition

Urban bike-sharing systems often suffer from:
-  **Stockout** (no bikes to rent)
-  **Overflow** (no empty slots to return)

The goal is to find the optimal bike distribution at the start of each day/month so that these events are minimized.

---

## 📂 Dataset

Data is sourced from **Konya ULASAV Open Data Platform**:

1. **Bike Usage Data**: Individual rentals/returns (2022–2023)  
   🔗 [Dataset Link](https://ulasav.csb.gov.tr/dataset/42-kiralik-bisiklet-kullanim-verileri)

2. **Station Metadata**: Locations and capacities of bike stations  
   🔗 [Dataset Link](https://ulasav.csb.gov.tr/dataset/42-paylasimli-kiralik-bisiklet-istasyonlari-konumlari)

---

##  Preprocessing

- Encoding fixes for Turkish characters
- Consolidation of monthly Excel files
- Filtering valid station codes (e.g., starting with "KON")
- Daily/weekly rental and return aggregation
- Net bike flow per station calculated:  
  `net_flow = avg_returns - avg_rentals`

---

##  Optimization Models

We developed four LP models using `PuLP` in Python:

| Model | Objective |
|-------|-----------|
| Model 1 | Minimize customer dissatisfaction (weighted over/underflows) |
| Model 2 | Maximize number of days until system failure |
| Model 3 | Same as Model 2 but with balanced allocation |
| Model 4 | Same as Model 3 with a minimum initial bike constraint (≥2) |

Each model balances trade-offs between **fairness**, **operational longevity**, and **minimized user frustration**.

---

##  Results Summary

- **Model 1** minimizes short-term dissatisfaction
- **Model 2 & 3** increase operational lifespan (e.g., 36 days)
- **Model 4** ensures realistic minimum bike numbers (≥2 per station), operational for 24+ days

All models run efficiently in seconds using the **CBC solver** in PuLP.

>  You can add your result figures here:
> 
> ![Model 1 Allocation](results/model1_allocation.png)  
> ![Model 2 Time Maximization](results/model2_operational_time.png)

---

##  How to Run

### Prerequisites
- Python ≥ 3.8
- `pulp`, `pandas`, `matplotlib`, `seaborn`

```bash
pip install pulp pandas matplotlib seaborn
