# Data Quality Report

## 1. Overview

This report summarises the data quality checks performed during the Silver transformation stage of the Banking Transaction and Fraud Analytics Platform.

The project processes two datasets:
- Berka Czech Bank dataset
- PaySim synthetic mobile money dataset

## 2. Data Volume

| Dataset | Records |
|---|---:|
| Account | 4,500 |
| Card | 892 |
| Client | 5,369 |
| Disposition | 5,369 |
| District | 77 |
| Loan | 682 |
| Orders | 6,471 |
| Transactions | 1,056,320 |
| Berka datasets combined | 1,079,680 |
| PaySim | 6,362,620 |
| Total | 7,442,300 |

## 3. Data Quality Checks

| Check | Result |
|---|---|
| Required field validation | Passed |
| PaySim business rule validation | Passed |
| Berka primary key duplicates | 0 |
| Duplicate PaySim rows | 0 |
| Berka referential integrity | Passed |
| PaySim fraud flag validation | Passed |
| Missing account dimension keys | 0 |
| Missing transaction date keys | 0 |

## 4. Data Handling

- Blank values were converted to NULL.
- Date fields were converted into appropriate date or timestamp formats.
- Numeric PaySim fields were converted to numeric data types.
- The client birth number was removed from Silver for privacy protection.
- District crime values marked with "?" were converted to NULL.
- Zero-value and negative-balance Berka transactions were retained because they were not confirmed as invalid.

## 5. Gold Layer Validation

The Gold layer contains seven tables.

| Gold table | Records |
|---|---:|
| dim_district | 77 |
| dim_customer | 5,369 |
| dim_account | 4,500 |
| dim_date | 2,191 |
| bridge_customer_account | 5,369 |
| fact_bank_transactions | 1,056,320 |
| fact_fraud_transactions | 6,362,620 |

All final Gold validation checks passed.

## 6. Fraud Dataset Summary

| Category | Records |
|---|---:|
| Total transactions | 6,362,620 |
| Fraudulent transactions | 8,213 |
| Non-fraudulent transactions | 6,354,407 |

The fraud rate is approximately 0.129%.

The PaySim dataset does not provide a source transaction ID. A SHA-256 hash generated from the source transaction fields was used as a technical identifier.

## 7. Conclusion

The Silver and Gold transformations completed their validation checks successfully. The resulting tables were saved in their respective Fabric Lakehouses and verified against expected record counts.