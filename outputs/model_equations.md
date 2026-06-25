# Model Equations

## Simple Regression Equations

### Model 1: Marketing Spend

**Equation:**
```
monthly_sales = 567,463.56 + 2.0519 × marketing_spend
```

| Term | Value | Interpretation |
|---|---|---|
| Intercept | 567,463.56 | Predicted sales when marketing spend = $0 (baseline) |
| marketing_spend coefficient | 2.0519 | Each additional $1 in marketing spend adds $2.05 in monthly sales |
| R-squared | 0.157 | Marketing spend alone explains 15.7% of sales variation |
| P-value | < 0.001 | Statistically significant |

**Business meaning:** A store that increases its marketing budget by $10,000 is expected to see approximately $20,500 more in monthly sales, all else being equal. However, this model explains only 15.7% of variation — many other factors matter.

---

### Model 2: Footfall

**Equation:**
```
monthly_sales = 447,699.03 + 35.6415 × footfall
```

| Term | Value | Interpretation |
|---|---|---|
| Intercept | 447,699.03 | Predicted sales when footfall = 0 (baseline — not meaningful in practice) |
| footfall coefficient | 35.64 | Each additional customer visit adds $35.64 in monthly sales |
| R-squared | 0.735 | Footfall alone explains 73.5% of sales variation |
| P-value | < 0.001 | Statistically significant |

**Business meaning:** This is the strongest single-variable predictor. Increasing footfall by 1,000 visitors per month is associated with approximately $35,640 more in monthly sales. Strategies to drive in-store traffic — events, promotions, digital marketing — are likely high-impact.

---

### Model 3: Customer Rating

**Equation:**
```
monthly_sales = 703,414.65 − 5,117.97 × customer_rating
```

| Term | Value | Interpretation |
|---|---|---|
| Intercept | 703,414.65 | Predicted sales when rating = 0 |
| customer_rating coefficient | −5,117.97 | Negative, but not meaningful — not significant |
| R-squared | 0.001 | Customer rating explains virtually none of sales variation |
| P-value | 0.647 | Not statistically significant |

**Business meaning:** Customer rating has no meaningful short-term relationship with monthly sales in this dataset. It should not be used as a sales predictor. The negative coefficient is noise, not a real effect.

---

## Multiple Regression Equation (Final Model)

**Equation:**
```
monthly_sales = 138,186.46
              + 1.1615 × marketing_spend
              + 33.6050 × footfall
              − 53,521.13 × avg_discount_pct
              + 2,824.42 × inventory_availability_pct
              + 36,186.24 × store_Airport
              + 14,366.81 × store_HighStreet
              + 25,653.02 × store_Mall
```

---

## Coefficient Explanations (Multiple Model)

| Variable | Coefficient | P-value | Significant? | Business Meaning |
|---|---|---|---|---|
| Intercept | 138,186.46 | 0.003 | Yes | Baseline sales for a Residential store with all other variables at zero |
| marketing_spend | +1.1615 | < 0.001 | Yes | Each additional $1 of marketing spend adds $1.16 in sales (after controlling for other factors) |
| footfall | +33.605 | < 0.001 | Yes | Each additional customer visit adds $33.61 in sales |
| avg_discount_pct | −53,521.13 | 0.159 | No | Higher discounts are associated with slightly lower sales, but the relationship is not statistically reliable |
| inventory_availability_pct | +2,824.42 | < 0.001 | Yes | A 1% improvement in stock availability adds ~$2,824 in sales — keeping shelves stocked matters |
| store_Airport | +36,186.24 | < 0.001 | Yes | Airport stores generate ~$36,186 more per month than a comparable Residential store |
| store_HighStreet | +14,366.81 | 0.023 | Yes | High Street stores generate ~$14,367 more per month than a comparable Residential store |
| store_Mall | +25,653.02 | < 0.001 | Yes | Mall stores generate ~$25,653 more per month than a comparable Residential store |

---

## Dummy Variable Approach

### Why Dummy Variables Are Needed

`store_type` is a categorical variable with 4 categories: **Residential**, **High Street**, **Airport**, and **Mall**. Regression models require numerical inputs. Each category is therefore converted to a binary (0/1) variable — a "dummy" — that indicates whether an observation belongs to that category.

### Categories and Reference Category

| Category | Dummy Variable Created | Included in Model? |
|---|---|---|
| Residential | store_Residential | **No — Reference Category** |
| High Street | store_HighStreet | Yes |
| Airport | store_Airport | Yes |
| Mall | store_Mall | Yes |

**Reference category: Residential.** This means all store type coefficients are interpreted as the difference in monthly sales compared to a Residential store, holding all other variables constant.

If all four dummies were included, the model would suffer from **perfect multicollinearity** (the dummy variable trap) — one dummy is always predictable from the other three. Dropping one (the reference) solves this.

### How to Interpret a Dummy Coefficient

> "A Mall store is expected to generate $25,653 more in monthly sales than a Residential store with the same footfall, marketing spend, and inventory availability."

This tells leadership that the physical store format itself carries value beyond what can be explained by traffic and spend.

---

## Final Model Selected

**Multiple Regression Model** — R² = 0.816, Adjusted R² = 0.812

**Reason for selection:**
1. Highest explanatory power — explains 81.6% of monthly sales variation vs 73.5% for the best simple model.
2. Captures multiple business levers simultaneously: traffic generation, marketing investment, stock management, and store format.
3. All variables except `avg_discount_pct` are statistically significant, giving leadership clear, reliable signals.
4. The model is parsimonious — it avoids overfitting by using only 7 predictors on 306 observations.
5. Residuals are approximately normally distributed around zero, satisfying a key regression assumption.
