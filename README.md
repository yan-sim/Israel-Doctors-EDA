# Israel-Doctors-EDA
Exploratory Data Analysis of Physician Workforce and Medical Training in Israel

## Project files

- [SQL Server database backup](Israel_Doctors_EDA.bak)
- [Original Cursor project archive, version 22](Experis_Israel_Doctors_Cursor_Project_v22.zip)
- [Analysis notebook](analysis/Israel_Doctors_EDA_Exploration_22.ipynb), with saved results
- [Hebrew project documentation](analysis/README_HE.md)
- [Source datasets](analysis/data), [CSV exports](analysis/exports), and [charts](analysis/charts)

## Run the analysis

Requires Python 3 and a Jupyter-compatible editor such as Cursor or VS Code.

```sh
cd analysis
python -m pip install -r requirements.txt
```

Open `Israel_Doctors_EDA_Exploration_22.ipynb`, select the Python environment, and run the cells in order with `analysis/` as the working directory. Saved outputs can be viewed without executing the notebook. Ministry of Health CSV files use Windows Hebrew (`cp1255`); the notebook handles this encoding.

The notebook reads the bundled CSV files directly; restoring the database is optional. To use the BAK, restore it with SQL Server Management Studio to a new database, adjusting file paths for your SQL Server instance. Do not overwrite an existing database.

## Scope and interpretation

The project explores physician workforce and training indicators, OECD comparisons, Israeli hospital training composition, and selected hospital quality measures. Source references are included in the notebook and data files, including OECD, Ministry of Health publications and open data, and World Bank population data.

Quality results labelled `PROVISIONAL` depend on unverified interpretations of missing numerators and case stratification. Comparisons and correlations are descriptive, do not establish causation, and do not measure the quality of individual physicians or graduates. Benchmark-equivalent physician counts are not normative estimates of a physician shortage. See the notebook's sensitivity analyses, limitations, and outstanding validation tasks before using the findings.

## Publication notes

The original ZIP and BAK are preserved byte-for-byte under simplified filenames. The extracted analysis is supplied for convenient browsing. The archive's original Hebrew documentation is retained, with opening instructions corrected to version 22 in the extracted copy.

The text and notebook files in the ZIP were scanned for common credential patterns, with no matches found; this is a limited check. **The database backup was published without inspecting its contents at the owner's explicit request.** The notebook's saved outputs contained no recorded execution errors; a full rerun and SQL restore have not been performed.

No additional license or redistribution rights are asserted for third-party datasets; consult their original providers' terms.

## Missing numerator validation (25 October 2026)

Notebook section **5.2.1** now compares blank approved-case counts against the independently recorded hip-fracture operation time. Of 1,470 source records with blank numerators, 1,355 have time greater than 48 hours; the remaining 115 are exactly at the recorded 48-hour boundary. All records above 48 hours have blank numerators; none below 48 hours do. These are source-record counts, not patient counts, and the rounded boundary is kept separate.

- [Presentation chart (PNG)](analysis/charts/quality_hip_missing_numerator_vs_time.png)
- [Vector chart (SVG)](analysis/charts/quality_hip_missing_numerator_vs_time.svg)
- [Audit counts, including case-weighted totals](analysis/exports/MOH_Hip_Blank_Numerator_Time_Audit.csv)

The added cell was executed and its actual output embedded. Other notebook cells were not rerun. Existing clinical results remain exploratory; validating source strata and specialty extraction is a separate task. The original downloadable ZIP remains the unchanged version-22 archive; use the notebook under `analysis/` for this update.
