# Metapopulation-model.
# A metapopulation model of disease spread between major cities in Russia.

The model shows how transport flows between the 12 largest cities in Russia affect the timing of peak epidemics of ARVI/influenza.

Using real data on disease incidence for 2000–2015, the model demonstrates that taking inter‑city passenger flows into account makes it possible to predict with significantly greater accuracy when a peak in disease incidence will occur in different cities.

## What this project does.

- Builds a metapopulation SIR model for 12 cities
- Uses a realistic matrix of transport flows (not pure gravity)
- Automatically calibrates parameters using 2009 data
- Checks the quality in other years (2011, 2007, 2013, 2015, etc.)
- Compares the accuracy of peak forecasts **with transport** and **without transport**

**Key Finding.**  
In all the years tested, the model with traffic flows predicts peak times significantly more accurately (the error is usually 2–4 times smaller).

## Quick start.

```bash
# 1. Install dependencies
pip install pandas numpy scipy matplotlib openpyxl

# 2. Place the data file next to the script
# Zab_v_bolshikh_gorodakh.xlsx

# 3. Run
python metapop_realistic.py


├── metapop_realistic.py          # main script
├── Zab_v_bolshikh_gorodakh.xlsx  # initial data
