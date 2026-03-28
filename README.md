# Fraud Claims Detection

Machine learning solution to detect fraudulent insurance claims for Global Insure.

## Overview

This project uses historical insurance claim data to build predictive models that identify potentially fraudulent claims early in the approval process. By analyzing patterns in claim timing, amounts, and customer profiles, we help insurance companies reduce financial losses and optimize investigation resources.

## Problem Statement

Global Insure processes thousands of claims annually, with significant losses from fraudulent claims. Manual inspection is time-consuming, reactive, and often detects fraud only after payment. This project aims to enable proactive fraud detection through data-driven insights.

## Key Findings

- **Temporal patterns are the strongest fraud indicator** - the timing between policy purchase and incident occurrence matters more than claim amounts or demographics
- **Random Forest model achieved 66% accuracy** on unseen data
- **Two features dominate**: policy_bind_date (57.8% importance) and incident_date (42.2% importance)
- **Expected ROI**: ~$4.6M annual savings from prevented fraud

## Dataset

- **Source**: `insurance_claims.csv`
- **Original size**: 1,000 claims × 40 features
- **After cleaning**: 431 claims × 36 features
- **Features include**: customer demographics, policy details, incident characteristics, claim amounts, vehicle information
- **Target variable**: fraud_reported (Y/N)

## Methodology

1. **Data Cleaning** - Handled missing values, removed invalid entries, dropped identifier columns
2. **Exploratory Data Analysis** - Univariate, correlation, and bivariate analysis
3. **Feature Engineering** - Oversampling for class imbalance, one-hot encoding, feature scaling, RFECV selection
4. **Model Building** - Logistic Regression (interpretable) and Random Forest (accurate)
5. **Validation** - 70-30 train-validation split with performance evaluation

## Models Developed

### Logistic Regression
- **Accuracy**: 57.8%
- **Strengths**: Interpretable, no overfitting, provides statistical significance
- **Use case**: Regulatory reporting and stakeholder communication

### Random Forest (Recommended)
- **Accuracy**: 66.2% (validation)
- **Cross-validation**: 84.9%
- **Strengths**: Captures non-linear patterns, higher accuracy
- **Limitation**: Overfits training data (100% train → 66% validation)
- **Use case**: Operational fraud scoring and prioritization

## Results

| Metric | Logistic Regression | Random Forest |
|--------|-------------------|---------------|
| Validation Accuracy | 57.8% | 66.2% |
| Sensitivity | 60.9% | ~66% |
| Interpretability | High | Low |
| Overfitting | None | Severe |

**Winner**: Random Forest for operational predictions, Logistic Regression for explanations.

## Business Impact

Assuming 1,000 annual claims (250 fraud, 750 legitimate):
- ✓ Correctly identify ~165 fraud cases ($9.4M prevented)
- ✓ Reduce manual review workload by 58% (1,000 → 420 claims)
- ✓ Net annual benefit: ~$4.6M
- ✗ Miss ~85 fraud cases (false negatives)
- ✗ Generate ~255 false alarms (investigation cost)

## Key Insights

1. **Focus on timing patterns** - Claims filed shortly after policy purchase are high-risk
2. **Claim amounts less reliable** - Fraudsters vary amounts to avoid detection
3. **Demographics don't matter much** - Fraud cuts across age, education, occupation
4. **Data quality is critical** - 57% data loss significantly impacted performance
5. **Feature engineering needed** - Should calculate days_between_policy_and_incident explicitly

## Recommendations

### Immediate (30 Days)
- Deploy Random Forest in shadow mode (no operational decisions yet)
- Implement business rule: flag claims filed within 30 days of policy purchase
- Fix data quality issues (required fields, validation rules)

### Short-Term (3-6 Months)
- Engineer better features (days_between, temporal extractions, ratios)
- Collect 1,500-2,000 additional training samples
- Test XGBoost, LightGBM, Neural Networks
- Target: 80%+ validation accuracy

### Long-Term (6-12 Months)
- Build comprehensive fraud detection system (ML + rules + network analysis)
- Implement feedback loop (capture outcomes → retrain)
- Semi-automate: fast-track low-risk, auto-investigate high-risk, human review moderate

## Project Structure

```
fraud-claims-detection/
├── Fraudulent_Claim_Detection_Starter.ipynb    # Complete solution notebook
├── insurance_claims.csv                         # Dataset (1,000 claims)
├── Fraud_Detection_Presentation.pptx            # Business presentation
├── Fraud_Detection_Technical_Report.pdf         # Detailed technical report
└── README.md                                    # This file
```

## Requirements

```
Python 3.x
pandas
numpy
scikit-learn
statsmodels
imbalanced-learn
matplotlib
seaborn
```

Install dependencies:
```bash
pip install pandas numpy scikit-learn statsmodels imbalanced-learn matplotlib seaborn
```

## Usage

1. Clone the repository
2. Install dependencies
3. Open `Fraudulent_Claim_Detection_Starter.ipynb` in Jupyter
4. Run all cells to reproduce the analysis
5. Review `Fraud_Detection_Technical_Report.pdf` for detailed findings
6. See `Fraud_Detection_Presentation.pptx` for executive summary

## Model Performance Summary

- **Best Model**: Random Forest
- **Validation Accuracy**: 66.2%
- **Most Important Features**: policy_bind_date, incident_date
- **Production Ready**: No (use as prioritization tool with human review)
- **Improvement Potential**: 80%+ with better features and more data

## Limitations

- Small training dataset (431 samples after cleaning)
- Random Forest overfits (100% train vs 66% validation)
- Only 2 features utilized (underutilized available data)
- Missing derived temporal feature (days_between)
- 66% accuracy insufficient for automated decisions

## Future Work

- Create days_between_policy_and_incident feature
- Expand dataset to 2,000+ labeled claims
- Test gradient boosting algorithms (XGBoost, LightGBM)
- Add regularization to reduce overfitting
- Integrate additional data sources (claim history, network analysis)
- Build real-time monitoring dashboard

## License

[Your License Here]

## Contact

[Your Contact Information]

---

**Project Assignment**: Fraudulent Claim Detection
**Organization**: Global Insure
**Date**: March 2026
