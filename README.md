# NextStep Cohort Income & Debt Analysis

**Python • pandas • statsmodels • matplotlib**

## 1. Introduction

This project leverages data from the Next Step (NS) Study—a longitudinal survey of 15,770 individuals born in England in 1989–1990—to identify factors that influence weekly income and debt levels at age 25. Participants were first interviewed at age 14 in 2004, then annually through 2010, with an additional wave in 2015–16 (8 total waves). We constructed two derived datasets, **W8DINCW** (income) and **W8QDEB2** (debt), to drive our analysis of socio‐demographic predictors at Wave 1 (age 14) and their impact on financial outcomes at Wave 8 (age 25).

Our final regression models reveal that over half of the significant predictors for both income and debt originate from Wave 1—including ethnic group, family socioeconomic class, mother’s marital status, independent schooling, and mother’s highest qualification—underscoring the lasting effect of early-life circumstances on adult financial well-being.

## 2. Data

- **Source:** Next Step Study (NS), waves 1–8  
- **Datasets:**  
  - `W8DINCW.csv` – cleaned weekly income at age 25  
  - `W8QDEB2.csv` – cleaned debt measures at age 25  
- **Size:**  
  - Income: 3,804 observations (after cleaning)  
  - Debt: 2,611 observations (after cleaning)

## 3. Methods

1. **Data Cleaning & Preparation**  
   - Negative values → NA; dropped predictors with >90% missing  
   - Converted remaining NAs in categoricals to a “missing” level  
2. **Exploratory Analysis**  
   - Boxplots & scatterplots to identify promising predictors  
   - Level-merging for high-cardinality categoricals (see Appendix 2)  
3. **Feature Selection**  
   - **Backward elimination** of non-significant variables (p > 0.05)  
   - Checked multicollinearity via VIF; resolved aliasing via manual removal  
4. **Modeling**  
   - Linear regression on raw income, then **log-transformed** income to address heteroscedasticity  
   - Linear regression on raw debt (no transformation)  
5. **Evaluation**  
   - Train/test split: 90% train, 10% test (cross-validation plots in Appendix 9)  
   - Diagnostics: residual vs. fitted, QQ plots, Cook’s distance  

## 4. Results

### Income Model (W8DINCW)

- **Final predictors:** ethnic group (W1ethgrpYP), parental socioeconomic class (W1nssecfam), mother’s highest qualification (W1hiqualmum), …  
- **Multiple R-squared:** 0.7481  
- **Adjusted R-squared:** 0.7424  
- **Residual Std. Error:** 35.99  

After log-transforming income:

- **Multiple R-squared:** 0.7770  
- **Adjusted R-squared:** 0.7715  

### Debt Model (W8QDEB2)

- **Final predictors:** housing tenure (W8TENURE), independent schooling (IndSchool), household gross income category (W1GrssyrHH_category), parental qualifications, …  
- **Multiple R-squared:** 0.08298  
- **Residual Std. Error:** 27847.21  
