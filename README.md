# IMO 2020 Difference-in-Differences Replication Package

## Research Project

**The Impact of IMO 2020 on Port Competitiveness and Container Shipping Costs: A Comparative Analysis of Rotterdam and Hamburg, 2018–2021**

Master's Research Project  
International Logistics and Transportation Management

---

## Overview

This repository contains the replication materials for a Master's research project examining the implementation of IMO 2020 and the differential evolution of container throughput at the ports of Hamburg and Rotterdam between 2018 and 2021.

The empirical analysis uses a Difference-in-Differences (DiD) framework, with Hamburg as the treated port and Rotterdam as the comparison port. Container throughput is used as the main empirical outcome to examine whether Hamburg experienced a different post-2020 trajectory relative to Rotterdam.

The analysis also considers the possible role of asymmetric compliance conditions and costs in interpreting the observed differences between the two ports. The empirical results are interpreted cautiously and are not presented as definitive proof of a causal effect of IMO 2020.

---

## Research Question

The central research question is:

> **To what extent was the implementation of IMO 2020 associated with a differential change in container throughput at Hamburg relative to Rotterdam between 2018 and 2021, and what role may asymmetric compliance costs have played in explaining this difference?**

---

## Empirical Strategy

The study applies a Difference-in-Differences model to quarterly container throughput data for Rotterdam and Hamburg from Q1 2018 to Q4 2021.

The main specification is:

`ln(TEU) = β0 + β1(Post) + β2(Hamburg) + β3(Post × Hamburg) + β4(COVID) + β5(WTO) + β6(Brent) + ε`

where:

- `ln(TEU)` is the natural logarithm of quarterly container throughput.
- `Post` equals 1 from Q1 2020 onward.
- `Hamburg` identifies the Port of Hamburg.
- `Post × Hamburg` is the Difference-in-Differences interaction term.
- `COVID` controls for the pandemic period.
- `WTO` represents global trade conditions using the WTO Goods Trade Barometer.
- `Brent` represents quarterly Brent crude oil prices.

The regression is estimated using OLS with HC1 heteroskedasticity-robust standard errors.

The final dataset contains **32 port-quarter observations**.

---

## Data Sources

### Eurostat

Quarterly container throughput data for Rotterdam and Hamburg are obtained from the Eurostat maritime transport database.

Dataset:

`mar_qg_qm_pvh__custom_21684101_linear_2_0(DCHT).csv.gz`

The analysis uses quarterly TEU observations from **2018 Q1 to 2021 Q4**.

### WTO Goods Trade Barometer

The WTO Goods Trade Barometer is used as a control for changes in global merchandise trade conditions.

Quarterly observations for 2018–2021 are incorporated directly into the analysis notebook.

### Brent Crude Oil Prices

Brent crude oil prices are based on U.S. Energy Information Administration (EIA) Europe Brent Spot Price FOB monthly observations.

Monthly observations are aggregated into quarterly averages for consistency with the quarterly port-throughput dataset.

---

## Repository Contents

### `DiD_IMO2020_Regression_FINAL(DCHT).ipynb`

Main replication notebook.

It contains:

- Eurostat data loading and preparation
- Port and period filtering
- WTO Goods Trade Barometer observations
- Brent crude oil quarterly averages
- variable construction
- pre-treatment trend diagnostic
- baseline Difference-in-Differences regression
- placebo test
- Antwerp robustness specification
- alternative COVID timing specifications
- parallel-trends figure generation
- regression-results export

### `Figure2_Parallel_Trends(DCHT).png`

Parallel-trends figure comparing indexed container throughput at Rotterdam and Hamburg.

The series are indexed to:

**2018 Q1 = 100**

The figure is based on Eurostat quarterly container throughput data.

### `Table4_DiD_Results(DCHT).csv`

Exported results from the baseline Difference-in-Differences regression.

### `mar_qg_qm_pvh__custom_21684101_linear_2_0(DCHT).csv.gz`

Raw Eurostat maritime transport dataset used by the notebook.

### `LICENSE`

MIT License covering the repository.

---

## Main Regression Results

The baseline Difference-in-Differences model produces the following main interaction estimate:

**Post × Hamburg**

- Coefficient: **−0.0570**
- HC1 robust standard error: **0.0252**
- z-statistic: **−2.263**
- p-value: **0.0236**

The exact transformation of the log coefficient is:

`100 × (exp(−0.0570) − 1) ≈ −5.54%`

This indicates that Hamburg experienced an approximately **5.5% weaker post-2020 change in container throughput relative to Rotterdam**, conditional on the controls included in the model.

This estimate is statistically significant at the 5% level.

### Model Statistics

- R²: **0.9833**
- Adjusted R²: **0.9793**
- Observations: **32**
- Standard errors: **HC1 robust**

The high R² should not be interpreted as evidence of causal identification. A substantial part of the explanatory power reflects persistent differences in throughput scale between Hamburg and Rotterdam.

---

## Control Variables

The final baseline model produces the following estimates for the principal controls:

- `Post`: β = **0.0362**, p = **0.1515**
- `COVID`: β = **0.0069**, p = **0.7093**
- `WTO`: β = **−0.0013**, p = **0.3391**
- `Brent`: β = **0.0019**, p = **0.0396**

The Brent coefficient is statistically significant at the 5% level in this specification. Given the small sample and two-port design, this association should be interpreted cautiously rather than as evidence of a direct causal relationship.

---

## Identification Diagnostics

### Pre-Treatment Trend Diagnostic

A differential linear pre-treatment trend test produces:

- Coefficient: **0.00479**
- p-value: **0.3760**

The test does not detect a statistically significant differential linear pre-treatment trend between Hamburg and Rotterdam.

This provides supportive evidence for the empirical design but does **not** by itself confirm the parallel-trends assumption.

### Placebo Test

A placebo treatment applied before the actual IMO 2020 implementation produces:

- Placebo DiD coefficient: **0.0329**
- p-value: **0.0354**

The statistically significant placebo estimate indicates evidence of differential pre-treatment dynamics.

For this reason, the main DiD estimate should not be interpreted as definitive causal proof that IMO 2020 itself caused the observed post-2020 difference.

---

## Robustness Checks

### Antwerp Comparison

Replacing Rotterdam with Antwerp as the comparison port produces:

- DiD coefficient: **−0.1010**
- p-value: **0.0024**
- Exact transformed effect: approximately **−9.61%**

The direction of the estimate remains negative and statistically significant.

### Alternative COVID Timing

The COVID-period definition is shifted across alternative starting quarters:

| COVID start | DiD coefficient | p-value |
| --- | ---: | ---: |
| Q1 2020 | −0.0570 | 0.0212 |
| Q2 2020 | −0.0570 | 0.0236 |
| Q3 2020 | −0.0570 | 0.0084 |

The estimated interaction remains negative and statistically significant across these alternative specifications.

These robustness checks demonstrate specification stability, but they do not eliminate the identification concerns indicated by the significant placebo test.

---

## Interpretation

Taken together, the results identify a statistically significant differential post-2020 throughput pattern between Hamburg and Rotterdam.

The direction of the estimated difference is consistent with the study's theoretical discussion of heterogeneous regulatory and compliance conditions. However, the analysis cannot isolate IMO 2020 from all other factors affecting port throughput during the period.

Important limitations include:

- the comparison of only two principal ports in the baseline model;
- the small sample of 32 port-quarter observations;
- the COVID-19 disruption;
- pre-existing differential dynamics indicated by the placebo test;
- possible omitted port-specific and carrier-specific factors;
- the absence of vessel-level information on scrubber adoption and compliance strategies.

The results should therefore be interpreted as evidence of a **statistically significant differential post-2020 throughput pattern**, rather than as definitive proof of a causal effect of IMO 2020.

---

## Reproducing the Analysis

To reproduce the analysis:

1. Download or clone this repository.
2. Open `DiD_IMO2020_Regression_FINAL(DCHT).ipynb` in Google Colab or Jupyter Notebook.
3. Ensure that the Eurostat dataset  
   `mar_qg_qm_pvh__custom_21684101_linear_2_0(DCHT).csv.gz`  
   is available in the notebook working directory.
4. Run the notebook cells sequentially from top to bottom.
5. The notebook estimates the baseline model and the diagnostic and robustness specifications.
6. The notebook also generates:
   - `Figure2_Parallel_Trends(DCHT).png`
   - `Table4_DiD_Results(DCHT).csv`

The WTO Goods Trade Barometer observations and quarterly Brent price series required by the regression are documented directly in the notebook.

---

## Software

The analysis is implemented in Python using standard data-analysis and econometric libraries, including:

- pandas
- NumPy
- statsmodels
- Matplotlib

The notebook can be executed in Google Colab or a compatible local Jupyter environment.

---

## Reproducibility Note

This repository is provided to improve transparency and reproducibility of the empirical analysis presented in the Master's research project.

The repository contains the dataset, analytical notebook, regression-results export, and parallel-trends figure required to inspect and reproduce the principal quantitative analysis.

Results should be interpreted together with the methodological assumptions, limitations, theoretical framework, and discussion presented in the full research project.

---

## License

This repository is distributed under the MIT License. See `LICENSE` for details.
