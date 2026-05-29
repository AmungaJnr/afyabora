# AfyaBora — AI-Powered Predictive Public Health Platform

**Founder:** Amunga Junior  
**Status:** Research prototype v0.1  
**Last updated:** May 2026

---

## What is AfyaBora?

AfyaBora (Swahili for "Better Health") is an AI platform designed to predict and monitor three interconnected public health threats:

- Infectious disease outbreaks (influenza, respiratory viruses)
- Climate-related health risks (heatwaves, hospitalization pressure)
- Respiratory health degradation from air quality events

The platform integrates Canadian public health surveillance data and  climate data through a five-layer architecture: data ingestion, AI/ML modelling, cloud infrastructure, decision-support interfaces, and a governance framework designed for equity and privacy.

---

## Repository structure
afyabora/
├── data/               ← cleaned datasets and model outputs
├── notebooks/          ← sprint notebooks (one per build sprint)
│   ├── sprint1_fluwatch.ipynb
│   ├── sprint2_sir_model.ipynb
│   ├── sprint3_climate_merge.ipynb
│   └── sprint4_xgboost_forecast.ipynb
├── src/                ← reusable Python modules (coming soon)
├── README.md
└── requirements.txt

---

## What has been built so far

**Sprint 1 — FluWatch data pipeline**  
Loads and cleans PHAC FluWatch influenza surveillance data (2014–2017). Plots national and provincial epi curves.

**Sprint 2 — SIR epidemiological model**  
Implements and fits a Susceptible-Infectious-Recovered model to the  2014-2015 flu season. Derives R₀ and identifies seasonal forcing as a key limitation of the basic SIR model.

**Sprint 3 — Climate-health correlation**  
Merges ECCC Toronto climate data with flu surveillance data. Finds r = -0.66 (p < 0.001) - strong statistically significant negative correlation between temperature and flu cases. Confirms AfyaBora's climate-health hypothesis with real data.

**Sprint 4 — XGBoost forecasting model**  
Trains an XGBoost model on engineered lag features to forecast weekly flu case counts. Achieves MAE = 226 cases, MAPE = 41.3% on the 2016-2017 season. Identifies flu_lag1 as the dominant predictor (72.8% feature importance). Operational utility confirmed - statistical 
accuracy limited by small training dataset.

---

## Key findings

- Temperature and flu cases: r = -0.66, p < 0.001
- Model 1 peak timing: correct
- Model 1 MAPE: 41.3% (target: <20% with more training data)
- Primary limitation: 3 seasons of training data — expanding to 
  10+ seasons is the highest-priority improvement

---

## How to run

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/afyabora.git
cd afyabora

# Create virtual environment
python -m venv venv
venv\Scripts\Activate.ps1  # Windows

# Install dependencies
pip install -r requirements.txt

# Open notebooks
jupyter notebook
```

---

## Data sources

- **PHAC FluWatch** - Canadian influenza surveillance 
  (health.canada.ca)
- **ECCC Historical Climate Data** - Toronto City Centre weather station 
  (climate.weather.gc.ca)

---

## Contact
Email - jnramunga@gmail.com
Amunga Junior - AfyaBora Research Platform  
Building toward national public health infrastructure integration.