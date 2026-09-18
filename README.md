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
python metapop_realistic.py
```

The script will:
1. Calibrate the model on 2009 data
2. Validate it on several other years
3. Compute detailed metrics
4. Generate comparison plots for all years
5. Save results to Excel files

---

## Project Structure

```
├── corr.ipynb                        # Correlation analysis of morbidity data
├── metapop_realistic.py              # Main model script
├── Zab_v_bolshikh_gorodakh.xlsx      # Source morbidity data
├── realistic_calibration_2009.xlsx
├── realistic_validation_*.xlsx
├── metrics_summary_all_years.xlsx
├── mae_comparison.xlsx
├── realistic_mobility_matrix.xlsx
├── all_years_peaks_comparison.png
└── peaks_YYYY.png                    # Individual year plots
```

---

## How the Model Works

### Mobility Matrix
Instead of a pure gravity model, the project uses an **expert-based mobility matrix** that reflects the real structure of passenger flows in Russia:

- Moscow as the main hub
- Strong Moscow – Saint Petersburg corridor
- Trans-Siberian route
- Ural cluster (Yekaterinburg – Chelyabinsk – Perm – Ufa)

The matrix is scaled by a single calibrated parameter (`mobility_scale`).

### Calibration
Parameters (`β`, `γ`, mobility scale, and initial seed size) are automatically calibrated on 2009 data by minimizing the mean absolute error (MAE) of peak weeks using the Nelder-Mead algorithm.

### Evaluation Metrics
- MAE, RMSE, Median AE, Max AE
- Bias
- Hit Rate (±1 week and ±2 weeks)
- Pearson and Spearman correlation of peak timing

---

## Results Summary (example)

| Year | MAE with transport | MAE without transport |
|------|--------------------|-----------------------|
| 2009 | ~1.11 weeks        | ~4.49 weeks           |
| 2011 | ~1.18 weeks        | ~4.20 weeks           |
| 2015 | ~0.60 weeks        | ~3.93 weeks           |

---

## Limitations

- The mobility matrix is expert-based, not derived from real passenger statistics.
- Calibration is performed only on peak timing (not on the full epidemic curve).
- The same transmission parameters are used for all cities.
- Seasonal forcing is not explicitly included.

---

## Future Improvements

- Replace the expert matrix with real railway + air passenger data
- Add seasonal forcing β(t)
- Calibrate on the full incidence curves
- Perform multi-year joint calibration
- Add uncertainty quantification

---

## License

MIT
```
