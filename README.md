# Interrupted Time Series Counterfactual: Global Price Change Impact on Churn

This repository demonstrates how to estimate the impact of a **global price change** on **customer churn** using a **single-series Interrupted Time Series (ITS)** design.

When a price change is applied to **everyone at once**, there is no untreated control group and a classic A/B test is not possible. The analysis therefore constructs a **model-based counterfactual** by projecting pre-intervention dynamics into the post period under a no-intervention assumption.

All data in this repository is **synthetic** and generated solely for demonstration purposes.

---

## Why this example exists

Not every important business decision can be tested cleanly.

In practice, some of the most consequential interventions happen under real-world constraints:

- price changes applied globally
- policy rollouts
- product changes that affect all users
- infrastructure or experience changes with no holdout group

In these settings, teams still need to answer questions like:

- Did churn actually increase because of the intervention?
- How large was the impact?
- Was the observed change larger than normal trend, seasonality, and noise?

This example shows one way to approach that problem more rigorously than a naive before-and-after comparison.

---

## What this repository demonstrates

The notebook walks through a complete ITS workflow for a **global treatment / no-control-group** setting:

1. Generate a realistic synthetic churn time series
2. Define the intervention date and ITS features
3. Fit a segmented regression model
4. Construct the no-intervention counterfactual
5. Estimate pointwise and cumulative impact
6. Diagnose residual autocorrelation with ACF / PACF
7. Run placebo (falsification) checks
8. Test sensitivity to modeling choices

The output is meant to be both:
- **methodologically credible** enough to demonstrate the core approach
- **business-readable** enough to explain the logic to nontechnical stakeholders

---

## Method overview

The notebook uses a standard segmented regression ITS design with:

- baseline time trend
- intervention level change
- post-intervention slope change
- month seasonality
- a contemporaneous business covariate
- HAC / Newey–West standard errors for more robust inference under autocorrelation

The core idea is to estimate:

- what happened after the intervention
- what would likely have happened **without** the intervention
- the gap between those two paths

That gap is the estimated **incremental effect**.

---

## Why this is better than a simple before-and-after

A naive before-and-after comparison treats every post-period change as if it were caused by the intervention.

That is often misleading.

ITS is more credible because it explicitly accounts for:

- pre-existing trend
- seasonality
- noise
- post-period divergence from the modeled no-intervention path

It is still not a replacement for a clean randomized experiment. But when a full-population intervention makes experimentation impossible, it is often a much stronger alternative than simple descriptive comparison.

---

## What the notebook includes

The notebook includes:

- a synthetic weekly churn time series
- a modeled counterfactual (no price change)
- a visual chart showing the **counterfactual**, **intervention date**, and **highlighted causal effect**
- residual diagnostics
- placebo intervention tests
- sensitivity checks for HAC lag choice and pre-period length
- a short business interpretation section at the end

Each major chart is followed by a plain-English explanation of what it shows and why it matters.

---

## When this approach is appropriate

A single-series ITS design is most useful when:

- the intervention affects the full population
- no clean control group exists
- the intervention timing is known
- enough pre-period history is available

It becomes less credible when:

- multiple major interventions overlap heavily
- structural breaks make the pre-period unreliable
- the post-period is too short
- important confounders are completely unobserved and unstable

---

## Key assumptions

This example relies on several important assumptions:

1. Pre-intervention dynamics are informative about the no-intervention path.
2. No other major concurrent intervention fully explains the post-period shift.
3. Trend and seasonality are modeled reasonably well.
4. Residual autocorrelation is handled appropriately in inference.

These assumptions should always be discussed explicitly in real work.

---

## Repository contents

- `ITS_PriceIncrease_Counterfactual.ipynb` — main notebook walkthrough
- `requirements.txt` — Python dependencies
- `README.md` — repository overview

---

## How to run

```bash
pip install -r requirements.txt
jupyter notebook Price_Increase_ITS_Counterfactual.ipynb
```

---

## Takeaway

The main lesson is simple:

When a global intervention makes A/B testing impossible, the right question is not just **“what changed?”**

It is:

**“What would likely have happened if the intervention had not occurred?”**

That is the counterfactual question, and it is the heart of causal measurement in imperfect real-world settings.
