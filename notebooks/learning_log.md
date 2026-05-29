# AfyaBora Learning Log

## Context
I am Amunga, founder of AfyaBora - an AI-powered predictive public health 
platform. I am at Year 0 building skills and a prototype. 

Completed sprints:
- Sprint 1: Loaded, cleaned and plotted PHAC FluWatch data in VS Code with Python.
  Clean data saved at data/fluwatch_clean.csv
- Sprint 2: Implemented SIR model in Python, fitted it to 2014-2015 flu season.
  Fitted results saved at data/sprint2_results.json
  Key finding: basic SIR model misses seasonal forcing - explains why AfyaBora 
  needs climate inputs in Layer 2.

Next sprint: Sprint 3 — merging climate data with flu data and computing 
correlations.

Environment: VS Code, Python 3.11, venv at C:\Users\jnram\afyabora\venv

# AB Model 1, v0.1
## Sprint 1 - FluWatch data pipeline
**What I built:** 
Data ingestion pipeline pulling PHAC FluWatch CSV, 
cleaning footnotes, decoding epidemiological week numbers into real dates, 
plotting national flu epi curve 2014-2017.

**What clicked:** 
Boolean indexing for filtering rows. The seasonal pattern 
in flu data. Why surveillance data undercounts reality.

**Still fuzzy:** Nothing

---

## Sprint 2 - SIR model
**What I built:** 
Implemented SIR differential equations in Python, ran with 
initial guess, fitted beta and gamma using scipy minimize with bounds and 
multiple starting points.

**What clicked:** 
The the basic SIR model is just but the foundation and needs to be retrofitted to meet the demand that AB wants to tackle. The R₀ of 7.48 shows that seasonal forcing is required.

**Still fuzzy:** 
- What odeint is actually doing mathematically step by step
- Why L-BFGS-B was chosen as the optimization method
- What seasonal forcing means in code - how would you actually add it
- Why the except block hides errors and when to use it vs not

**Key concepts learned:**
- S, I, R compartments and what they represent
- R₀ = beta/gamma and what it means for outbreak growth
- Local minima - optimizer getting stuck in wrong solutions
- Why the basic SIR model needs seasonal forcing to match real flu data
- Why the except block was hiding real errors

---

## Sprint 3 - Climate data merge and correlation

**What I built:** 
Pulled ECCC daily temperature data for Toronto, 
cleaned and aggregated to weekly, merged with flu surveillance data,
computed Pearson correlation, plotted dual-axis climate-health chart.

**Key finding:** 
r = -0.66, p < 0.001 - strong statistically significant 
negative correlation between temperature and flu cases. 
AfyaBora's climate-health hypothesis is supported by the data.

**What clicked:** I am finally getting familiar with the code, my ability to independently decipher what it is doing and why it is needed. The interpretation of data has been easy for me since the beginning. AB's structure, need and flow is coming to life and I see the progression. 

**Still fuzzy:** 
- Pearson correlation code; like what it is exactly and why that particular method was used. Why not another correlation method?

**Concepts learned:**
- Pearson correlation and what r and p-value mean
- Why inner merge keeps only matching dates
- Interpolation for filling missing temperature values
- Dual axis charts for comparing two different scales
- Epidemic exhaustion - why flu peaks before coldest temperatures

**Why Pearson?**
There are several correlation but the three most common are:
1. Pearson - measures linear relationships between two continuous numerical variables. Assumes both variables are normally distributed and that the relationship is in a straight line. This applies for temp and flu cases as both are continuous numbers and their relationship is roughly linear. An increase in temp by 5 degrees, cases go up by roughly a proportional amount.

2. Spearman - measures monotonic relationships; one variable consistently increases as the other increases or decreases but not necessarily in a straight line. Works best with rankings especially where data has outliers or isn't normally distributed.

3. Kendall - similar to Spearman but more robust with small datasets or many tied values. Less commonly used in epidemiology.

Temp and flu data match Pearson and the p_value and r show this. However, Pearson assumes that temp has an immediate effect on flu. But there is a lag effect; cold weather this week drives people indoors in which infections will show up in surveillance 1-2 weeks later.

Sprint 4 will address this lag effect.

Sprints 1-3 mark the end of AB Model 0.


## Sprint 4 — XGBoost forecasting model

**What I built:** 
Trained my model using XGBoost for forecasting. Split the data into a training and testing set. 

**Key finding:** 
The model for operationall utility is works but in terms of statistical accuracy it off. With a target of 20%, a MAPE of 41.2% is way off. The problem is the peak seasons. The data used lacks the variety that the power of XGBoost would cherish hence when it gets to the peak, it has issues predicting accurately. It seems to be overfitting.

The current influencer in the model's predictive powers is the last week's numbers to predict the next week's. Other features have close to 36% of the remaining influence. A data variety once more.

**What clicked:** 
That the model works well, operationally. Statistically, a larger data set with better population-level info would have aided a better modelling of the data.

**Still fuzzy:** 
How this can be rectified. Wondering if I need use an entirely new data.

**Concepts learned:**
- Feature engineering and lag features
- Why time series data must never be shuffled
- Train/test split by season not randomly
- XGBoost — gradient boosting and weak learners
- MAE, RMSE, MAPE  - what each measures and when each matters
- Feature importance  - what the model relied on most
- Autoregressive models  - predicting a variable from its own past
- Statistical accuracy vs operational utility