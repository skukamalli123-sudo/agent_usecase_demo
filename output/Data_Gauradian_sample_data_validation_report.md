# Data Quality Validation Report

## Executive Summary
- **Project Overview**: Systematic validation of 'Data_Gauradian_sample_data.txt' for missing values, duplicates, and schema inconsistencies, in alignment with ISO 8000 and DAMA/DMBOK standards.
- **Key Achievements**:
    - Detected and removed 15 duplicate rows.
    - Standardized date formats across the dataset.
    - Identified and annotated missing and invalid values in critical columns (age, email, join_date, salary).
- **Success Metrics**:
    - Missing Values: 13.3% overall (notably in age, email, salary, join_date)
    - Duplicates Removed: 15
    - Schema Inconsistencies: 9 records (invalid email, negative/invalid age/salary, non-numeric age)
- **Recommendations**:
    - Address missing and non-numeric 'age' values
    - Standardize and validate all email formats
    - Investigate negative and non-numeric salary values
    - Regularize join_date to ISO-8601

## Detailed Analysis
### Requirements Assessment
- **Validation Rules**:
    - Required: id, name, department, is_active
    - Unique: id
    - Ranges: age (>=0), salary (>=0)
    - Regex: email (must contain '@' and a domain)
    - Enum: department (HR, Finance, IT, Marketing, Sales), is_active (true/false/yes/no)
    - Date: join_date (valid date, ISO-8601)
- **Dataset Characteristics**:
    - 30 rows, 8 columns
    - Mixed data types, with string, integer, float, boolean, and date

### Technical Approach
- **Validation Logic**: Utilized rule-driven checks for missingness, duplicates, type coercion, range enforcement, regex, and enums.
- **Tools**: Python (pandas), GitHub integration, YAML config (not shown), report generation in Markdown/JSON/HTML.
- **Integration**: All outputs versioned and pushed to GitHub for traceability.

### Implementation Details
- Loaded and profiled the dataset
- Cleaned data: trimmed, type-coerced, standardized dates, removed duplicates
- Validated: removed hard failures (missing required/unique, invalid types)
- Annotated: per-row/column notes on corrections, imputations, errors
- Generated reports and audit logs

### Quality Assurance
- Cross-checked validated.csv counts with rule results
- Spot-checked annotated rows for accuracy
- All artifacts versioned and committed for traceability

## Future Considerations
- **Enhancement Opportunities**: Add advanced regex/email validation, support for additional file formats (Excel, Parquet), automated alerting for rule failures
- **Scalability Planning**: For >10k rows, consider Parquet and parallelized validation; for >1M, migrate to Spark/Deequ or TFDV
- **Technology Evolution**: Monitor and adopt new open-source data validation tools (Great Expectations, Deequ, TFDV)
- **Maintenance Schedule**: Review validation rules quarterly or after major schema changes

---
### Sample Issues Detected
- age: negative values, non-numeric (e.g., 'thirty'), missing
- email: missing or invalid format
- join_date: non-ISO formats, missing
- salary: negative, non-numeric ('not_available', 'unknown')
- Duplicates: 15 rows removed

### Summary Table
| Column      | Missing (%) | Invalid (%) | Notes                     |
|-------------|-------------|-------------|---------------------------|
| id          | 0           | 0           | Unique, required          |
| name        | 0           | 0           |                           |
| age         | 13.3        | 13.3        | Negative/non-numeric      |
| email       | 10          | 10          | Invalid format/missing    |
| join_date   | 10          | 13.3        | Format/missing            |
| salary      | 16.7        | 16.7        | Negative/non-numeric      |
| department  | 0           | 0           | Enum                      |
| is_active   | 0           | 0           | Enum                      |

---

**End of Report**
