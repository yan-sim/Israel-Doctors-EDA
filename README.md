# Israel Doctors EDA | Physician Supply, Training and Hospital Quality

**Exploratory Data Analysis · Experis Academy · 2026**

This project examines a public-health policy dilemma in Israel: how to expand the physician workforce while safeguarding medical training and quality of care. It combines OECD and World Bank indicators with Israeli Ministry of Health data on residents and hospital process measures.

> **Scope:** This is an exploratory, observational study. Hospital-level associations cannot establish the quality of individual physicians, causal effects of medical education, or the impact of the Yatziv reform.

## Research questions

1. **Supply:** How reliant is Israel on internationally trained physicians, and how did physician supply change relative to population growth?
2. **Quality:** Is the share of hospital residents who graduated from institutions not approved under the relevant reform criteria associated with performance on selected hospital quality-process measures?

The second question concerns **hospital composition and hospital outcomes**, not individual doctors' treatment results.

## Key findings

| Analysis | Finding | Interpretation |
| --- | --- | --- |
| Foreign-trained physician stock, 2021 | **57.8%** in Israel vs **~13.5%** median among reporting OECD countries | Israel is unusually reliant on foreign-trained physicians. The category includes immigrants and Israelis who studied abroad; it is **not** the population directly affected by the reform. |
| Israel, 2010–2024 | Combined training-based physician stock per 1,000 residents **+8.9%**; separate *practising-physicians* indicator **+20.9%** | These are **different series and populations** and must not be conflated. |
| OECD practising physician comparison, 2021 | Israel **3.39** per 1,000; median **3.79** (32 reporting countries) or **3.53** (fixed panel of 26 countries) | The corresponding benchmark-equivalent differences are ~**3,749** or ~**1,310** physicians. Neither is a medical staffing requirement or normative shortage estimate. |
| Hospitals, 2021 | Pearson \(r\): **−0.128** (CHADS, n=21), **−0.174** (colon antibiotics, n=24), **+0.295** (hip-fracture surgery within 48h, n=23) | No consistent negative association was detected in these indicators. Sample sizes and case-mix/measurement limitations prevent a claim of no association. |
| Specialties, 2020 | Cardiology share vs CHADS \(r = −0.750, n=9\); nominal \(p≈0.020\) | **Exploratory only:** not significant after correction for three reported tests; sensitive to hospital composition, and specialty extraction / indicator attribution still require source-level verification. |

The 2024 change in the medical-graduates series remains unexplained; no structural-break explanation is claimed.

## Notebooks and data

- **[Portfolio review notebook](analysis/Israel_Doctors_EDA_Portfolio.ipynb)** — concise, runnable presentation of **existing CSV exports** (reproduces the displayed summaries and sensitivity charts, not the full raw-data pipeline).
- **[Full exploratory notebook (v22)](analysis/Israel_Doctors_EDA_Exploration_22.ipynb)** — original, detailed investigation with saved outputs and historical working notes; retained for auditability.
- **[Hebrew project overview](analysis/README_HE.md)**.
- **[Methodology, validation status and limitations](RESEARCH_VALIDATION.md)** — what has actually been checked, what remains provisional, and source references.
- [Exported tables](analysis/exports/), [source and intermediate CSVs](analysis/data/), [chart files](analysis/charts/).
- [SQL Server backup](Israel_Doctors_EDA.bak) and [original Cursor project archive](Experis_Israel_Doctors_Cursor_Project_v22.zip) are retained as source/legacy artifacts. No standalone validated SQL query scripts are currently included.

## Reproduce the review notebook

Requires Python 3.10+ and Jupyter/VS Code/Cursor.

```bash
git clone https://github.com/yan-sim/Israel-Doctors-EDA.git
cd Israel-Doctors-EDA/analysis
python -m pip install -r requirements.txt
jupyter notebook Israel_Doctors_EDA_Portfolio.ipynb
```

Execute **Run All** from the `analysis/` working directory. The portfolio notebook reads local, versioned CSV exports and does **not** require SQL Server. The original v22 notebook has additional upstream processing and has **not** been certified here by a fresh end-to-end rerun. The optional `.bak` file requires a separate SQL Server restoration and should be reviewed before reuse.

## Quality-measure caveat

Hospital process-rate calculations use an interpretation that some blank numerator fields represent **zero documented successes**. A cross-field audit of hip-fracture operation time supports that interpretation for records above 48 hours: 1,355 blank-numerator source records are above the threshold; another 115 have a recorded value **exactly 48 hours**, where boundary definitions/rounding need care. The interpretation is **not independently confirmed for every metric** by the data publisher; the resulting clinical associations remain **provisional**.

The 2020 specialty matrix was extracted from a published PDF. Relevant hospital-to-specialty alignment and whether the CHADS measure is appropriately attributable to cardiology need explicit verification before treating the specialty result as validated.

## Project tools

SQL Server / T-SQL (source database), Python, pandas, NumPy, SciPy, Matplotlib, Jupyter, and presentation design. The shareable review notebook uses the exported CSVs; SQL transformations are **not represented as reproducible scripts** in this repository.

## Sources

- [OECD — Medical graduates](https://www.oecd.org/en/data/indicators/medical-graduates.html)
- [OECD — Medical Education and Training in Israel](https://www.oecd.org/content/dam/oecd/en/publications/reports/2023/05/medical-education-and-training-in-israel_5355b9bf/4125e770-en.pdf)
- [Israel Ministry of Health — resident specialty composition, 2020 (report PDF)](https://www.gov.il/BlobFolder/reports/shifts-reduction-joint-team-intermediate-conclusions-report/he/files_committees_shifts-reduction_shifts-reduction-joint-team-Intermediate-Conclusions-Report.pdf)
- [WHO — Quality health services](https://www.who.int/news-room/fact-sheets/detail/quality-health-services)
- World Bank population and Ministry of Health hospital-process datasets (see original notebook).

**Author:** Yaniv Simha · **Use:** Exploratory analysis and learning portfolio. Consult original data-provider terms before redistribution.
