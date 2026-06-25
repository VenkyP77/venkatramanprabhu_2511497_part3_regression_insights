# Part 3: Regression Insights — Retail Chain Sales Analysis

## Business Problem Summary

The leadership team of a retail chain wants to understand what factors drive monthly sales performance across stores. They are considering actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritising certain store types or regions. This project uses regression analysis to identify which factors are most strongly associated with monthly sales and provides a data-backed business recommendation.

---

## Dataset Description

**File:** `data/business_regression_data.xlsx`

| Column | Type | Description |
|---|---|---|
| store_id | Categorical (ID) | Unique store identifier — not used in regression |
| month | Date | Month of observation (Jan–Apr 2025) — not used directly |
| region | Categorical | Store region: East, North, South, West |
| store_type | Categorical | Store format: Residential, High Street, Airport, Mall |
| marketing_spend | Numerical | Monthly marketing expenditure ($) |
| footfall | Numerical | Number of customer visits in the month |
| avg_discount_pct | Numerical | Average discount offered as a proportion (e.g. 0.12 = 12%) |
| staff_count | Numerical | Number of staff members |
| inventory_availability_pct | Numerical | % of time inventory was available |
| competitor_distance_km | Numerical | Distance to nearest competitor (km) |
| holiday_flag | Binary (0/1) | Whether a public holiday occurred in that month |
| customer_rating | Numerical | Average customer satisfaction rating (1–5) |
| **monthly_sales** | **Numerical** | **Dependent variable — total monthly sales ($)** |
| monthly_profit | Numerical | Monthly profit — excluded to avoid confounding |

**Dataset size:** 320 rows, 14 columns (306 rows used after removing rows with missing values in key variables)

**Missing values:**
- `competitor_distance_km`: 6 missing values
- `customer_rating`: 8 missing values

---

## Dependent and Independent Variables

**Dependent Variable:** `monthly_sales`

**Independent Variables used in regression:**
- Numerical: `marketing_spend`, `footfall`, `avg_discount_pct`, `inventory_availability_pct`
- Categorical (converted to dummies): `store_type`

**Variables excluded from regression:**
- `store_id` — identifier, no predictive value
- `month` — only 4 time points, insufficient for time-series analysis
- `monthly_profit` — downstream of sales; including it would cause circular reasoning
- `customer_rating` — simple regression showed R² = 0.0007, p = 0.647 (not significant)
- `staff_count`, `holiday_flag`, `competitor_distance_km` — retained in workbook but not in final model to keep the model parsimonious

---

## Regression Approach

Three simple regression models were run first (one predictor each), followed by one multiple regression model combining numerical and dummy variables. All models use `monthly_sales` as the dependent variable.

**Models:**
1. Simple Model 1: `monthly_sales ~ marketing_spend`
2. Simple Model 2: `monthly_sales ~ footfall`
3. Simple Model 3: `monthly_sales ~ customer_rating`
4. Multiple Regression Model: `monthly_sales ~ marketing_spend + footfall + avg_discount_pct + inventory_availability_pct + store_Airport + store_HighStreet + store_Mall`

---

## Dummy Variable Approach

The categorical variable **`store_type`** was converted into dummy variables:

| Dummy Variable | Value 1 Meaning |
|---|---|
| store_Airport | Store is an Airport-type store |
| store_HighStreet | Store is a High Street-type store |
| store_Mall | Store is a Mall-type store |

**Reference category: Residential** (dropped to avoid the dummy variable trap). All coefficients for store type dummies are interpreted relative to a Residential store with the same other characteristics.

See `outputs/model_equations.md` for full explanation.

---

## Model Comparison Summary

| Model | Variables | R-squared | Key Significant Predictors |
|---|---|---|---|
| Simple 1 | marketing_spend | 0.157 | marketing_spend (p < 0.001) |
| Simple 2 | footfall | 0.735 | footfall (p < 0.001) |
| Simple 3 | customer_rating | 0.001 | None (p = 0.647) |
| Multiple | 4 numerical + 3 dummies | 0.816 | footfall, marketing_spend, inventory_availability_pct, store dummies |

---

## Final Model Selected

**Multiple Regression Model** — explains 81.6% of the variation in monthly sales (R² = 0.816). All key predictors are statistically significant (p < 0.05) except `avg_discount_pct`, which is retained for business context.

---

## Business Recommendation

1. **Footfall is the single most powerful driver** — every additional 1,000 customers adds approximately $35,600 in monthly sales.
2. **Marketing spend has a significant positive effect** — every additional $1,000 in marketing spend adds approximately $1,162 in monthly sales (5.4× return at the margin when scaled).
3. **Inventory availability matters** — a 1% improvement in availability adds about $2,824 in monthly sales; consistent stock should be a priority.
4. **Airport and Mall stores outperform Residential** by ~$36,000 and ~$25,600 per month respectively, even after controlling for footfall and marketing spend.
5. **Discounting does not significantly boost sales** — the coefficient for `avg_discount_pct` is negative and not statistically significant (p = 0.16), suggesting indiscriminate discounting should be reviewed.

---

## Assumptions and Limitations

- Regression shows association, not causation. Increasing marketing spend does not guarantee proportional sales growth — other unmeasured factors may be at play.
- Only 4 months of data (Jan–Apr 2025). Seasonal effects and longer trends are not captured.
- `monthly_profit` was excluded to avoid post-treatment bias; the model targets sales volume only.
- Multicollinearity warning (condition number 1.11e+06) suggests some predictors may be correlated.
- Stores with missing data (14 rows) were excluded — results may not fully represent those stores.

---

## Screenshots Included

| File | Description |
|---|---|
| `screenshots/simple_regression_output.png` | Output for simple regression: footfall vs monthly_sales |
| `screenshots/multiple_regression_output.png` | Full multiple regression output table |
| `screenshots/residuals_preview.png` | Residual analysis — actual vs predicted vs residual |
| `screenshots/model_comparison_preview.png` | Model comparison table showing R², variables, and significance |
