# Predicting College Freshman Academic Success: Pre-College Indicators Analysis

## Executive Summary

This project investigates how pre-college academic and environmental/context variables relate to first-year college GPA. Using HSLS:09 (2009-2016), we analyzed 23,503 students in the raw data and ~2,271 complete-case observations for modeling. Across both EDA and predictive modeling, we found that **academic preparation (especially cumulative high school GPA and AP/IB credit exposure) is the strongest predictor**, while context variables add smaller but still meaningful signal.

## Research Question

To what extent do pre-college academic indicators predict first-year college academic performance? We compare academic factors (high school GPA, AP/IB credits, rigor, school test context) and environmental/context factors (SES, school climate/problem scales, family and school background) to evaluate their relative predictive power for freshman GPA.

## Dataset Overview

- **Source**: HSLS:09 (NCES)  
- **Raw sample**: 23,503 students  
- **Modeling sample**: ~2,271 complete cases  
- **Outcome**: `FRESHMAN_GPA` (`X5YR1GPA`)  
- **Predictors**: academic, school context, and family context variables selected from the HSLS codebook and cleaned feature set

---

## EDA Findings (Descriptive Patterns)

### 1. GPA Distribution and Transition to College
Cumulative high school GPA is right-skewed, with many students near higher GPA ranges. Freshman GPA is also right-skewed but includes a small spike at zero. This suggests that college performance shifts downward for part of the sample relative to high school outcomes, indicating a meaningful transition effect.

### 2. High School GPA vs Freshman GPA
Scatter and regression plots show a clear positive association between cumulative HS GPA and freshman GPA. Students with stronger high school records generally perform better in first-year college, though there is visible spread, meaning GPA alone does not fully explain outcomes.

### 3. AP/IB Exposure and Early College Performance
Students with more AP/IB credits show higher average freshman GPA. Binned comparisons (0, 1–3, 4–6, 7+) show an upward trend, suggesting that exposure to advanced coursework in high school is associated with stronger early college outcomes.

### 4. Context Variables from EDA
SES and school-context variables show weaker but noticeable gradients. For example, higher SES and better school context generally align with higher freshman GPA averages. However, effects are less consistent than GPA/AP trends, and some categories (especially high-income bins) have small counts that make estimates noisy.

### 5. Correlation Structure
Correlation analysis shows:
- strong positive relationship between HS GPA variables and freshman GPA
- moderate relationship for AP/IB credits and SES
- weak relationships for household size and school mobility
- notable overlap among context variables (e.g., school problem vs school climate), which raises multicollinearity concerns in multivariable models

---

## Modeling Findings (Predictive Comparison)

### 1. Linear Model Comparison
Using the same target (`FRESHMAN_GPA`):

- **Academic-only model**: `R² ≈ 0.285`
- **Environment-only model**: `R² ≈ 0.063`
- **Combined linear model**: `R² ≈ 0.298`

This shows academic predictors explain much more variance than context-only predictors, and adding context to academic variables improves performance only modestly.

### 2. Key Coefficients in Combined Linear Model
In combined models, the most reliable contributors were:
- `HS_GPA_CUM` (largest effect)
- `TOTAL_AP_CREDITS`
- `SES_COMPOSITE_URBANICITY_ADJ` (smaller but significant in some specifications)

Some context coefficients changed sign or significance across model setups, likely due to shared variance and collinearity among SES/school indicators.

### 3. Nonlinear Model Check (XGBoost)
To test whether nonlinear interactions improve prediction:

- **Tuned XGBoost (5-fold CV)**  
  - `CV R² ≈ 0.312`  
  - `CV RMSE ≈ 0.756`  
  - `CV MAE ≈ 0.565`

XGBoost performs slightly better than combined linear regression (`0.312` vs `0.298`), indicating some nonlinear structure, but the improvement is modest and does not change the core interpretation.

### 4. Feature Importance from XGBoost
`HS_GPA_CUM` remains the dominant feature by a clear margin. Secondary features include AP credits and selected school/context variables, but their importance is notably smaller.

---

## Conclusion

Bringing EDA and modeling together, the project consistently shows that **academic preparation is the strongest signal of first-year college GPA**, especially cumulative high school GPA and AP/IB coursework. Environmental/context variables are not irrelevant, but they act more as incremental background factors than primary predictors in this setup.

Even with linear + nonlinear models, explained variance stays around 30%, so a large share of freshman GPA remains influenced by factors not captured here (e.g., college fit, mental health, support systems, unobserved student traits). The project therefore supports a practical conclusion: traditional academic preparation remains the most reliable early predictor, while context adds useful but smaller predictive information.

## Limitations and Next Steps

1. This is observational modeling (predictive association, not causal inference).  
2. Complete-case filtering reduces sample size and may introduce selection bias.  
3. Composite and coded variables may introduce interpretation and coding-direction sensitivity.  
4. Freshman GPA is only an early outcome; future work should include retention and degree attainment outcomes.  
5. A stronger next step is subgroup analysis and improved missing-data handling to test robustness across student populations.
