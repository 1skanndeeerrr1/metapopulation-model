# Metapopulation Model of Disease Incidence Peaks in Russian Cities

A metapopulation SIR model that incorporates inter-city transport flows to improve the prediction of epidemic peak timing across major Russian cities.

---

## Preliminary Data Analysis

Before building the model, we analyzed weekly morbidity data for 12 major Russian cities (1985–2016).

**Key findings:**

- There is a **high and statistically significant correlation** in the dynamics of disease incidence between cities (Pearson correlation coefficients mostly range from 0.65 to 0.88).
- Particularly strong synchronization is observed between geographically and transport-linked cities (e.g., Moscow – Saint Petersburg, Yekaterinburg – Chelyabinsk – Perm, Novosibirsk – Omsk).
- A total of **66 significant correlation pairs** were identified (p < 0.01).

These results indicate that epidemic waves in different cities are not independent. One of the important mechanisms behind this synchronization is **inter-city transport flows**.

Full analysis code, correlation matrices, and heatmap are available in the notebook:

📄 [`corr.ipynb`](corr.ipynb)

---

## Model Overview

The project implements a **metapopulation SIR model** for 12 large Russian cities:

- Moscow  
- Saint Petersburg  
- Novosibirsk  
- Yekaterinburg  
- Nizhny Novgorod  
- Samara  
- Omsk  
- Kazan  
- Chelyabinsk  
- Ufa  
- Perm  
- Rostov-on-Don  

**Main features:**

- Realistic (expert-based) mobility matrix between cities
- Automatic calibration of parameters on 2009 data
- Out-of-sample validation on multiple years (2011, 2003, 2007, 2013, 2015)
- Comparison of peak timing prediction accuracy **with** and **without** transport flows
- Extended set of evaluation metrics (MAE, RMSE, Hit Rate, correlation, etc.)

**Key result:**  
Accounting for transport flows consistently reduces the error in predicting epidemic peak weeks (often by a factor of 2–4).

---

## Quick Start

```bash
# Install dependencies
pip install pandas numpy scipy matplotlib openpyxl seaborn

# Place the data file in the project directory
# Zab_v_bolshikh_gorodakh.xlsx

# Run the full pipeline
python model.py

The script will:

Calibrate the model on 2009 data
Validate it on several other years
Compute detailed metrics
Generate comparison plots for all years
Save results to Excel files
