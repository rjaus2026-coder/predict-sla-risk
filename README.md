# Predicting SLA Risk for Cycle Stock Orders (US & Canada)

This project evaluates **when SLA risk prediction adds operational value** by applying the same analytics framework to cycle stock orders in the United States and Canada.

Rather than optimizing model performance for its own sake, the analysis is designed to determine whether **SLA misses can be meaningfully anticipated at order creation**, and how that value changes with **operational stability, data quality, and execution maturity**.

The work complements prior availability and dispatch analysis by explicitly testing the **limits of prediction**, not just reporting outcomes.

---

## What This Project Demonstrates

- Practical application of predictive analytics to a real supply chain problem  
- How operational context, not algorithms, governs predictive value  
- Clear distinction between exception-driven failures and systemic variability  
- Why improving operations naturally reduces predictability  
- Risk scoring as a prioritization tool, not an automation mechanism  
- A disciplined framework for deciding when not to deploy ML  

---

## Dataset Overview

Two anonymized datasets were analyzed:

### United States
- Two distribution warehouses  
- Higher order volume  
- Greater upstream replenishment complexity  
- Low SLA miss rates with exception-driven failures  

### Canada
- Single warehouse  
- Lower volume  
- Fewer structural disruptions  
- Historically higher SLA miss rates with systemic patterns  

All identifying attributes (customers, SKUs, internal codes, locations) were anonymized prior to analysis.  
Raw data files are intentionally excluded from this repository.

---

## Scope and Timeframe

- Analysis window: January 2023 – March 2025  
- Included items: Cycle stock only (Move Codes 1–3)  
- Excluded: Non-stock, exception, and irregular items  

The timeframe intentionally captures:
- Pre-intervention instability  
- Transitional corrective actions  
- Stabilized execution with measurable improvement  

---

## SLA Definitions (Critical to Interpretation)

The analysis measures **SLA risk**, defined as the probability that a cycle stock order will miss its applicable service-level agreement.

SLA rules are designed to reflect how the operation actually functions, not an idealized calendar.

### Shared Operational Rules (US and Canada)

- Orders placed after 2:00 p.m. on Thursday may still be considered on time if shipped on Monday  
- Orders placed on Friday may still be considered on time if shipped on Monday  
- Weekend orders receive their SLA clock starting Monday morning  

These rules prevent artificial penalties caused by non-working days and fixed dispatch cutoffs.

### United States SLA
- Baseline SLA: ship within 24 hours of sales order creation for in-stock items  
- SLA clock respects the shared exception rules above  

### Canada SLA
- Baseline SLA: ship within 2 calendar days of sales order creation  
- SLA clock respects the same shared exception rules as the US  

---

## Method Summary

- Load and normalize each regional dataset  
- Filter to:
  - Analysis window: Jan 2023 – Mar 2025  
  - Cycle stock only: Move Codes 1–3  
- Apply region-specific SLA logic and compute `sla_met`  
- Engineer creation-time features only to prevent leakage  
- Train interpretable baseline models (Logistic Regression)  
- Evaluate:
  - Predictive signal (ROC-AUC, PR-AUC)  
  - Threshold-based tradeoffs (precision vs recall)  
  - Operational usability of risk scores  

No execution-stage data is used. This constraint is intentional.

---

## Key Findings

### United States
- SLA miss rates are low (~9–13%)  
- Failures are largely exception-driven  
- Creation-time features provide minimal predictive signal  
- Threshold tuning does not produce operationally usable tradeoffs  

### Canada
- SLA miss rates historically higher (~28–33%)  
- Misses exhibit repeatable patterns  
- Risk scoring provides actionable prioritization  
- Between Q1 2023 and Q1 2025:
  - 107 fewer SLA misses  
  - Miss rate reduced from 42.7% to 28.1% at higher volume  

As execution stabilized, predictive signal diminished, indicating that remaining failures are increasingly exception-driven.

---

## Key Outputs

### Notebooks
- US analysis: `notebooks/predict_sla_risk_us.ipynb`  
- Canada analysis: `notebooks/predict_sla_risk_ca.ipynb`  

Each notebook is fully runnable top-to-bottom and documents assumptions and limitations in plain language.

## Project Artifacts

This repository intentionally focuses on **analysis and decision logic**, not production outputs.

- No trained models are persisted
- No charts or tables are exported
- No automated scoring pipelines are implemented

All results are generated **in-notebook** to support interpretation, validation, and discussion rather than downstream automation.

This design choice reflects the project’s core finding: predictive modeling should be applied selectively and only where it provides operational leverage.

---

## Interpretation and Actionability

This project demonstrates that **predictive analytics value is context-dependent**.

- In stable environments, analytics should focus on:
  - Exception detection  
  - Root-cause analysis  
  - Execution-stage monitoring  

- In unstable or transitioning environments:
  - Risk scoring can support disciplined triage  
  - Thresholds should be chosen based on capacity, not accuracy  

As operations mature, the role of analytics must shift accordingly.

---

## How Often This Should Be Run

- Monthly: trend review and risk stratification  
- Quarterly: model review only if operating context materially changes  

Running this more frequently adds noise without increasing insight.

---

## How to Run This Project

1. Install dependencies:
   - pandas  
   - numpy  
   - scikit-learn  
   - matplotlib  

2. Place pre-anonymized data in a local `data/` directory  
3. Open either notebook and run all cells top-to-bottom  

To reuse the framework, ensure the same column structure and apply the appropriate SLA rules.

---

## Why This Matters

This project demonstrates disciplined analytics leadership:

- Knowing when prediction helps and when it does not  
- Avoiding “AI for AI’s sake”  
- Aligning analytics effort with real operational leverage  
- Treating predictive models as decision-support tools, not automation engines  

The outcome is not a model, but a **repeatable decision framework** for applying analytics responsibly in supply chain operations.
