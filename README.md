## Methodology

### 1. Exploratory Data Analysis
**Insight EDA:**
- Electricity consumption follows bimodal daily pattern
- Fossil generation positively correlated with price
- Renewable generation suppresses price — merit order effect
- Solar panel degradation hypothesis identified

**Model EDA:**
- Statistical tests — Spearman correlation, ANOVA, VIF
- Missing value analysis — MNAR/MAR investigation
- Outlier detection using IQR method
- Multicollinearity check — max inter-feature correlation 0.67

### 2. Preprocessing
- Weather data aggregated from city to country level
- Lag features engineered — price_lag_24 and price_lag_168
- Time features extracted — hour, day of week, month, weekend flag
- One hot encoding for weather categories
- StandardScaler applied for Linear Regression only
- Train test split — 80/20, shuffle=False for temporal integrity

### 3. Models Compared
| Model | MAPE |
|-------|------|
| Linear Regression | 7.81% |
| XGBoost Default | 8.15% |
| XGBoost Tuned | 7.18% |
| **Random Forest** | **7.18%** |

## Key Findings
- Price lag features are strongest predictors — confirming 
  strong price autocorrelation in electricity markets
- Fossil gas generation is most important generation feature — 
  validating merit order effect found in EDA
- Day of week captures industrial vs residential demand patterns
- Random Forest and tuned XGBoost achieve identical performance
- Tuning XGBoost improved performance by 0.97 percentage points

## Technologies Used
- Python, Pandas, NumPy
- Scikit-learn, XGBoost
- Matplotlib, Seaborn
- SciPy — statistical testing

## How To Run
```bash
pip install pandas numpy scikit-learn xgboost 
            matplotlib seaborn scipy
```
1. Open `1_EDA.ipynb` and run all cells
2. Open `2_Preprocessing.ipynb` and run all cells
3. Open `3_Model_Training.ipynb` and run all cells

## Limitations
- Weather data represents city level averages — not wind 
  farm specific locations
- Dataset covers 2015-2018 — renewable penetration has 
  increased significantly since then
- Median imputation calculated on training data only 
  to prevent leakage
