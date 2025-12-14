# NPRI Time-Series Forecasting: Coal Phase-out Impact Prediction

## Project Objective (Policy-Driven Forecasting)

This project addresses a critical environmental policy question: **Predict the total annual pollutant releases (in kilograms) from the fossil-fuel powered electricity generation sector in the year 2030, assuming a complete phase-out of coal-fired power plants.**

This is framed as a **Time-Series Regression** challenge using the National Pollutant Release Inventory (NPRI) dataset, requiring advanced data preparation and specialized mathematical modeling to forecast the complex non-linear trend of releases from the remaining non-coal facilities.

## Methodology and Technical Execution

### Technologies Used

* **Language:** Python
* **Environment:** Jupyter Notebook / Google Colab
* **Core Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy.optimize` (for curve fitting)

### Data Engineering and Target Construction

A major component of this project was transforming the raw NPRI data to create the specific prediction target:

1.  **Unit Standardization:** The original 737,516 records contained releases across 12 pathways in mixed units (g, kg, tonnes). All pathways were summed and standardized to a single unit: **kilograms (kg)**.
2.  **Sector and Coal Isolation:** Data was filtered for the Fossil-fuel electric power generation sector ($\text{NAICS } 221112$). A feature was engineered (`is_using_coal`) by identifying $\text{28}$ coal facilities (releasing $\ge 5 \text{ kg}$ of Mercury).
3.  **Final Target:** The $\text{28}$ coal facilities were **excluded** to simulate the phase-out. The final time-series target is the aggregated total annual releases (in kg) for the remaining **non-coal facilities** by year.

### Modeling Strategy: Non-linear Trend Forecasting

Due to the expectation that environmental releases follow a non-linear, asymptotic trend (releases decrease rapidly initially and then level off), a standard linear regression is unsuitable.

The model uses a custom implementation of the **Declining Logistic (S-Curve) Function** to accurately fit the historical trend and forecast the total releases for the year 2030. This function is ideal for modeling scenarios that approach a fixed minimum or maximum boundary over time.



The fitted curve provides a mathematically sound forecast of the expected environmental impact from the remaining non-coal sources after the major policy intervention (coal phase-out).

## Project Setup

To clone and execute this analysis locally, use the following commands.

```bash
git clone [Your Repository URL Here]
cd NPRI-Coal-Phaseout-2030-Forecasting
pip install -r requirements.txt
jupyter notebook Model_integrated_2400&3510_DataStorm_V6.ipynb
