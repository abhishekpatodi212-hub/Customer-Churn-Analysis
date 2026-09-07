# Customer Churn Analysis
**Stack:** SQL + Python + Power BI

## Overview
A telecom-style churn dataset (4,000 customers) analyzed two ways: SQL for
descriptive/diagnostic aggregation, and Python (scikit-learn) for a predictive
churn-risk model that scores every customer.

## Files
| File | Purpose |
|---|---|
| `customer_churn.csv` | Raw dataset (4,000 rows, 14 columns) |
| `churn_analysis.sql` | 10 SQL queries: churn rate, drivers (contract, tenure, support calls, payment method), revenue at risk, high-value at-risk customer list |
| `churn_prediction.py` | Python: feature engineering + Logistic Regression model, evaluation metrics, feature-importance & confusion-matrix charts, and a full churn-risk score export |
| `model_performance_metrics.csv` | Accuracy / precision / recall / F1 / ROC-AUC from the trained model |
| `churn_risk_scores.csv` | Every customer scored with a `ChurnRiskScore` (0–1) and `RiskSegment` (Low/Medium/High) — this is the file to feed into Power BI |
| `feature_importance.png`, `confusion_matrix.png` | Model diagnostic charts |
| `Customer_Churn_Dashboard.xlsx` | Excel dashboard: Raw Data (with risk scores), formula-driven Summary sheet, Charts sheet, and a "Model Insights" sheet embedding the Python model's charts |

## How to run the Python model
```bash
pip install pandas numpy scikit-learn matplotlib
python3 churn_prediction.py
```
This regenerates `churn_risk_scores.csv` and the two PNG charts from
`customer_churn.csv`.

## Model performance (this run)
See `model_performance_metrics.csv` — Logistic Regression with `class_weight="balanced"`,
evaluated on a 25% held-out test split. ROC-AUC and recall are the metrics that matter
most here, since the business cost of missing an at-risk customer usually outweighs the
cost of a false alarm.

## Power BI dashboard design
1. **Churn Overview** — KPI cards (churn rate, revenue at risk, high-risk count), churn rate by contract type/tenure bucket.
2. **Risk Scoring** — table of `churn_risk_scores.csv` filtered to `RiskSegment = "High"`, sorted by `MonthlyCharges` — this becomes the retention team's outreach list.
3. **Model Transparency** — feature importance bar chart (import `feature_importance.png` or rebuild from the coefficients) so stakeholders can see *why* the model flags someone.

Use `churn_risk_scores.csv` (not the raw file) as the Power BI source — it already
contains the model's predictions alongside the original fields.

## Key insights (from this synthetic dataset)
- Month-to-month contracts churn at a much higher rate than annual contracts — the single strongest signal.
- Customers with 3+ support calls in the last 6 months are meaningfully more likely to churn — a good early-warning trigger.
- Customers under 12 months tenure are the highest-risk cohort, suggesting the biggest opportunity is a better onboarding/early-engagement program.
# Customer-Churn-Analysis
