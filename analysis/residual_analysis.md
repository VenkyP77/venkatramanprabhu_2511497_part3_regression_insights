# Residual Analysis

## Final Model Used

**Multiple Regression Model:**
`monthly_sales = 138,186 + 1.162 × marketing_spend + 33.605 × footfall − 53,521 × avg_discount_pct + 2,824 × inventory_availability_pct + 36,186 × store_Airport + 14,367 × store_HighStreet + 25,653 × store_Mall`

**Sample size:** 306 observations (after removing rows with missing values)

---

## Predicted Values and Residual Summary

Predicted sales were calculated using the multiple regression model. Residuals are defined as:

`Residual = Actual Monthly Sales − Predicted Monthly Sales`

| Metric | Value |
|---|---|
| Mean Residual | $0.00 (expected — OLS property) |
| Std Deviation of Residuals | $44,160 |
| Minimum Residual | −$157,039 |
| Maximum Residual | +$102,834 |

The residual standard error of ~$44,160 means the model's predictions are typically within ±$44,000 of actual sales — reasonable for sales figures ranging from ~$400,000 to ~$950,000.

---

## Top 5 Records — Largest Positive Residuals (Under-Predictions)

These are stores where **actual sales significantly exceeded what the model predicted** — the model under-estimated their performance.

| # | Store ID | Month | Region | Store Type | Actual Sales ($) | Predicted Sales ($) | Residual ($) |
|---|---|---|---|---|---|---|---|
| 1 | STR-1030 | 2025-02 | West | Residential | 820,519 | 717,685 | +102,834 |
| 2 | STR-1032 | 2025-01 | South | High Street | 914,544 | 815,637 | +98,907 |
| 3 | STR-1073 | 2025-03 | East | Residential | 813,317 | 716,285 | +97,031 |
| 4 | STR-1028 | 2025-04 | East | Mall | 713,611 | 617,602 | +96,010 |
| 5 | STR-1050 | 2025-04 | North | Residential | 735,787 | 640,921 | +94,866 |

**Business interpretation of positive residuals:**
- These stores performed materially better than expected given their footfall, marketing spend, and store type.
- Possible unmeasured factors: superior store management, local events, unique product mix, loyal customer base, or particularly effective staff.
- STR-1030 and STR-1073 are both Residential stores — this suggests that some Residential stores may have characteristics (e.g., catchment area demographics, local competition dynamics) that allow them to outperform the average Residential store significantly.
- STR-1032 (High Street, South) achieved over $914,000 in sales, which is close to the dataset maximum — this store may warrant further investigation as a best-practice case.

---

## Top 5 Records — Largest Negative Residuals (Over-Predictions)

These are stores where **actual sales were significantly below what the model predicted** — the model over-estimated their performance.

| # | Store ID | Month | Region | Store Type | Actual Sales ($) | Predicted Sales ($) | Residual ($) |
|---|---|---|---|---|---|---|---|
| 1 | STR-1017 | 2025-03 | West | High Street | 685,379 | 842,418 | −157,039 |
| 2 | STR-1023 | 2025-02 | South | Mall | 627,172 | 754,729 | −127,557 |
| 3 | STR-1012 | 2025-01 | West | Residential | 595,468 | 718,262 | −122,794 |
| 4 | STR-1009 | 2025-01 | North | Residential | 641,865 | 743,674 | −101,809 |
| 5 | STR-1001 | 2025-04 | East | Residential | 658,920 | 758,994 | −100,074 |

**Business interpretation of negative residuals:**
- These stores performed well below model expectations despite having favourable footfall, marketing spend, and store type characteristics.
- Possible causes: local economic downturn, supply chain disruptions, poor store execution, high staff turnover, or nearby competitive entry not captured in the data.
- STR-1017 (High Street, West) has the single largest negative residual (−$157,039). The model expected ~$842,000 in sales but actual was only $685,000 — a gap of 18.6%. This store should be investigated for operational issues or local market challenges.
- Three of the five largest negative residuals are Residential stores, suggesting the model may slightly over-estimate average-quality Residential stores when their footfall numbers are inflated by external factors that do not convert to sales efficiently.

---

## Under-Prediction vs Over-Prediction by Store Type

| Store Type | Avg Residual ($) | Interpretation |
|---|---|---|
| Airport | Slightly positive | Model tends to marginally under-predict Airport stores |
| Mall | Mixed | Residuals spread across positive and negative |
| High Street | Mixed | One very large negative outlier (STR-1017) skews perception |
| Residential | Mixed | Both the largest positive and some large negative residuals come from this type |

**Overall:** The model does not show a systematic directional bias for any one store type. However, Residential stores have the highest residual variance — meaning the model is less precise for this type. This may be because Residential stores are more influenced by hyper-local factors (neighbourhood demographics, local events) that the current variables do not capture.

---

## Conclusion

The model's residuals are approximately normally distributed around zero (mean = $0.00), which is a good sign — there is no systematic directional bias. However, residuals as large as ±$100,000–$157,000 on sales of $600,000–$900,000 represent a ±15–20% error range in the worst cases. For strategic planning, the model provides reliable directional guidance, but individual store performance predictions should be used with caution.
