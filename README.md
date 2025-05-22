# 🚖 NYC Green Taxi Trip Analysis with Azure Data Platform

This project is designed to ingest, transform, and analyze New York City Green Taxi trip data using Azure Data Factory (ADF), Azure Data Lake Storage (ADLS), Azure Databricks, and Power BI. The pipeline follows a Medallion Architecture (Bronze, Silver, Gold) to ensure scalability, reliability, and structured data transformation.

---

## 📁 Project Architecture

![Project Architecture](https://github.com/Nareshmaila7/NYC-TAXI-DataEngineer-Project/blob/17d238c007f0377a66111b1069d68c10083a57f1/Project%20Architecture.png)

**Medallion Architecture Layers:**

- **Bronze Layer:** Raw data directly ingested from the NYC Taxi dataset REST API.
- **Silver Layer:** Cleaned and transformed data for analysis.
- **Gold Layer:** Final aggregated data in Delta format used for reporting in Power BI.

---

## ⚙️ Tech Stack

- **Azure Data Factory**: For orchestrating and automating data ingestion workflows.
- **Azure Data Lake Storage Gen2 (ADLS)**: For storing raw and transformed data.
- **Azure Databricks**: For scalable data processing and transformation using Spark and Delta Lake.
- **Power BI**: For interactive data visualization and reporting.
- **Service Principal Authentication**: For secure access between ADF and Databricks.

---

## 🔄 Data Flow

1. **Data Source**  
   Monthly green taxi trip records (January to December) are fetched dynamically from a public NYC REST API.

2. **Bronze Layer (ADF)**  
   - A **ForEach activity** in ADF loops through 12 monthly datasets.
   - Inside ForEach, a **Copy Activity** uses dynamic parameters to fetch and load data into the Bronze container in ADLS.

3. **Silver Layer (Databricks)**  
   - Databricks reads the raw Parquet files from the Bronze layer.
   - Basic cleaning and transformation are applied.
   - Transformed data is written back to the Silver container.

4. **Gold Layer (Databricks + Delta Lake)**  
   - Further transformations are applied.
   - Data is saved in **Delta format** in the Gold container.
   - Delta tables are created for reporting.

5. **Reporting (Power BI)**  
   - Power BI connects to Delta tables for interactive dashboards and visualizations.

---

## 🧱 Components

### Azure Data Factory (ADF)
- **Pipeline** with ForEach + Copy activities
- **Parameterization** for dynamic REST API calls
- Linked Services and Datasets configured for REST, ADLS

### Azure Data Lake Storage (ADLS)
- `bronze/`, `silver/`, and `gold/` containers for Medallion architecture

### Azure Databricks
- Notebooks for:
  - Reading/writing Parquet from/to ADLS
  - Data cleaning and transformation
  - Writing data as Delta format

### Power BI
- Connected to Databricks SQL/Delta tables
- Built visual reports and dashboards
