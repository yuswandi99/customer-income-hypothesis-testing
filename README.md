# Customer Income & Spending — Hypothesis Testing

Statistical analysis of 2,240 marketing-campaign customers. The tests check whether **education** and **marital status** create significant differences in income, and whether **income is related to total spending**. The goal is to find useful variables for customer segmentation.

## Hypotheses
| # | H0 | H1 | Test |
|---|----|----|------|
| 1 | No income difference across education levels | There is a significant difference | Kruskal-Wallis + Dunn post-hoc (Bonferroni) |
| 2 | No income difference across marital status | There is a significant difference | Kruskal-Wallis |
| 3 | No relationship between income and total spent | There is a relationship | Spearman rank correlation |

**Why non-parametric tests?** Income and spending are right-skewed and contain outliers, so the normality assumption is not met.

## Dataset
- **Marketing Campaign / Customer Personality Analysis** (public dataset): 2,240 rows × 29 columns
- Demographics, income, product spending (wine, meat, fruit, fish, sweets, gold), purchase channels, and campaign response

## Tools
Python · Pandas · NumPy · SciPy · scikit-posthocs · Matplotlib · Seaborn

## Workflow
1. **Descriptive statistics and EDA**: distributions, boxplots, and group statistics (mean, median, std)
2. **Data cleaning**
   - Filled 24 missing `Income` values with the **median**, because income has outliers
   - Merged invalid marital categories (`Alone`, `Absurd`, `YOLO`) into `Single`
   - Created a `total_spent` feature by summing the 6 product categories
3. **Hypothesis testing** at α = 0.05

## Results
| Test | Statistic | p-value | Decision |
|------|-----------|---------|----------|
| Education → Income | H = 142.52 | < 0.001 | **Reject H0** |
| Marital Status → Income | H = 5.91 | 0.206 | Fail to reject H0 |
| Income ↔ Total Spent | ρ = 0.847 | < 0.001 | **Reject H0** (strong positive) |

**Dunn post-hoc** shows three income tiers by education:
- **Low:** Basic (significantly lower than every other group)
- **Middle:** 2n Cycle
- **High:** Graduation, Master, PhD (PhD is significantly higher than Graduation, p = 0.023)

## Conclusion
- Income has a **strong positive relationship** with spending (ρ = 0.85).
- Education level significantly affects income, so it **indirectly separates customers by spending potential**. Marital status does not.
- **Recommendation:** use education level as a segmentation variable to target high-spending customers with more personalized marketing.

## Repository Structure
```
customer-income-hypothesis-testing/
├── hypothesis_testing.ipynb   # full analysis (narrative in Bahasa Indonesia)
└── README.md
```

## How to Run
1. Open the notebook in Google Colab or Jupyter
2. Upload `marketing_campaign.csv` (tab-separated)
3. `pip install scikit-posthocs`, then run all cells

---
**Author:** Andi Yuswandi · [GitHub](https://github.com/yuswandi99)
