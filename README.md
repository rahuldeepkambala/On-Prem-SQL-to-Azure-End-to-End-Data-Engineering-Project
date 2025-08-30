
🏗️ On-Prem SQL to Azure Data Lake – End-to-End Data Engineering Project

The On-Prem SQL to Azure Pipeline is designed to migrate and process enterprise data from on-premises SQL Server into Azure Data Lake using modern data engineering practices. The project demonstrates expertise in hybrid data integration, incremental loading, and transformation with Azure services.

🎯 1️⃣ Business Goal

The goal of this project is to modernize the existing on-prem SQL data platform by moving it to Azure, enabling scalable analytics, cost optimization, and advanced business insights.

Key Objectives:

📥 Reliable Data Ingestion – Automate data loads from on-prem SQL to Azure Data Lake.
⏳ Incremental Loading – Efficiently capture only changed records to reduce costs and improve performance.
⚡ Data Transformation – Standardize and process data in Databricks for analytics.
📊 Business Insights – Provide clean, aggregated datasets for reporting in Power BI.
🔔 Operational Monitoring – Enable automated email alerts for pipeline health.
🚀 CI/CD Deployment – Manage deployments with Azure DevOps and GitHub integration.

🏗️ 2️⃣ Architecture & Tech Stack

Architecture Flow:

Ingestion Layer (Bronze) – On-prem SQL data ingested using ADF into ADLS raw zone.

Transformation Layer (Silver) – Databricks performs cleansing, standardization, and enrichment.

Aggregation Layer (Gold) – Databricks creates curated Delta Tables for BI consumption.

Consumption – Power BI dashboards built on Gold layer datasets.

Monitoring & Deployment – Logic Apps for alerts, Azure DevOps for CI/CD.

Tools & Services Used:

🔄 Data Ingestion: Azure Data Factory (ForEach, If Condition, Incremental Loads)

🗄️ Storage: Azure Data Lake Storage (Bronze/Silver/Gold)

🔥 Processing: Azure Databricks (PySpark transformations)

🗃️ Format: Delta Lake (partitioning, schema evolution, time travel)

🔔 Alerts: Logic Apps (email notifications on pipeline failure/success)

🚀 CI/CD: Azure DevOps + GitHub (ARM template deployments)

📊 Visualization: Power BI

🔄 3️⃣ Step-by-Step Implementation
Step 1: Data Ingestion (Bronze Layer)

Built a metadata-driven pipeline in ADF using ForEach and If Condition.

Full load for tables without LastModified column (e.g., DimAirport).

Incremental load for tables with LastModified column (e.g., DimFlight, DimPassenger).

Implemented HighWatermark logic for incremental processing.

Data stored in ADLS Bronze folder (/bronze/{TableName}/).

Step 2: Transformation (Silver Layer)

Used Databricks notebooks (PySpark) to clean and standardize data.

Handled nulls, standardized datetime formats, applied schema enforcement.

Saved transformed data in Parquet format in Silver zone.

Step 3: Data Aggregation (Gold Layer)

Created Delta Tables for business-ready datasets.

Implemented partitioning for performance.

Supported time travel for auditing historical data.

Step 4: Monitoring with Logic Apps

Configured Logic App workflows to trigger on ADF pipeline status.

Sent email alerts on success/failure to stakeholders.

Step 5: Deployment with Azure DevOps

Exported ADF ARM templates to adf_publish/ folder.

Used Azure DevOps pipeline for CI/CD deployment.

Version-controlled all assets in GitHub (ADF, Databricks notebooks, Logic Apps).

🛑 4️⃣ Challenges Faced & Solutions
⚠️ Challenge	✅ Solution
Duplicate activity names in ADF	Used dynamic names: FullLoad_@{item().TableName} / IncrementalLoad_@{item().TableName}
Misuse of @item()	Restricted usage to inside ForEach child activities only
Initial watermark handling	Defaulted to '1900-01-01 00:00:00.000' for first load
Query performance issues	Applied Delta Lake optimizations (partitioning, caching)
Cost management	Enabled Databricks cluster auto-termination + Parquet compression
Schema evolution	Used Delta Lake features to handle changes automatically
👨‍💻 5️⃣ Role & Contributions

🏗️ Designed and built the metadata-driven ingestion pipeline in ADF.

🔄 Implemented incremental loading using HighWatermark and LastModified column.

🔥 Transformed raw data into curated datasets using Databricks + PySpark.

🗃️ Optimized storage with Parquet and Delta Lake (partitioning, schema evolution).

🔔 Automated monitoring with Logic Apps email alerts.

🚀 Set up CI/CD with Azure DevOps and GitHub.

📊 Delivered insights through Power BI dashboards for business users.

🚀 6️⃣ Business Impact & Outcomes

✅ Reliable migration from on-prem SQL to Azure cloud platform.
✅ Faster queries (5x improvement) with Delta Lake optimizations.
✅ Reduced storage costs using Parquet compression.
✅ Scalable solution handling both batch and near real-time ingestion.
✅ Business users gained actionable insights via curated Power BI dashboards.
