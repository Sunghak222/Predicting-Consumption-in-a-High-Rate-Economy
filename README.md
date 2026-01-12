# Project Title

## 1. Research Question
- What happens to consumption under a high-interest-rate environment?

## 2. Key Findings
- Consumption contraction is primarily driven by level effects such as interest and unemployment rate.
- Short-term changes in inflation and income play a secondary role.
- The model captures direction and timing but smooths extreme shocks such as COVID-19.

## 3. Data
The analysis uses monthly U.S. macroeconomic time-series data from FRED:

- **PCEC96** – Real Personal Consumption Expenditures  
  *(used to construct the 3-month consumption growth target)*

- **FEDFUNDS** – Federal Funds Effective Rate  
  *(policy interest rate)*

- **CPIAUCSL** – Consumer Price Index (Headline CPI)

- **CPILFESL** – Core Consumer Price Index  
  *(excluding food and energy)*

- **UNRATE** – Unemployment Rate

- **DSPIC96** – Real Disposable Personal Income


## 4. Methodology
- Target: 3-month log consumption growth
- Model: Ridge regression
- Features: Level + change hybrid
- Reason for not using ARIMA/LSTM

## 5. Results
- RMSE ≈ 0.035
- R² ≈ −0.01
- Coefficient interpretation

## 6. Limitations
- COVID-19
- Monthly frequency
- Linear structure
