# Rural Climate and Population Data Integration

An Excel-based data engineering project that expanded and standardized a village-level panel dataset for research on extreme temperature and rural population mobility in China.

## Project overview

The analytical challenge was not regression modeling. It was building a reliable research-ready panel from records collected in different years and stored across multiple sources.

The workflow covered:

1. Reviewing the existing village-level data structure and variable dictionary.
2. Appending earlier-year observations to the master workbook.
3. Constructing a consistent `year-province-village` record key.
4. Matching geographic attributes through multi-condition Excel lookups.
5. Standardizing 120 columns covering geography, migration, labor, income, land, infrastructure, climate, and emissions.
6. Checking unmatched records, missing values, identifiers, and year coverage before downstream analysis.

## Scale of work

| Metric | Result |
|---|---:|
| Original data rows | 1,747 |
| Rows appended and integrated | 1,539 |
| Final panel rows | 3,286 |
| Variables retained | 120 |
| Years represented | 2009-2017 |

The workbook contained 3 header rows, so the final worksheet extended through row 3,289.

## Data sources

- China Rural Fixed Observation Point survey data
- NOAA Global Historical Climatology Network station reference data
- Derived extreme-temperature measures
- Geographic and administrative matching fields

The rural survey data are research-restricted and contain village names and coordinates. Raw records are therefore not published in this repository.

## Data architecture

The final table combined these domains:

- Geographic identity and coordinates
- Population migration and labor mobility
- Village income and enterprise activity
- Healthcare and public services
- Extreme-temperature indicators
- Carbon emissions
- Population, education, and employment structure
- Agricultural land and crop areas
- Land transfer and infrastructure

See [`documentation/data_dictionary.csv`](documentation/data_dictionary.csv) for a portfolio-level field map.

## Key Excel methods

- Composite record keys
- Multi-condition `XLOOKUP`
- Structured row appending
- Cross-year identifier reconciliation
- Missing-match flags
- Formula propagation and spot checks
- Year and row-count reconciliation

Representative matching logic is documented in [`code/excel_formula_reference.md`](code/excel_formula_reference.md).

## Quality controls

- Verified final record counts by year.
- Used province and village codes as stable matching fields.
- Kept an explicit unmatched result rather than silently filling uncertain records.
- Preserved the original 120-column schema during row expansion.
- Separated the original-data sheet from the expanded-data sheet for auditability.

## Repository structure

```text
code/
  excel_formula_reference.md
data/
  README.md
documentation/
  data_dictionary.csv
results/
  panel_coverage_summary.csv
reports/
  Rural_Climate_Data_Integration_Summary.pdf
README.md
```

## Author contribution

I participated in the data integration and cleaning stage of the research project. My work focused on appending historical observations, reconciling record identifiers, using Excel lookup formulas to populate geographic information, preserving the 120-variable schema, and preparing the combined village-year panel for subsequent analysis by the research team.

## Skills demonstrated

Excel, XLOOKUP, panel-data construction, multi-source integration, identifier management, geographic matching, missing-value review, quality control, and research data documentation.

## Limitations

- The raw survey data cannot be publicly redistributed.
- Geographic attributes reused across years assume village identifiers remained consistent.
- Ambiguous or unmatched identifiers require manual review.
- This repository documents the data-engineering stage and does not claim responsibility for the project's later Stata regressions.

