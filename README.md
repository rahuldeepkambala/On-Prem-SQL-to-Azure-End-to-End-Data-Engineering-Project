# 🏗️ On-Prem SQL to Azure Data Engineering Project

This project demonstrates how to modernize an on-premises SQL Server data platform by migrating to Azure, enabling scalable analytics, cost optimization, and advanced business insights. It follows the **Medallion Architecture (Bronze → Silver → Gold)** and implements end-to-end data engineering practices.

---

## 🎯 Business Goal

The goal of this project is to modernize the existing on-prem SQL data platform by moving it to Azure, enabling scalable analytics, cost optimization, and advanced business insights.

### Key Objectives

- 📥 **Reliable Data Ingestion** – Automate data loads from on-prem SQL to Azure Data Lake.  
- ⏳ **Incremental Loading** – Efficiently capture only changed records to reduce costs and improve performance.  
- ⚡ **Data Transformation** – Standardize and process data in Databricks for analytics.  
- 📊 **Business Insights** – Provide clean, aggregated datasets for reporting in Power BI.  
- 🔔 **Operational Monitoring** – Enable automated email alerts for pipeline health.  
- 🚀 **CI/CD Deployment** – Manage deployments with Azure DevOps and GitHub integration.  

---

## 🏗️ Architecture & Tech Stack

![Architecture Diagram](https://github.com/user-attachments/assets/32e4e1eb-d892-44d1-83bc-a6c922db6487)  


**Architecture Flow:**  

- **Ingestion Layer (Bronze)** – On-prem SQL data ingested using ADF into ADLS raw zone.  
- **Transformation Layer (Silver)** – Databricks performs cleansing, standardization, and enrichment.  
- **Aggregation Layer (Gold)** – Databricks creates curated Delta Tables for BI consumption.  
- **Consumption** – Power BI dashboards built on Gold layer datasets.  
- **Monitoring & Deployment** – Logic Apps for alerts, Azure DevOps for CI/CD.

**Tools & Services Used:**  

- 🔄 Data Ingestion: Azure Data Factory (ForEach, If Condition, Incremental Loads)  
- 🗄️ Storage: Azure Data Lake Storage (Bronze/Silver/Gold)  
- 🔥 Processing: Azure Databricks (PySpark transformations)  
- 🗃️ Format: Delta Lake (partitioning, schema evolution, time travel)  
- 🔔 Alerts: Logic Apps (email notifications on pipeline failure/success)  
- 🚀 CI/CD: Azure DevOps + GitHub (ARM template deployments)  
- 📊 Visualization: Power BI  

---

## 🔄 Step-by-Step Implementation

### 1️⃣ Data Ingestion (Bronze Layer)

- Built a **metadata-driven pipeline** in ADF using `ForEach` and `If Condition`.  
- Full load for tables without `LastModified` column (e.g., `DimAirport`).  
- Incremental load for tables with `LastModified` column (e.g., `DimFlight`, `DimPassenger`).  
- Implemented **HighWatermark logic** for incremental processing.  
- Data stored in ADLS Bronze folder (`/bronze/{TableName}/`).  

### 2️⃣ Transformation (Silver Layer)

- Used Databricks notebooks (PySpark) to clean and standardize data.  
- Handled nulls, standardized datetime formats, applied schema enforcement.  
- Stored transformed data in **Parquet format** in the Silver zone.  

### 3️⃣ Data Aggregation (Gold Layer)

- Created Delta Tables for business-ready datasets.  
- Implemented partitioning for performance.  
- Supported **time travel** for auditing and history tracking.  

### 4️⃣ Monitoring with Logic Apps

- Configured Logic Apps to trigger on ADF pipeline success/failure.  
- Sent **email alerts** to stakeholders.  

### 5️⃣ Deployment with Azure DevOps

- Exported **ADF ARM templates** to `adf_publish/` folder.  
- Configured **Azure DevOps pipeline** for CI/CD deployment.  
- Version-controlled all assets in GitHub (ADF pipelines, Databricks notebooks, Logic Apps).  

---

## 🛑 Challenges & Solutions

| ⚠️ Challenge | ✅ Solution |
|--------------|------------|
| Duplicate activity names in ADF | Used dynamic names: `FullLoad_@{item().TableName}` / `IncrementalLoad_@{item().TableName}` |
| Misuse of `@item()` | Restricted usage inside ForEach child activities only |
| Initial watermark handling | Defaulted to `'1900-01-01 00:00:00.000'` for first load |
| Query performance issues | Applied Delta Lake optimizations (partitioning, caching) |
| Cost management | Enabled Databricks cluster auto-termination + Parquet compression |
| Schema evolution | Used Delta Lake features to handle schema changes automatically |

---

## 👨‍💻 Role & Contributions

- 🏗️ Designed and implemented the **end-to-end data pipeline** in Azure.  
- 🔄 Built **incremental + full load ingestion** logic using ADF.  
- 🔥 Performed data cleansing and standardization with PySpark in Databricks.  
- 🗃️ Optimized storage with Parquet and Delta Lake.  
- 🔔 Automated **pipeline health monitoring** with Logic Apps.  
- 🚀 Managed **CI/CD deployments** via Azure DevOps + GitHub.  
- 📊 Built **Power BI dashboards** for insights and business reporting.  

---

## 🚀 Business Outcomes

- ✅ **Reliable migration** from on-prem SQL to Azure cloud.  
- ✅ **5x faster queries** using Delta Lake optimizations.  
- ✅ **Reduced storage costs** with Parquet compression.  
- ✅ **Automated monitoring** with alerts for quick issue detection.  
- ✅ **Scalable solution** supporting batch + incremental processing.  
- ✅ **Actionable insights** delivered through Power BI dashboards.  
