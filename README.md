# Crime Data Pipeline and Reporting Dataset

## Project overview

This project prepares a BI-ready reporting dataset for four selected police forces using UK Police street-level crime data and public enrichment datasets. The notebook follows the pipeline layers specified in the project brief: ingestion, cleaning and validation, feature engineering and transformation, aggregation for reporting, and export.

## GitHub repository
https://github.com/FBackhouse1/Rockborne_CrimeDataAggregation

## Current notebook

Main notebook:

```text
FennerBackhouse_Proj5_CrimeData.ipynb
```

Final exported reporting dataset from the notebook:

```text
Data/AggregateCrimeDatasetReport.csv
```

## Selected police forces

The pipeline processes four Police.uk force downloads:

- Cleveland
- West Yorkshire
- North Yorkshire
- Wiltshire

The project date range is April 2023 to March 2026, giving 36 reporting months.

## Source datasets

### Primary dataset

UK Police street-level crime data, downloaded by month and police force.
https://data.police.uk/data/

### Enrichment datasets

1. ONS police force area population estimates, used to calculate normalised crime rates per 1,000 residents.
https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/adhocs/3194populationestimatesforpoliceforceareasinenglandandwalesbysingleyearofageandsexmid1991tomid2024
2. Index of Multiple Deprivation data at LSOA level, joined to crime records using LSOA code to add socioeconomic context.
https://www.gov.uk/csv-preview/691ded56d140bbbaa59a2a7d/File_7_IoD2025_All_Ranks_Scores_Deciles_Population_Denominators.csv

## Final reporting grain

The final dataset is aggregated to:

```text
police_force_code x police_force_name x year_month x season x crime_type
```

This supports monthly force-level comparison by crime category, with seasonal attributes and enrichment measures.

## Final dataset shape from the executed notebook

The latest notebook validation summary reported:

- Raw crime rows ingested: 1,541,355
- Rows after cleaning: 1,482,730
- Final reporting rows: 2,016
- Police forces: 4
- Months: 36
- Crime categories: 14
- Duplicate rows at final reporting grain: 0
- Missing required final values: 0

## Important assumptions

- Rows with missing `crime_id` are retained because all missing `crime_id` values were Anti-social behaviour records. Removing these records would remove 153,030 valid incidents, equal to 10.32 percent of the cleaned crime dataset.
- Exact duplicate rows are removed during crime cleaning.
- IMD enrichment is joined at LSOA level. Records without matched IMD data are retained in crime counts and counted in `missing_imd_count`.
- Population is annual, while crime data is monthly. Annual population is applied to each month in the same calendar year.
- The population file contains estimates up to 2024. The 2024 estimate is used as the latest available population denominator for 2025 and 2026.

## Output files in this documentation pack

- `FennerBackhouse_Proj5_CrimeData.ipynb`: jupyter notebook file containing pipeline
- `AggregateCrimeDatasetReport.csv`: final reporting CSV crime dataset
- `README.md`: project overview and run notes.
- `Statement_of_Work.docx`: formal statement of work.
- `Data_Dictionary.csv`: data dictionary for the final reporting dataset.
- `Workflow_Diagram.png`: visual workflow diagram.

## How to run

1. Ensure the input data folders and enrichment files match the paths defined in the notebook setup section.
2. Open and run `FennerBackhouse_Proj5_CrimeData.ipynb` from top to bottom.
3. Review the validation outputs in the Export Layer.
4. Use `Data/AggregateCrimeDatasetReport.csv` as the Power BI reporting dataset.
