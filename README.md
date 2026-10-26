# DAS-Final-Project-Option1
This is the final project for the LEAP Data analysis course, including a hands-on example in order to review basic data analysis concepts
# Understanding Diabetes Progression | Final Project Portfolio

**Course**: LEAP – Data Analytics and Statistics with Applications  
**Scenario**: Scenario 1 – Understanding Diabetes Progression  


---

## 1. Project Title & Overview
This portfolio presents an end-to-end data analytics and statistical modeling project investigating disease progression in diabetes patients over a one-year baseline period.

## 2. Research Question
*Which patient clinical and biological characteristics are associated with diabetes progression, what do regression models reveal, and what valid conclusions can be drawn without overstepping into unwarranted causal claims?*

---

## 3. Data Description & Responsible Use
- **Source**: NCSU-hosted diabetes dataset (`diabetes.tab.txt`).
- **Sample Size**: 442 patients, 10 predictor variables, and 1 continuous progression measure.
- **Variables**:
  - `progression` ($Y$): Quantitative measure of disease progression one year after baseline.
  - Demographic & Clinical: `age`, `sex` (treated as categorical factor), `bmi` (body mass index), `bp` (average blood pressure).
  - Serum Measurements: `s1` (total serum cholesterol), `s2` (low-density lipoproteins), `s3` (high-density lipoproteins), `s4` (total cholesterol / HDL), `s5` (log of serum triglycerides level), `s6` (blood glucose sugar level).
- **Data Quality**: 0 missing values, 0 duplicate rows, no out-of-range artifacts.
- **Responsible Interpretation**: As clinical data, privacy safeguards and careful statistical reporting are essential. Associations must not be communicated as direct causal clinical guidelines.

---

## 4. Analysis Workflow
1. **Data Cleaning & Preprocessing**: Imported raw tab-separated data, normalized column names to lower case, converted `sex` into a categorical factor, and confirmed data cleanliness.
2. **Exploratory Data Analysis (EDA)**: Computed summary metrics (mean, median, SD, IQR) and plotted distributions (histograms and boxplots).
3. **Correlation & Feature Selection**: Computed Pearson correlation matrix among continuous variables, identified collinear serum pairs (`s1` vs `s2`, `s3` vs `s4`), and selected top uncorrelated predictors (`bmi`, `bp`, `s5`).
4. **Regression Modeling**:
   - Simple Linear Regression: `progression ~ bmi`
   - Multiple Linear Regression: `progression ~ bmi + bp + s5`
5. **Model Evaluation & Diagnostics**: Checked residual behavior via Residuals vs. Fitted plot, evaluated multicollinearity using Variance Inflation Factors (VIF), and assessed confidence intervals.

---

## 5. Key Results Summary

### Model Comparison Table
| Metric | Simple Model (`bmi`) | Multiple Model (`bmi` + `bp` + `s5`) |
| :--- | :--- | :--- |
| **Formula** | $\widehat{Y} = -117.77 + 10.23(\text{bmi})$ | $\widehat{Y} = -334.88 + 6.50(\text{bmi}) + 0.90(\text{bp}) + 49.58(\text{s5})$ |
| **$R^2$** | 0.344 | 0.480 |
| **Adjusted $R^2$** | 0.342 | 0.477 |
| **Residual Std Error ($\sigma$)** | 62.51 | 55.77 |
| **All Predictors $p$-value** | $< 0.001$ | $< 0.001$ for all terms |

### Diagnostic Metrics (Multiple Model)
- **Multicollinearity (VIF)**:
  - `bmi`: 1.34
  - `bp`: 1.27
  - `s5`: 1.34
  *(All VIF values are well below critical thresholds, indicating no problematic collinearity).*
- **Residuals vs. Fitted**: Displayed balanced spread around zero without severe funneling or non-linear patterns.

---

## 6. Interpretation & Limitations
- **Observational Nature**: This study is observational. Regression coefficients show statistical associations, **not direct causal effects**.
- **Omitted Variables (Confounders)**: Crucial clinical factors such as medication regimen, lifestyle/diet changes, physical activity, and treatment compliance are missing from the dataset.
- **Generalizability**: Findings reflect the specific cohort of 442 patients and may not directly generalize across diverse demographics or distinct clinical settings without further external validation.
- **Unexplained Variance**: Approximately 52% of disease progression variability remains unexplained by the model, precluding its standalone use for individual prognosis.

---

## 7. Deliverables & Repository Navigation
- 📁 **[scripts/2b_Scenario1_Diabetes_Analysis.R](scripts/2b_Scenario1_Diabetes_Analysis.R)**: Complete, commented, reproducible R code.
- 📄 **[report/Analytical_Report.pdf](report/Analytical_Report.pdf)**: 4–6 page structured PDF report covering all 6 project questions.
- 📊 **[presentation/Decision_Maker_Presentation.pdf](presentation/Decision_Maker_Presentation.pdf)**: 5-slide non-technical presentation tailored for healthcare leadership.

---

## 8. Personal Reflection
- **Key Learnings**: Gained hands-on experience differentiating predictive performance ($R^2$, adjusted $R^2$) from clinical utility, alongside mastering diagnostic checks (VIF, residual patterns) in R.
- **Challenges**: Navigating strong inter-correlations among serum variables (`s1`–`s6`) required careful justification of predictor selection to avoid redundant information.
- **Future Improvements**: Given more time and data, evaluating non-linear interactions, testing regularization techniques (Ridge/Lasso), and collecting longitudinal patient treatment history would significantly improve predictive reliability.
