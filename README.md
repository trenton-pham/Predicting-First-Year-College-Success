# Predicting College Freshman Academic Success: Pre-College Indicators Analysis

## Executive Summary

This project investigates the predictive power of pre-college academic indicators on first-year college performance. Using data from the High School Longitudinal Study (HSLS: 2009-2016), we analyzed over 23,000 students to determine which high school factors most strongly correlate with college freshman GPA. Our findings reveal that **high school GPA is the dominant predictor of college success**, with accumulated GPA across all four years showing correlations exceeding 0.5. We also identified meaningful contributions from academic rigor, standardized test exposure, and socioeconomic context, while household size, homework hours, and school mobility showed negligible predictive power.

## Research Question

To what extent do pre-college academic indicators predict first-year college academic performance? Using high school GPA, standardized test scores (SAT/ACT context), coursework rigor, AP/IB credits, and educational context factors, we model students' first-year college performance to evaluate the relative predictive power of these variables and identify systematic patterns of under- or over-performance.

## Dataset Overview

- **Source**: HSLS: 09 (High School Longitudinal Study 2009-2016), available at https://nces.ed.gov/surveys/hsls09/
- **Sample Size**: 23,503 students (after data cleaning: ~13,000 complete cases)
- **Time Period**: 2009-2016 longitudinal tracking from secondary education through college
- **Key Variables Selected**: 25 variables after feature selection process across academic, school context, and family context dimensions

For details on our variable selection methodology, see `variable_selection.ipynb` where we narrowed down from 9,000+ variables to 25 key predictors.

## Key Findings

### Strong Predictors of College Freshman GPA (Correlation > 0.35)

1. **High School GPA (All Years)**: r > 0.50
   - Cumulative high school GPA is the strongest single predictor
   - Annual GPAs (9th-12th grade) all show strong correlations with freshman GPA
   - Suggests sustained academic performance in high school translates most directly to college success

2. **AP/IB Credit Completion**: r ≈ 0.30
   - Exposure to college-level coursework in high school provides meaningful advantage
   - Students with more AP/IB credits show notably higher freshman GPAs
     
### Moderate Predictors (Correlation 0.15-0.25)

4. **Socioeconomic Status (SES Composite)**: r ≈ 0.20
   - SES shows stronger predictive power than raw family income bracket
   - Reflects cumulative resource access, academic support infrastructure
   - More nuanced measure of educational advantage

5. **Student Motivation**: r ≈ 0.19
   - Student-reported school motivation shows modest positive correlation
   - Effect plateaus at higher motivation levels

6. **School Academic Context**: r ≈ 0.15
   - School average SAT/ACT performance moderately predicts student outcomes
   - School climate scales (both administrator and student perceptions) show weak but measurable relationships
   - Higher SES schools correlate with better school problem management

### Non-Predictive Factors (Correlation < 0.10)

- **Homework Hours**: No meaningful correlation despite intuitive appeal
- **Household Size**: No clear trend despite theoretical concerns about resource dilution
- **Number of High Schools Attended**: Minimal impact on freshman GPA (when controlling for sample size bias)

## Detailed Analysis

### 1. High School GPA Performance Trajectories

**Distribution Patterns**: The distribution of cumulative high school GPA shows pronounced right-skew, with many students achieving high GPAs (3.5-4.0). In contrast, freshman GPA shows similar right-skew but with a notable spike at zero, hypothesized to represent student attrition or academic failure. This indicates that college represents a meaningful performance recalibration for many students.

**Comparison Insight**: The high-concentration of 4.0 GPAs in high school dramatically decreases in college, suggesting either: (1) higher college course difficulty, (2) different grading standards, or (3) self-selection effects where only highly-prepared students enroll.

### 2. Freshman GPA vs. High School GPA Relationship

The linear regression reveals a positive relationship (slope ~0.70, statistically significant) where freshman GPA increases with high school GPA. However, the wide scatter around this fitted line indicates substantial variance unexplained by high school GPA alone. Key observations:

- Students with high school GPAs of 3.5+ show more concentrated freshman GPA outcomes
- Lower high school GPA students show extreme variance, with some achieving 3.0+ college GPAs and others failing
- The relationship is genuine but far from deterministic, indicating other factors substantially affect college performance

### 3. Coursework Rigor Impact

Students completing college-bound core curricula achieve meaningfully higher median freshman GPAs compared to those in standard core or minimal core pathways. The boxplot demonstrates:

- **Rigor Level 1** (College-bound core): Median GPA ~2.8, tighter distribution
- **Rigor Levels 5-6** (Minimal/other): Median GPA ~2.5, slightly wider variance
- Difference of approximately 0.3 GPA points represents meaningful educational advantage

This suggests coursework rigor serves as both a direct preparation mechanism and a proxy for school/peer academic culture.

### 4. AP/IB Credit as College-Level Readiness Indicator

Students with 7+ AP/IB credits show markedly higher freshman GPAs (median ~3.0) compared to students with zero AP/IB credits (median ~2.6). The progression is clear:

- 0 credits: Mean GPA ~2.6
- 1-3 credits: Mean GPA ~2.75
- 4-6 credits: Mean GPA ~2.85
- 7+ credits: Mean GPA ~3.0

However, note the small sample sizes for higher credit tiers, which may introduce sampling variability.

### 5. School Context and Academic Environment

**School Climate vs. Problem Scale**: Schools with better-managed issues (lower problem scale) demonstrate significantly better school climate. The strong negative relationship suggests that institutional problems directly undermine school environment perception.

**School Context Predicting Outcomes**: While school climate and problem scales show statistically significant relationships with freshman GPA, effect sizes are modest (correlations ~0.15). Schools with better climates produce students with ~0.2 higher median GPAs. This suggests school environment influences outcomes but likely through mechanisms not fully captured by these summary scales.

**School Average Test Scores**: Schools with higher average SAT performance show student outcomes distributed in higher GPA quartiles. Q1 (lowest SAT schools) students show median freshman GPA ~2.5; Q4 (highest SAT schools) students show median ~2.8. The relationship is present but not overwhelming, indicating many factors beyond school average performance determine individual student outcomes.

### 6. Socioeconomic and Family Context

**Family Income Bracket Effects**: Mean freshman GPA generally increases from income bracket 1-7 (from ~2.5 to ~2.8), suggesting cumulative advantage of higher-resourced families. However, income brackets 10-12 show regression or nonsensical patterns, likely due to small sample sizes in these categories (n<50), making them unreliable for interpretation.

**SES Composite Impact**: The socioeconomic status composite (urbanicity-adjusted) shows clearer positive relationship than raw income brackets. Students with higher SES composite scores achieve approximately 0.3-0.4 higher freshman GPAs across the distribution. This more sophisticated measure captures neighborhood/regional economic context beyond household income alone.

**Interpretation**: SES effects likely operate through multiple channels: access to test prep, tutoring, academic counseling, and peer effects from economically advantaged peer groups.

### 7. Student Motivation

The distribution of student-reported school motivation is left-skewed, indicating this sample is relatively academically motivated. Breaking motivation into quintiles reveals clear GPA progression: Q1 (lowest motivation) students average ~2.4 GPA; Q5 (highest motivation) students average ~2.9 GPA. The effect size (~0.5 GPA difference) is substantial, though directionality remains ambiguous: does high motivation lead to college success, or does prior success generate motivational confidence?

### 8. Correlation Heatmap Summary

The comprehensive correlation analysis identified critical confounding relationships:

- **SES and Family Income**: High multicollinearity (r ≈ 0.75). We retained SES as it provides more contextual information.
- **School Problem and Climate Scales**: Moderate negative correlation (r ≈ -0.65), suggesting they measure related school-functioning constructs.
- **School Test Averages and Problem Scale**: Negative correlation (r ≈ -0.50), indicating school quality/resources relate to student preparation levels.
- **Freshman GPA Correlation**: All high school GPA measures show r > 0.50. AP credits, rigor, and SES show r ≈ 0.25-0.30. Student motivation, test context, and school climate show r ≈ 0.10-0.20.

## Model Implications and Framework

The analysis suggests a hierarchical model of college readiness determinants:

**Tier 1 (Strongest)**: Historical academic performance (High School GPA)
- Demonstrates sustained effort, capability, and adaptation to academic demands
- Most direct predictor of future academic performance

**Tier 2 (Moderate)**: Academic challenge and preparation (AP/IB)
- Exposure to college-level content directly prepares students

**Tier 3 (Weak)**: Broader Context (SES, School Climate, Student Motivation)
- Provide background/moderating effects
- May operate through mechanisms not fully captured by their summary measures

**Non-Predictive**: Structural factors (household size, school mobility, homework hours)
- Lack direct predictive power in this dataset
- May be overshadowed by sorting effects or indirect pathways

## Limitations and Considerations

1. **Cross-Sectional Analysis**: Our analysis is fundamentally descriptive. We cannot establish causal mechanisms; high school GPA and college GPA may both reflect unmeasured traits (e.g., conscientiousness, inherent ability).

2. **Sample Composition Bias**: The HSLS:09 dataset excludes students who did not attend college or for whom follow-up data was unavailable. This creates sample selection bias favoring college-attending students, likely understating variance and overestimating predictive relationships.

3. **Outliers and Data Quality**: The spike of zero freshman GPAs lacks clear explanation and may represent miscoded dropouts, failed completions, or administrative anomalies. Sensitivity to this coding decision exists.

4. **Unobserved Variables**: Variables like test anxiety, mental health, family trauma, or college fit (institution type, major alignment) are not captured but likely meaningfully affect freshman outcomes.

5. **Temporal Dynamics**: The study tracks cohorts entering college around 2013-2014, potentially reflecting pre-pandemic educational contexts and norms that may not generalize to current cohorts.

6. **Missing Mechanism Understanding**: Correlations with moderate strength (0.15-0.25) for variables like motivation and school climate suggest important pathways remain unmeasured. Qualitative research on how school context affects college adaptation would strengthen mechanistic understanding.

## Recommendations for Future Work

1. **Longitudinal Outcome Tracking**: Extend analysis to include sophomore-year and cumulative college GPA, retention rates, and time-to-graduation to assess whether predictive patterns stabilize or shift.

2. **Disaggregated Analysis**: Examine predictive patterns separately by demographics (gender, race, first-generation status) to identify equity gaps and reveal whether predictors operate uniformly across groups.

3. **Mechanism Investigation**: Conduct qualitative case studies on high under/over-performers to understand how contextual factors (school transitions, family circumstances, academic support) operate through student experience.

4. **Institutional-Level Analysis**: Use hierarchical modeling to separate student-level and school-level effects, quantifying how much variance in freshman GPA represents student differences vs. college/program differences.

5. **Recent Cohorts**: Replicate with more recent data to assess whether predictive relationships have shifted in response to test-optional policies, increased college enrollment, or pandemic-related educational changes.
