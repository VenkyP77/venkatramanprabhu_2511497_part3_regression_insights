# Final Business Recommendation

## Executive Summary

Based on regression analysis of 306 monthly store-level observations across 80 stores (January–April 2025), footfall is the single most powerful driver of monthly sales, followed by marketing spend and inventory availability. Store format also plays a significant role — Airport and Mall stores consistently outperform Residential stores by $25,000–$36,000 per month even after accounting for traffic and spend. Discounting does not appear to reliably increase sales.

---

## Which Factors Appear Most Strongly Associated with Monthly Sales?

### 1. Footfall (Customer Visits) — Strongest Driver

- **R-squared (alone): 0.735** — footfall explains 73.5% of monthly sales variation as a single variable.
- **Multiple model coefficient: +$33.61 per visitor**
- **Business implication:** Every 1,000 additional customers entering a store is associated with approximately $33,600 more in monthly sales.
- **This is the most controllable and impactful lever leadership has.**

### 2. Marketing Spend — Significant Positive Effect

- **Multiple model coefficient: +$1.16 per dollar spent**
- **P-value: < 0.001**
- **Business implication:** Marketing investment reliably translates to sales. A $50,000 increase in monthly marketing budget is associated with roughly $58,000 in additional sales — a positive return on spend, especially when footfall-generating marketing is prioritised.

### 3. Inventory Availability — Operationally Critical

- **Multiple model coefficient: +$2,824 per 1% improvement**
- **P-value: < 0.001**
- **Business implication:** Stores that keep shelves better stocked sell more. A store improving from 85% to 90% inventory availability would be expected to generate approximately $14,120 more in monthly sales — entirely from operational improvement, no extra spend required.

### 4. Store Type — Airport and Mall Stores Outperform

| Store Type | Premium Over Residential ($/month) | P-value |
|---|---|---|
| Airport | +$36,186 | < 0.001 |
| Mall | +$25,653 | < 0.001 |
| High Street | +$14,367 | 0.023 |
| Residential | Reference | — |

Airport and Mall stores generate materially more revenue than Residential stores, even after controlling for footfall, marketing, and inventory.

---

## Which Variables Should Leadership Focus On?

| Priority | Variable | Recommended Action |
|---|---|---|
| 1 | **Footfall** | Invest in footfall-driving initiatives: local events, improved signage, digital advertising targeting store catchment areas, extended opening hours |
| 2 | **Marketing Spend** | Maintain or increase marketing budgets for underperforming stores; track ROI using footfall and sales lift |
| 3 | **Inventory Availability** | Reduce stock-outs through better demand forecasting, supplier management, and safety stock policies. Target 92–95% availability across all stores |
| 4 | **Store Format Mix** | When evaluating new store locations or store conversions, prioritise Airport and Mall formats where feasible |

---

## Which Variables Should Not Be Over-Interpreted?

### Average Discount Percentage
- **P-value: 0.159** — not statistically significant.
- The coefficient is negative (−$53,521 per unit of avg_discount_pct), suggesting higher discounts do not reliably increase sales and may slightly reduce revenue.
- **Do not expand discounting programmes expecting a sales lift.** The data does not support this strategy. Leadership should audit existing discount programmes for profitability impact.

### Customer Rating
- **R-squared: 0.001, P-value: 0.647** — no meaningful relationship with monthly sales in this dataset.
- Customer satisfaction matters for long-term loyalty, but it should not be treated as a short-term sales lever. Do not expect improvements in ratings to translate to near-term revenue.

### Staff Count, Holiday Flag, Competitor Distance
- These variables were not included in the final model because initial analysis showed weaker or inconsistent associations. They may matter in specific sub-segments but should not drive company-wide strategy without further analysis.

---

## What Business Actions Would You Recommend?

1. **Launch footfall-first marketing campaigns.** Shift a portion of marketing budgets toward activities with direct footfall impact — local social media geo-targeting, in-mall activations, proximity marketing. Measure footfall before and after.

2. **Set an inventory availability floor of 92%.** Stores below this threshold are leaving measurable revenue on the table. Work with supply chain to reduce stock-outs, particularly for top-selling SKUs.

3. **Review the discounting strategy.** Current data suggests discounting is not driving incremental sales. Run a controlled experiment — reduce discounting in a subset of stores for one quarter and compare sales outcomes — before committing to deeper discounts company-wide.

4. **Investigate high-residual stores.** The five stores with the largest negative residuals (STR-1017, STR-1023, STR-1012, STR-1009, STR-1001) are under-performing significantly versus model expectations. Conduct store-level audits to identify operational issues. The five stores with the largest positive residuals are outperforming expectations — identify what they are doing differently and replicate it.

5. **Prioritise Airport and Mall locations for expansion.** If the retail chain is evaluating new store openings, the data supports a premium for Airport and Mall formats. Factor the estimated +$25,000–$36,000/month premium into site selection financial models.

---

## Risks and Limitations Leadership Should Keep in Mind

| Risk | Detail |
|---|---|
| Short time horizon | Only 4 months of data (Jan–Apr 2025). Seasonal peaks (summer, Christmas) are not captured. The model may not generalise to full-year performance. |
| Missing variables | Factors like store size (sq ft), local demographics, product mix, and regional economic conditions are not in the dataset but likely influence sales. |
| Multicollinearity | Marketing spend and footfall are likely correlated — more marketing drives more footfall. Separating their individual effects is difficult. The condition number (1.11e+06) flags this concern. |
| Residual error | The model's typical prediction error is ~$44,000 per store per month. For individual store decisions, this level of uncertainty matters. Use model outputs for portfolio-level strategy, not individual store targets. |
| Outliers | STR-1017 had a residual of −$157,000 — nearly 4× the average residual. A single operational issue, renovation, or data error at one store can significantly distort model outputs. |

---

## Why Regression Shows Association, Not Causation

Regression measures **correlation** — how variables move together in the data — not whether one variable **causes** another. For example:

- The model shows that higher footfall is associated with higher sales. But we cannot say that merely counting more customers causes more sales — the relationship may be driven by a third factor (e.g., the store is in a popular location that independently drives both foot traffic and purchasing intent).
- Similarly, marketing spend correlates with sales, but stores in stronger markets may spend more AND sell more for reasons unrelated to marketing effectiveness.
- A true causal test would require a **randomised controlled experiment** (e.g., randomly assign marketing budgets to stores and compare outcomes), which this observational dataset does not support.

**Practical guidance:** Use the regression findings to prioritise hypotheses and investment areas, but validate causal claims through controlled pilots before scaling.

---

## Confidence Level

The Multiple Regression Model (R² = 0.816, F-statistic p < 0.001) provides a strong and statistically reliable basis for the above recommendations. The findings on footfall, marketing spend, and inventory availability are consistent across simple and multiple models, increasing confidence in their importance.
