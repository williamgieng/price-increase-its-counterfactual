# Interrupted Time Series Counterfactual: Price Change Impact on Churn

This repository demonstrates how to estimate the impact of a **global price change** on **customer churn** using **Interrupted Time Series (ITS)**.

Because the price increase was applied to all customers simultaneously, no untreated control group exists. The analysis therefore constructs a **model-based counterfactual** by projecting pre-intervention behavior into the post period under a no-intervention assumption.

All data in this repository is **synthetic** and generated solely for demonstration purposes.

---

## Problem Statement

When a price change is rolled out globally, traditional A/B testing is not possible. However, stakeholders still need an estimate of:

- whether churn increased due to the price change
- how large the impact was
- whether the observed change exceeds normal time-series variation

This notebook shows how **Interrupted Time Series** can be used to answer those questions under realistic constraints.

---

## Method Overview

The analysis follows a standard segmented regression ITS design:

- Baseline trend estimation using pre-intervention data
- Immediate **level change** at the intervention point
- **Slope change** after the intervention
- Explicit construction of a **counterfactual (no price change)** trajectory

Key methodological components include:
- Segmented regression (level + slope change)
- Model-based counterfactual prediction
- Robust inference using **Heteroskedasticity- and Autocorrelation-Consistent (HAC / Newey–West)** standard errors
- Residual diagnostics via **ACF/PACF**
- Validation using placebo intervention tests
- Sensitivity checks on autocorrelation window and pre-period length

---

## What the Notebook Contains

The notebook walks through the full workflow step by step:

1. Synthetic time-series generation with trend, seasonality, and noise  
2. Construction of ITS features (`time`, `post`, `time_since_intervention`)  
3. Segmented regression model fit  
4. Counterfactual prediction (no-intervention scenario)  
5. Pointwise and cumulative impact estimation  
6. Residual diagnostics (ACF/PACF)  
7. Placebo (falsification) tests  
8. Sensitivity analyses  

Each chart includes an explanation directly below it to clarify what is being shown and why it matters.

---

## Interpretation

- The **counterfactual** represents what churn would have been had the price change not occurred, assuming pre-intervention dynamics continued.
- The difference between observed churn and the counterfactual in the post period represents the estimated **incremental impact** of the price change.
- HAC standard errors ensure statistical inference remains valid in the presence of autocorrelation and changing variance.

---

## How to Run

```bash
pip install -r requirements.txt
