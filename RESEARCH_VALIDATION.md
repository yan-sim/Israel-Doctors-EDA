# Research validation & interpretation notes

**Status:** public-facing methodological documentation for the 2026 exploratory project. **Not** a certification of clinical data quality or a causal evaluation.

## What can be reproduced from the repository

The curated [portfolio notebook](analysis/Israel_Doctors_EDA_Portfolio.ipynb) loads the stored CSV outputs, displays core comparisons, and generates figures. It is an audit-friendly **downstream presentation layer**, not an independent re-derivation of the Ministry of Health or OECD source extracts. The full v22 notebook remains available unchanged for provenance.

### Confirmed against versioned CSV exports

| Question | Source export | Reproducible description |
| --- | --- | --- |
| Data completion sensitivity | `OECD_2021_Interpolation_Sensitivity.csv` | OECD 2021 foreign-trained share vs graduates correlation remains **−0.358** before and after interpolation (27 countries). Graduates vs practising physicians changes **+0.220** (31) → **+0.270** (32). |
| Physician stock vs actively practising | `Israel_2010_2024_population_physician_growth_summary.csv` | Combined training-stock per 1,000 residents **+8.896%**; practising physician rate **+20.930%**. Different denominators/definitions and should not be interpreted as the same indicator. |
| OECD benchmark sensitivity | `OECD_2021_Israel_Practising_Physicians_Benchmarks.csv`, `OECD_2010_2024_Israel_vs_fixed_medians.csv` | 2021 Israeli practising rate **3.39/1,000**; median **3.79** across 32 reporting countries, versus **3.53** for a 26-country fixed panel. Differences correspond to **3,749** versus approximately **1,310** benchmark-equivalent physicians. |
| Hospital correlations | `MOH_2021_training_quality_correlations_PROVISIONAL.csv` | CHADS **r=−0.1278 (n=21)**, antibiotics **r=−0.1745 (n=24)**, hip fracture **r=+0.2950 (n=23)**. Results are observational, and small sample sizes limit sensitivity. |
| Specialty correlations | `MOH_2020_specialty_vs_2020_quality_pearson_PROVISIONAL.csv` | Cardiology/CHADS **r=−0.7504 (n=9; nominal p≈0.0198)**; surgery/antibiotics **r=−0.1913 (n=10)**; orthopedics/hip fracture **r=+0.4448 (n=10)**. The nominal cardiology p-value is **not** significant after a 3-comparison Bonferroni threshold of 0.0167. Exploratory comparisons beyond these three make confirmatory interpretation still weaker. |
| Cardiology leave-one-hospital-out | `MOH_2020_Cardiology_CHADS_Leave_One_Out.csv` | All recalculated correlations are negative; excluding Shamir gives **r≈−0.630, p≈0.094**. The sign persists, the strength and nominal significance do not. |
| Hip fracture missing-numerator audit | `MOH_Hip_Blank_Numerator_Time_Audit.csv` | **1,470** blank-numerator source records: **1,355** have operation-time \(>48h\), **115** exactly \(48h\), none \(<48h\). The field’s threshold boundary/rounding still matters. Source-record counts must not be called patient counts. |

## What remains limited or unverified

1. **2020 specialty-to-hospital extraction:** a table was transcribed from an Israeli Ministry of Health PDF; all hospital columns and missing values should be checked against the page image before claiming an independently verified extraction. The published table can be found in the [official PDF](https://www.gov.il/BlobFolder/reports/shifts-reduction-joint-team-intermediate-conclusions-report/he/files_committees_shifts-reduction_shifts-reduction-joint-team-Intermediate-Conclusions-Report.pdf). No specialty numerators/denominators are available in the current table, so a percent can represent very few residents.
2. **Attribution of CHADS:** the share of residents in cardiology does not necessarily correspond to the personnel responsible for the hospital CHADS process measure; hospital protocol/department attribution needs checking.
3. **Blank numerator convention:** cross-field evidence exists for hip fracture, but it does not constitute a publisher confirmation for all three measures; sensitivity checks and the `PROVISIONAL` designation remain appropriate.
4. **Case mix & ecological inference:** patient severity, comorbidities, hospital resources, team composition, and other confounding are insufficiently controlled. Hospital-level relationships cannot identify effects of individual physicians’ training.
5. **OECD country sets:** cross-sectional available-case and longitudinal fixed-panel medians answer different comparison questions. Using the median as a staffing target would be an overinterpretation.
6. **2024 graduates series:** a large one-year change appears in the Israel data series, but the reason has **not** been confirmed. Do not attribute it to policy or to a verified definition change.
7. **Scope of the Yatziv reform:** OECD foreign-trained physician stock includes migrants and Israelis trained abroad. It is **not** identical to graduates from the specific institutions affected by the reform.
8. **End-to-end reproducibility:** the review notebook runs from committed derived exports. A clean full refresh from external data plus SQL Server, and a verified SQL migration script, are **not** claimed.

## Correct language for a presentation or job interview

- **Supported:** “We did not detect a consistent negative hospital-level association across the three selected process indicators in 2021.”
- **Unsupported:** “There is no association between training and physician quality.”
- **Supported:** “The specialty-level cardiology finding is a hypothesis for follow-up, limited by nine observations and hospital composition.”
- **Unsupported:** “This analysis proves cardiology graduates of certain institutions deliver worse care.”
- **Supported:** “The benchmark gap equals a certain number of physicians if Israel matched a comparator rate.”
- **Unsupported:** “This proves the exact physician shortage.”

## Analysis limitations vs unfinished tasks

A **structural limitation** such as hospital-level ecological inference should remain visible in the final write-up. An **outstanding validation task** should be recorded here, not silently presented as if completed. This document deliberately distinguishes reproducible computations from clinically validated conclusions.
