# Model Comparison

## Overview

Four regression models were built to explain monthly sales performance across 80 retail stores (306 observations after data cleaning). This document compares their explanatory power, significant variables, business usefulness, and limitations.

---

## Model Definitions

| Model Name | Dependent Variable | Independent Variable(s) |
|---|---|---|
| Simple Model 1 | monthly_sales | marketing_spend |
| Simple Model 2 | monthly_sales | footfall |
| Simple Model 3 | monthly_sales | customer_rating |
| Multiple Model | monthly_sales | marketing_spend, footfall, avg_discount_pct, inventory_availability_pct, store_Airport, store_HighStreet, store_Mall |

---

## Comparison Table

| Item | Simple Model 1 | Simple Model 2 | Simple Model 3 | Multiple Model |
|---|---|---|---|---|
| **Variables Used** | marketing_spend | footfall | customer_rating | 4 numerical + 3 dummies |
| **R-squared** | 0.157 | 0.735 | 0.001 | 0.816 |
| **Adjusted R-squared** | — | — | — | 0.812 |
| **F-statistic p-value** | < 0.001 | < 0.001 | 0.647 | < 0.001 |
| **Significant Variables (p < 0.05)** | marketing_spend | footfall | None | marketing_spend, footfall, inventory_availability_pct, store_Airport, store_HighStreet, store_Mall |
| **Intercept** | 567,463.56 | 447,699.03 | 703,414.65 | 138,186.46 |
| **Key Coefficient** | 2.05 per $ | 35.64 per visitor | −5,117.97 per rating point | See model equations |
| **Business Usefulness** | Low–Moderate | High | None | High |
| **Residual Std Error (approx)** | ~95,500 | ~53,600 | ~103,800 | ~44,160 |

---

## Detailed Model Assessment

### Simple Model 1 — marketing_spend

- **R-squared: 0.157** — marketing spend alone explains only 15.7% of the variation in sales.
- **Coefficient: 2.05** — every additional $1 in marketing spend is associated with $2.05 more in monthly sales.
- **P-value: < 0.001** — the relationship is statistically significant.
- **Business usefulness:** Moderate. The model confirms marketing investment has a positive association with sales, but it is a weak predictor on its own. Other factors are more important.
- **Limitation:** Ignores footfall, store type, inventory, and discount effects — all of which likely mediate how marketing translates to sales.

---

### Simple Model 2 — footfall

- **R-squared: 0.735** — footfall alone explains 73.5% of monthly sales variation. This is the strongest single predictor.
- **Coefficient: 35.64** — each additional customer visit per month is associated with $35.64 more in monthly sales.
- **P-value: < 0.001** — highly significant.
- **Business usefulness:** High. Footfall is a leading indicator — anything that drives more customers into stores (marketing, location, promotions) ultimately drives sales. Decisions about store location, opening hours, and events should prioritise footfall impact.
- **Limitation:** Does not distinguish between store types or regions. A high-footfall Airport store and a high-footfall Residential store may have very different conversion rates.

---

### Simple Model 3 — customer_rating

- **R-squared: 0.001** — customer rating explains essentially none of the monthly sales variation.
- **Coefficient: −5,117.97** — the direction is negative, which is counterintuitive (higher rating → lower sales), though this is entirely driven by noise.
- **P-value: 0.647** — not statistically significant. We cannot reject the null hypothesis that there is no relationship.
- **Business usefulness:** None for predicting sales in this dataset. Customer rating may matter for long-term retention but does not appear to drive short-term monthly sales.
- **Limitation:** Rating may be a lagging indicator — its effect on sales could take multiple months to appear and is not captured in this 4-month window.

---

### Multiple Regression Model (Final Model)

- **R-squared: 0.816** — the model explains 81.6% of monthly sales variation. This is a strong model.
- **Adjusted R-squared: 0.812** — accounting for the number of predictors, the model remains highly explanatory.
- **Significant variables:**
  - `footfall` (p < 0.001) — dominant driver
  - `marketing_spend` (p < 0.001) — significant positive effect
  - `inventory_availability_pct` (p < 0.001) — significant positive effect
  - `store_Airport` (p < 0.001) — Airport stores outperform Residential by ~$36,186
  - `store_Mall` (p < 0.001) — Mall stores outperform Residential by ~$25,653
  - `store_HighStreet` (p = 0.023) — High Street stores outperform Residential by ~$14,367
- **Borderline/weak variable:**
  - `avg_discount_pct` (p = 0.159) — not statistically significant; coefficient is negative (−53,521), suggesting higher discounts do not reliably boost sales
- **Business usefulness:** High. The model can be used to identify which levers — footfall, marketing, inventory — leadership should prioritise, and which store types may need differentiated strategies.
- **Limitation:** The condition number (1.11e+06) suggests potential multicollinearity. Some variables may share predictive information (e.g., marketing spend and footfall are likely correlated). Only 4 months of data — seasonal patterns cannot be captured. Missing data rows (14 of 320) were excluded.

---

## Summary Recommendation

**Use the Multiple Regression Model as the final model.** It explains 81.6% of monthly sales variation — substantially more than any simple model — and provides actionable insights across multiple business levers simultaneously. Simple Model 2 (footfall) is a useful quick diagnostic but lacks the granularity to drive strategy.
