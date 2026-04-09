# Price Increase Analysis with Interrupted Time Series (ITS)

## Why this matters

Not every important business decision can be tested cleanly.

Price changes, policy rollouts, and product shifts often affect every user at once. There is no control group. The experiment is never run.

And yet, teams still need to answer a critical question:

**Did the intervention actually work?**

The most common mistake is to rely on simple before-and-after comparisons. But those often confuse natural trends, seasonality, or external factors with real impact.

This notebook shows how to build a credible counterfactual using interrupted time series (ITS), allowing you to estimate what would have happened without the intervention.

---

## The problem

Suppose a company introduces a price increase.

After the change, a key metric (e.g., churn, engagement, or conversions) shifts. The immediate temptation is to attribute that change to the price increase.

But that conclusion is often wrong.

A naive before-and-after comparison assumes:

- nothing else changed  
- no underlying trends were present  
- no seasonality or external factors influenced the metric  

In reality, those assumptions rarely hold.

---

## The common mistake

A simple comparison might suggest:

> “The metric changed after the intervention, so the intervention caused the change.”

But this ignores what would have happened anyway.

Without a counterfactual, it is easy to mistake:
- ongoing trends  
- random fluctuations  
- or external shocks  

for causal impact.

This leads to confident conclusions based on unreliable measurement.

---

## The approach

Interrupted Time Series (ITS) provides a more credible alternative.

Instead of comparing before vs after directly, we:

1. Model the pre-intervention trend  
2. Project that trend forward to estimate a counterfactual baseline  
3. Compare the observed post-intervention data to that baseline  

The difference between:
- what actually happened  
- and what would have happened without the intervention  

is the estimated impact.

---

## What this notebook demonstrates

This notebook uses a synthetic dataset to illustrate:

- a realistic pre-intervention trend  
- an intervention point (price increase)  
- post-intervention observations  
- a counterfactual projection based on pre-intervention behavior  

The goal is not to build the most complex model, but to show:

**how to reason about causal impact when experiments are not possible**

---

## Key takeaway

Without a counterfactual, it is easy to attribute changes to an intervention that had no real effect.

Better measurement does not just improve analysis.

**It prevents the wrong decisions.**

---

## Limitations

Interrupted time series relies on an important assumption:

> the pre-intervention trend would have continued unchanged in the absence of the intervention.

If that assumption is violated (e.g., due to structural breaks or external shocks), the estimates may be biased.

Like all causal methods, ITS requires careful judgment in both modeling and interpretation.

---

## When to use this approach

ITS is especially useful when:

- no clean control group exists  
- the intervention affects all users at once  
- historical data is available  
- trends can be reasonably modeled  

Common examples include:

- price changes  
- policy rollouts  
- infrastructure or system changes  
- company-wide product updates  

---

## Repository contents

- `ITS_PriceIncrease_Counterfactual.ipynb` – main notebook demonstrating the approach  
- synthetic dataset generation and modeling steps  
- visualizations comparing observed vs counterfactual outcomes  

---

## Final thought

Rigor matters most when the conditions are imperfect.

That is exactly when the pressure to cut corners is highest—and exactly when bad measurement is most likely to send a strategy in the wrong direction.
