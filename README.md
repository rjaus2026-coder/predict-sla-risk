# Predicting SLA Risk for Cycle Stock Orders (US vs Canada)

## Overview

This repository evaluates when SLA risk prediction adds operational value by applying the same analytics and modeling framework to cycle stock orders in the United States and Canada. Rather than optimizing for model accuracy alone, the analysis focuses on predictive signal viability, operational context, and practical decision support. The objective is to determine whether SLA misses can be meaningfully anticipated using information available at order creation, and how that value differs across regions operating under similar business rules.

## Problem Context

Cycle stock orders are expected to meet tight dispatch SLAs. Misses introduce downstream impacts including expediting, customer dissatisfaction, and operational rework. The central questions addressed are whether SLA misses can be predicted early enough to matter, whether identical modeling approaches perform consistently across regions, and how any resulting risk scores should be used in practice.

## Analytical Approach

The analysis is intentionally constrained to creation-time features to reflect what planners actually know when decisions are made. Inputs include calendar timing, order size, move codes, warehouse identifiers, and leakage-safe historical SLA performance indicators. A Logistic Regression baseline is used to prioritize interpretability and operational relevance. Validation is time-based to prevent leakage, and model outputs are evaluated using probability thresholds rather than binary accuracy to reflect real-world capacity tradeoffs.

Raw data is anonymized and excluded from the repository by design. All notebooks expect pre-anonymized inputs placed locally.

## United States Findings

In the United States, SLA miss rates are low, generally in the range of 9–13 percent. Modeling results show weak predictive signal, with performance only marginally better than random and no threshold producing an operationally usable balance of precision and recall. Misses are largely exception-driven rather than systemic, limiting the value of creation-time prediction. In this context, analytics effort is better focused on exception management, root-cause analysis, and execution-stage monitoring rather than early prediction.

## Canada Findings

Canada presents a contrasting case. Historical SLA miss rates are materially higher, ranging from approximately 28–33 percent, and exhibit greater variability across time and operational categories. Between Q1 2023 and Q1 2025, Canada reduced SLA misses by 107 orders while processing higher volume, lowering the miss rate from 42.7 percent to 28.1 percent. This reflects genuine operational improvement rather than volume effects.

Modeling results show modest but real predictive signal. While creation-time features do not support deterministic prediction, risk scores provide meaningful ranking capability. Thresholds in the 0.30–0.40 range enable practical triage, allowing planners to prioritize a manageable subset of orders while capturing a significant share of SLA misses. As execution stabilized over time, predictive signal diminished, indicating that remaining misses are increasingly exception-driven.

## Cross-Region Comparison and Implications

Applying the same models and features across both regions demonstrates that predictive effectiveness is driven primarily by operational context rather than algorithm selection. Stable systems with low miss rates are harder to predict and benefit less from early-stage modeling. Less stable or improving systems exhibit patterns that can be exploited for prioritization and early intervention.

The key takeaway is that predictive analytics should be deployed selectively. Where execution variability is systemic, risk scoring can support disciplined triage. Where operations are stable and failures are isolated, analytics adds more value by diagnosing causes and strengthening execution than by predicting outcomes. This repository is intentionally framed as an operations analytics decision exercise, demonstrating judgment in where predictive modeling should and should not be applied.
