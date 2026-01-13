# Does a High Interest Rate Suppress Consumption Growth?

## 1. Research Question

This project investigates the following question:

**Do standard macroeconomic conditions explain short-term fluctuations in U.S. consumption, particularly under high-interest-rate environments?**

Rather than maximizing predictive accuracy, the goal is to examine whether commonly used macro indicators—such as interest rates, inflation, unemployment, and income—contain explanatory power for short-term consumption growth.

---

## 2. Data

All data are sourced from the Federal Reserve Economic Data (FRED) database and are observed at a monthly frequency.

**Variables used:**

- **PCEC96**  
  Real Personal Consumption Expenditures  
  → Used to construct the target variable

- **FEDFUNDS**  
  Federal Funds Effective Rate  
  → Monetary policy stance

- **CPIAUCSL**  
  Headline Consumer Price Index  
  → Overall inflation pressure

- **CPILFESL**  
  Core Consumer Price Index (excluding food and energy)  
  → Persistent inflation component

- **UNRATE**  
  Unemployment Rate  
  → Labor market conditions

- **DSPIC96**  
  Real Disposable Personal Income  
  → Household purchasing power

The sample period begins in 2007 and extends through 2025, subject to data availability after lag construction.

---

## 3. Target Variable Construction

The target variable is defined as the **3-month log growth rate of real personal consumption expenditures**:

\[
y_t = \log(PCE_t) - \log(PCE_{t-3})
\]

**Why 3-month growth?**
- Reduces high-frequency monthly noise
- Reflects short-term economic dynamics more meaningfully than 1-month changes
- Allows limited lag for policy and labor market effects to materialize

Because this is a rolling growth measure, large shocks mechanically affect multiple adjacent observations.

---

## 4. Methodology

A **Ridge regression** model is employed to analyze the structural relationship between macroeconomic variables and consumption growth.

Key design choices:
- Lagged macro variables are used to respect temporal ordering
- Features are standardized using `StandardScaler`
- Regularization (Ridge) mitigates multicollinearity common in macro data

This model is intentionally simple to preserve interpretability.  
The objective is **explanatory analysis**, not black-box forecasting.

---

## 5. Evaluation Strategy

The dataset is split by time to avoid data leakage:

- **Training set:** pre-2020
- **Test set:** 2020 onward

To account for the COVID-19 shock, performance is evaluated under two test settings:

1. **With COVID-19**  
   → Full test period

2. **Without COVID-19 (adjusted)**  
   → December 2019 to June 2021 excluded  
   (Adjusted to reflect the 3-month growth window)

This separation allows the analysis to distinguish between normal economic dynamics and exogenous crisis shocks.

---

## 6. Results

### Quantitative Findings
- RMSE improves after excluding the COVID-19 period, indicating better absolute prediction accuracy during normal times.
- R² becomes unstable or strongly negative when COVID-19 is excluded, due to the extremely low variance of consumption growth in normal regimes.

This behavior is expected given the definition of R² and does not imply model failure.

### Coefficient Interpretation
- Interest rates and unemployment exert small but persistent negative effects on consumption growth.
- Inflation variables exhibit weaker and less consistent relationships.
- Disposable income changes contribute marginally at short horizons.

Overall, macroeconomic variables explain **average consumption dynamics**, but not high-frequency fluctuations.

---

## 7. Visualization

The figure below compares actual and predicted 3-month consumption growth over the full sample period.

Key observations:
- During normal periods, predictions track a smooth average path.
- During crisis periods (notably COVID-19), the model fails to react to sharp collapses and rebounds.

This reflects the exogenous and policy-driven nature of the shock, which is not captured by standard macro indicators.

---

## 8. Limitations

- The model cannot anticipate sudden behavioral or policy-driven shocks.
- Short-term consumption growth exhibits very low variance during normal periods, limiting predictability.
- The analysis relies solely on aggregate macroeconomic indicators and excludes micro-level consumption behavior.

These limitations are intrinsic to the research question and data structure.

---

## 9. Conclusion

**Macroeconomic conditions influence the level of consumption,  
but short-term consumption growth remains largely unpredictable outside of crisis periods.**

This project highlights the limits of macro-based regression models in explaining short-run consumption dynamics, especially during periods of economic stability.

---

