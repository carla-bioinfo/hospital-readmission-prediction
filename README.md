# 🏥 Hospital Readmission Risk Prediction & Analytics

**Project Status:** OPÇÃO A Complete ✅ | OPÇÃO B Ready ⏳  
**Author:** Carla Rodrigues (@carla-bioinfo)  
**Date:** 2026-06-21  
**GitHub:** [carla-bioinfo/hospital-readmission-prediction](https://github.com/carla-bioinfo/hospital-readmission-prediction)

---

## 🎯 Project Overview

A comprehensive **machine learning and data science project** to predict 30-day hospital readmission risk using clinical and demographic features. This project demonstrates advanced feature importance analysis, model optimization, and production-ready ML pipeline development.

**Key Application:** Healthcare data science | Readmission prediction | Risk stratification

---

## 📊 Dataset

- **Size:** 10,000 synthetic patients
- **Features:** 21 (clinical + demographic)
- **Target:** Binary (readmitted in 30 days: Yes/No)
- **Class Distribution:** 53.6% (no readmission) vs 46.4% (readmission)
- **Train/Test Split:** 70/30 (stratified)

### Features (Clinical Relevance)

| Category | Features |
|----------|----------|
| **Demographic** | age, gender |
| **Hospitalization** | los_days (length of stay), admission_type, discharge_type |
| **Comorbidities** | comorbidities, diabetes, hypertension, heart_disease, copd, kidney_disease |
| **Lab Values** | hemoglobin_g_dl, creatinine_mg_dl, sodium_mmol_l |
| **Vitals** | systolic_bp, diastolic_bp, heart_rate, bmi |
| **Temporal** | admission_month, admission_day_of_week, admission_quarter |

---

## 🚀 Project Status

### ✅ OPÇÃO A: Feature Importance Analysis (COMPLETE)

**Deliverables:**
- ✅ 3 complementary feature importance methods
  - Logistic Regression coefficients (linear effects)
  - Random Forest feature importance (non-linear effects)
  - Feature interaction analysis (synergistic/antagonistic effects)
- ✅ 3 professional visualizations (300 DPI, 844 KB)
- ✅ Comprehensive report (434 lines, 33 sections)
- ✅ Validation checklist (7 phases)
- ✅ GitHub commits (2x)

**Key Findings:**
1. **Top Risk Factors (Linear - LR):**
   - heart_disease: +0.2243 (strongest)
   - diabetes: +0.2029
   - comorbidities: +0.1571
   
2. **Top Non-Linear Features (RF):**
   - creatinine_mg_dl: 10.0% importance
   - systolic_bp: 8.5% importance
   - heart_rate: 8.4% importance

3. **Model Performance (with class weights):**
   - Sensitivity: 52.59% (improved from 39.22%)
   - Specificity: 59.20%
   - ROC-AUC: 0.5877 (weak, optimization needed)

4. **Critical Insight:**
   - LR and RF **partially disagree** on feature importance
   - Suggests both **linear AND non-linear effects** are important
   - All feature interactions show **antagonistic effects** (floor effect hypothesis)

---

### ⏳ OPÇÃO B: Hyperparameter Tuning (READY)

**Objective:** Optimize model parameters to improve ROC-AUC and sensitivity

**Planned Approach:**
1. GridSearchCV on Logistic Regression (C, penalty)
2. GridSearchCV on Random Forest (max_depth, n_estimators, min_samples_split)
3. Threshold optimization (sensitivity vs specificity trade-off)
4. 5-fold cross-validation for stability

**Target Performance:**
- Sensitivity: 65%+ (medical priority: catch readmissions)
- Specificity: 55%+ (acceptable trade-off)
- ROC-AUC: 0.60+

**Estimated Time:** 40-50 minutes

---

### ⏳ OPÇÃO C: Production Pipeline (PLANNED)

**Objective:** Create reproducible, deployable ML pipeline

**Components:**
1. Model serialization (pickle)
2. Preprocessing pipeline (scaler + encoders)
3. Prediction API (predict readmission risk)
4. Documentation & handoff

---

## 📁 Project Structure
hospital-readmission-prediction/

├── data/

│   ├── raw/

│   │   └── hospital_patients_raw.csv (10K patients, 21 features)

│   └── processed/

│       ├── X_train_scaled.csv, X_test_scaled.csv

│       ├── y_train.csv, y_test.csv

│       ├── feature_importance_coefficients.csv

│       ├── feature_importance_rf.csv

│       ├── feature_interactions.csv

│       └── encoding_mapping.json

├── models/

│   ├── logistic_regression_weighted.pkl

│   ├── random_forest_importance.pkl

│   └── scaler.pkl

├── figures/

│   ├── 01_feature_importance_comparison.png

│   ├── 02_pareto_importance.png

│   └── 03_correlation_with_target.png

├── docs/

│   ├── HANDOFF.md (minimal context for next session)

│   ├── RESUMO_SESSÃO.md (complete session summary)

│   ├── OPÇÃO_A_FEATURE_IMPORTANCE_REPORT.md (434 lines)

│   ├── OPÇÃO_A_VALIDATION_CHECKLIST.md

│   └── README.md (this file)

├── venv/ (Python 3.9.2, all dependencies)

└── .gitignor
---

## 🔍 Key Analyses & Visualizations

### Analysis 1: Feature Importance Comparison
**File:** `figures/01_feature_importance_comparison.png`

Side-by-side comparison of:
- **Left:** Logistic Regression coefficients (top 10)
- **Right:** Random Forest importance (top 10)

Shows **discordance** between linear and non-linear models.

### Analysis 2: Pareto Analysis
**File:** `figures/02_pareto_importance.png`

Cumulative importance curve with 80% threshold:
- **Finding:** Top 10 features explain 76.1% of model's decisions
- **Implication:** Dimensionality reduction possible

### Analysis 3: Feature-Target Correlation
**File:** `figures/03_correlation_with_target.png`

Heatmap of Pearson correlations:
- **Positive:** Risk factors (red bars)
- **Negative:** Protective factors (green bars)
- **Note:** Weak correlations (max 0.11) explain model difficulty

---

## 📊 Detailed Results

### Clinical Interpretation

**🔴 Risk Factors (Increase Readmission)**

| Feature | Mechanism | Clinical Action |
|---------|-----------|-----------------|
| **heart_disease** | Post-discharge decompensation, arrhythmias | 48h follow-up, home monitoring |
| **diabetes** | Glycemic dyscontrol, infection risk | Aggressive insulin titration, home glucose monitoring |
| **comorbidities** | Reduced physiologic reserve | Integrated care team (physician, pharmacist, social work) |
| **creatinine_mg_dl** | Impaired drug clearance | Medication review (renally adjusted doses) |
| **age** | Physiologic aging, fragilization | Geriatric assessment (age >75) |

**🟢 Protective Factors (Decrease Readmission)**

| Feature | Mechanism | Note |
|---------|-----------|------|
| **Planned admission** | Better baseline optimization | Elective > emergency |
| **systolic_bp** | ⚠️ PARADOXICAL | Requires validation on real data |
| **Seasonality** | Possible seasonal patterns | Weak effect, needs investigation |

### Feature Interactions (Surprising Finding)

**All 28 analyzed feature pairs show ANTAGONISTIC effects:**
- heart_disease × diabetes: synergy = -0.0992
- creatinine × heart_disease: synergy = -0.0820
- diabetes × age: synergy = -0.0759

**Interpretation:**
- Expected: Synergistic (2 diseases = worse than 1)
- Found: Antagonistic (combined effect smaller than sum)
- **Hypothesis:** Floor effect (already at max risk)
- **Caveat:** May be dataset artifact, requires real data validation

---

## 🔧 Technical Implementation

### Data Processing Pipeline

```python
# 1. Feature Engineering
- Temporal extraction: month, day_of_week, quarter
- Categorical encoding: LabelEncoder for gender, admission_type, discharge_type
- Normalization: StandardScaler (mean=0, std=1)

# 2. Train/Test Split
- 70/30 split with stratification
- Maintains class distribution in both sets
- Prevents data leakage (fit on train, transform on test)

# 3. Class Weighting
- readmission class weighted 1.08x
- Compensates for imbalanced data
- Improves sensitivity at cost of specificity
```

### Models Trained

1. **Logistic Regression (Best for OPÇÃO A)**
   - Class weights: balanced
   - Regularization: L2 (default)
   - Interpretation: Direct coefficients

2. **Random Forest (Non-linear comparison)**
   - Trees: 100
   - Max depth: 10
   - Feature importance: Gini-based

3. **Gradient Boosting (Baseline)**
   - Estimators: 100
   - Learning rate: 0.1

---

## 💡 Key Insights & Learnings

### 1. Linear vs Non-Linear Effects
- **LR emphasizes:** heart_disease, diabetes, comorbidities
- **RF emphasizes:** creatinine, systolic_bp, lab values
- **Meaning:** Different aspects of readmission risk captured

### 2. Class Imbalance Solution
- Without class weights: 39.2% sensitivity (misses 60% of readmissions!)
- With class weights: 52.6% sensitivity (still misses 47%)
- **Trade-off:** Lost 12.7% specificity to gain 13.4% sensitivity
- **Clinical judgment:** Acceptable in healthcare (false alarms < missed risks)

### 3. Feature Correlations are Weak
- Strongest univariate: heart_disease (r=0.109)
- Most features: r < 0.11
- **Implication:** Readmission is complex, multivariate phenomenon
- **Challenge:** Low predictive power with current features

### 4. Pareto Principle Applies
- Top 5 features: 49.3% importance
- Top 10 features: 76.1% importance
- Top 15 features: 93.5% importance
- **Opportunity:** Can reduce model complexity without major loss

---

## ⚠️ Limitations & Caveats

### Data Limitations
- ❌ Synthetic dataset (generated with known patterns)
- ❌ Missing unmeasured variables (social determinants, medication adherence)
- ❌ No temporal dynamics (time-to-readmission patterns)
- ✅ Balanced classes (unlike real hospital data)

### Methodological Limitations
- ❌ Logistic Regression assumes linearity (not capturing interactions)
- ❌ Random Forest biased toward high-cardinality features
- ❌ Feature interactions may be dataset artifact
- ❌ Multicollinearity NOT tested (VIF not calculated)
- ❌ All findings REQUIRE validation on real hospital data

### Model Performance Limitations
- ❌ ROC-AUC 0.5877 (barely better than random!)
- ❌ Sensitivity 52.6% (still misses ~47% of readmissions)
- ❌ Features insufficient for high-confidence predictions
- ✅ Class weights improved sensitivity significantly

---

## 📚 Methodology & Standards

### Machine Learning Best Practices
- ✅ Stratified train/test split (maintains class distribution)
- ✅ Feature scaling before linear models
- ✅ Class weights for imbalanced classification
- ✅ Explicit data leakage prevention
- ✅ Multiple validation approaches (LR + RF agreement)

### Tools & Libraries
Python 3.9.2

pandas: Data manipulation
numpy: Numerical computation
scikit-learn: ML models & preprocessing
matplotlib/seaborn: Visualizations
joblib: Model serialization
### Clinical Standards Referenced
- LACE Index: Predicts 30-day readmission
- Charlson Comorbidity Index: Standardized measurement
- CMS Readmission Reduction Program: Clinical focus areas

---

## 🚀 How to Use This Project

### 1. Setup Environment
```bash
cd /home/bioinfo/hospital-readmission-prediction
source venv/bin/activate
```

### 2. Load Pre-processed Data
```python
import pandas as pd
X_train = pd.read_csv('data/processed/X_train_scaled.csv')
X_test = pd.read_csv('data/processed/X_test_scaled.csv')
y_train = pd.read_csv('data/processed/y_train.csv', header=None).values.ravel()
y_test = pd.read_csv('data/processed/y_test.csv', header=None).values.ravel()
```

### 3. Load Pre-trained Model
```python
import joblib
lr_model = joblib.load('models/logistic_regression_weighted.pkl')
scaler = joblib.load('models/scaler.pkl')

# Make predictions
y_pred = lr_model.predict(X_test)
y_pred_proba = lr_model.predict_proba(X_test)[:, 1]
```

### 4. View Results
figures/

├─ 01_feature_importance_comparison.png

├─ 02_pareto_importance.png

└─ 03_correlation_with_target.png
docs/

├─ OPÇÃO_A_FEATURE_IMPORTANCE_REPORT.md (detailed findings)

└─ HANDOFF.md (next session context)
---

## 📈 Next Steps (OPÇÃO B & C)

### OPÇÃO B: Hyperparameter Tuning
1. **GridSearchCV** on Logistic Regression parameters
2. **GridSearchCV** on Random Forest parameters
3. **Threshold optimization** for medical use case
4. **Cross-validation** (5-fold) for model stability

**Goal:** Achieve Sensitivity 65%+, ROC-AUC 0.60+

### OPÇÃO C: Production Pipeline
1. Model serialization & API
2. Preprocessing pipeline encapsulation
3. Prediction function for new patients
4. Documentation & deployment guide

### Future Improvements
- Real hospital data validation
- Advanced feature engineering (polynomial, interaction terms)
- Ensemble methods (stacking, voting)
- Temporal analysis (time-to-readmission patterns)
- External validation on different populations

---

## 🎓 Teaching Methodology

This project follows **MÉTODO_DE_ENSINO_ESTRUTURADO** (Structured Teaching Method):

- ✅ Max 3 commands per round (cognitive load management)
- ✅ Clear O QUÊ / POR QUÊ / COMO explanations
- ✅ Validation checklist before advancing
- ✅ Reproducible workflows with full documentation
- ✅ Git-based version control for continuity

**Result:** Professional-grade data science work with deep understanding.

---

## 👩‍💻 Author

**Carla Rodrigues**
- GitHub: [@carla-bioinfo](https://github.com/carla-bioinfo)
- Focus: Lynch Syndrome, MMR genes, Bioinformatics + Data Science
- Portfolio: Healthcare data science, Machine learning, Genomics

---

## 📄 Documentation Files

| File | Purpose | Status |
|------|---------|--------|
| `docs/HANDOFF.md` | Minimal context for next session | ✅ Ready |
| `docs/RESUMO_SESSÃO.md` | Complete session summary | ✅ Complete |
| `docs/OPÇÃO_A_FEATURE_IMPORTANCE_REPORT.md` | Detailed findings (434 lines) | ✅ Complete |
| `docs/OPÇÃO_A_VALIDATION_CHECKLIST.md` | Validation (7 phases) | ✅ Complete |

---

## 🔗 Links & References

- **GitHub Repository:** https://github.com/carla-bioinfo/hospital-readmission-prediction
- **Project Timeline:** OPÇÃO A (Complete) → OPÇÃO B (Next) → OPÇÃO C (Final)
- **Session Summary:** `docs/RESUMO_SESSÃO.md`
- **Handoff Context:** `docs/HANDOFF.md`

---

## ✅ Project Status Summary

| Component | Status | Details |
|-----------|--------|---------|
| Data Processing | ✅ Complete | 10K patients, 21 features, 70/30 split |
| EDA | ✅ Complete | 0 missing values, balanced classes |
| Feature Engineering | ✅ Complete | Temporal, categorical, normalization |
| Model Training | ✅ Complete | LR, RF, GB trained with class weights |
| Feature Importance | ✅ Complete | 3 methods, 3 visualizations |
| Documentation | ✅ Complete | 434-line report + checklists |
| GitHub | ✅ Complete | 2 commits, pushed to main |
| Hyperparameter Tuning | ⏳ Ready | GridSearchCV prepared, OPÇÃO B next |
| Production Pipeline | ⏳ Planned | OPÇÃO C after OPÇÃO B |

---

**Last Updated:** 2026-06-21  
**Status:** OPÇÃO A Complete ✅ | OPÇÃO B Ready ⏳ | OPÇÃO C Planned ⏳

---

*This README reflects the current state of the project. All findings are based on synthetic data and require validation on real hospital data before clinical deployment.*
