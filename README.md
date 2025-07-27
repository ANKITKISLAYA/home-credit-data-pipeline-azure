---

## Architecture: Medallion (Bronze → Silver → Gold)

### Bronze Layer – Raw Ingestion
- Ingested Kaggle CSVs to **ADLS Gen2** using ADF
- Stored in `/bronze/home_credit/`

### Silver Layer – Cleaned & Joined Data
- Cleaned with **Databricks Notebooks**
- Joined application, bureau, and previous application data
- Stored in `/silver/home_credit/`

### Gold Layer – Feature Aggregates
- Risk profile views (debt-to-income, credit utilization, etc.)
- Materialized as **external tables** in Synapse using Serverless SQL
- Stored in `/gold/applicant_risk_profiles/`

---

## Tech Stack

| Layer              | Tools Used                                                                 |
|-------------------|------------------------------------------------------------------------------|
| Orchestration      | Azure Data Factory (ADF)                                                   |
| Storage            | Azure Data Lake Storage Gen2 (ADLS)                                        |
| Compute            | Azure Databricks (PySpark), Synapse Serverless SQL                         |
| Visualization      | Power BI                                                                   |
| CI/CD              | GitHub Integration with ADF, manual folder structure                       |

---

## Key Features

### 1. **Applicant Risk Profile View**
One row per applicant with:
- Debt-to-Income Ratio
- Total Loan Amount
- Credit Utilization

Saved as: `gold.applicant_risk_profiles`

### 2. **Feature Insights View**
Aggregated view for Power BI dashboards:
- Avg loan/income by gender
- Default rate by education level
- Credit utilization histograms

Saved as: `gold.feature_insights`

---

## How to Reproduce

### Prerequisites
- Azure Subscription
- Databricks Workspace
- Azure Synapse Analytics
- GitHub Repository

