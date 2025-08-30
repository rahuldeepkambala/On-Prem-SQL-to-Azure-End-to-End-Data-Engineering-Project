# 🏗️ On-Prem SQL to Azure – Data Engineering Project

This project demonstrates how to modernize an on-premises SQL Server data platform by migrating it to Azure, enabling scalable analytics, cost optimization, and advanced business insights. The implementation follows the **Medallion Architecture (Bronze → Silver → Gold)** and showcases modern end-to-end data engineering practices.

---

## 🎯 Business Goal

The goal of this project is to move the existing on-premises SQL Server platform to Azure, enabling a scalable, reliable, and cost-efficient data environment. By doing this, businesses gain faster access to analytics-ready data, reduce operational costs, and support advanced reporting and business intelligence.

**Key Objectives:**

- 📥 **Reliable Data Ingestion** – Automate extraction of data from on-prem SQL Server into Azure Data Lake.
- ⏳ **Incremental Loading** – Capture only changed records to reduce compute costs and improve performance.
- ⚡ **Data Transformation** – Standardize, cleanse, and enrich raw data using Databricks for analytics-ready datasets.
- 📊 **Business Insights** – Deliver clean, aggregated data for dashboards in Power BI.
- 🔔 **Operational Monitoring** – Track pipeline health with automated alerts on failures or successes.
- 🚀 **CI/CD Deployment** – Enable repeatable deployments using Azure DevOps and GitHub version control.

---

## 🏗️ Architecture & Tech Stack

**Architecture Diagram:**  

![On-Prem SQL to Azure Architecture](https://github.com/user-attachments/assets/32e4e1eb-d892-44d1-83bc-a6c922db6487)  
*Logo placeholder: Add company or Azure logo at top-left for branding.*

**Architecture Flow:**  

1. **Ingestion Layer (Bronze)** – Raw data is ingested from on-prem SQL Server into **Azure Data Lake Storage (ADLS)** using Azure Data Factory.
2. **Transformation Layer (Silver)** – Databricks notebooks clean, standardize, and enrich the data.
3. **Aggregation Layer (Gold)** – Databricks creates curated Delta Tables optimized for reporting and analytics.
4. **Consumption Layer** – Power BI dashboards visualize curated datasets for business users.
5. **Monitoring & Deployment** – Logic Apps send alerts on pipeline health; Azure DevOps manages CI/CD.

**Tools & Services Used:**

| Layer/Function | Tool/Service |
|----------------|--------------|
| Data Ingestion | Azure Data Factory (ForEach, If Condition, Incremental Loads) |
| Storage | Azure Data Lake Storage (Bronze/Silver/Gold) |
| Processing | Azure Databricks (PySpark transformations) |
| Data Format | Delta Lake (partitioning, schema evolution, time travel) |
| Monitoring | Logic Apps (email notifications on pipeline success/failure) |
| CI/CD | Azure DevOps + GitHub (ARM template deployments) |
| Visualization | Power BI |

---

## 🔄 Step-by-Step Implementation

### 1️⃣ Data Ingestion (Bronze Layer)

```python
# ADF pipeline pseudo-code for metadata-driven ingestion
for table in table_list:
    if table.has_last_modified:
        incremental_load(table)
    else:
        full_load(table)
