# 🚗 Car Shop Data Engineering Project [ODS → Staging → DWH(Analytics)]

 
**End-to-End Retail Data Pipeline using Azure SQL, SSIS, SSAS, and Power BI**

> A full-stack business intelligence and data engineering project that demonstrates building a complete analytics pipeline from raw data to insightful dashboards using Microsoft technologies.

---

## 📌 Project Overview

This project simulates a real-world data pipeline for a Car Shop business. It follows a structured **ETL + Semantic Modeling + Visualization** approach using:

- **Azure SQL Database** (source)
- **SSIS** for ETL across ODS → Staging → DWH
- **SQL server Database** (destination)
- **SSAS Tabular** for the semantic model
- **Power BI** for reporting and dashboards

---

## 🏗️ Architecture

```mermaid
graph TD
A[Azure SQL Source] --> B[ODS (Initial + Incremental Load)]
B --> C[Staging (Cleaned, Transformed)]
C --> D[Data Warehouse (Dim/Fact)]
D --> E[SSAS Semantic Layer]
E --> F[Power BI Dashboard]
```

---

## 🔄 ETL Workflow (SSIS)

### ✅ 1. ODS Layer (Operational Data Store)
- Loaded raw tables as-is:
  - `Brands`, `Categories`, `Customers`, `Order_Items`, `Orders`, `Products`, `Staff`, `Stocks`, `Stores`, `Date`
- Used **SSIS packages** for initial 
<img src="https://github.com/mohamedabodonia/-Car-Shop-Data-Engineering-Project-ODS-Staging-DWH-Analytics-/blob/main/SSIS%20Package/ODS%20initital%20load.jpeg?raw=true">

**incremental loading**
- No transformations applied—just raw replication for audit and backup
- <img src="https://github.com/mohamedabodonia/-Car-Shop-Data-Engineering-Project-ODS-Staging-DWH-Analytics-/blob/main/SSIS%20Package/incremental%20Load%20using%20Sql.jpeg?raw=true">

- <img src="https://github.com/mohamedabodonia/-Car-Shop-Data-Engineering-Project-ODS-Staging-DWH-Analytics-/blob/main/SSIS%20Package/ODS%20incremental%20Load.jpeg?raw=true">

### ✅ 2. Staging Layer
- Performed light transformations In Initial Load:
  - Trimmed all string columns
  - Replaced null values
 
-   <img src="https://github.com/mohamedabodonia/-Car-Shop-Data-Engineering-Project-ODS-Staging-DWH-Analytics-/blob/main/SSIS%20Package/Transformation%20in%20Staging.jpeg?raw=true">
    
- **Incremental load** from ODS to staging using date/time keys
- Staging DB acts as a clean, shaped layer before modeling

-   <img src="https://github.com/mohamedabodonia/-Car-Shop-Data-Engineering-Project-ODS-Staging-DWH-Analytics-/blob/main/SSIS%20Package/Staging%20Incremental%20Load.jpeg?raw=true">

### ✅ 3. Data Warehouse Layer
- Designed a **star schema** with dimension and fact tables
- Created **surrogate keys**
- Merged related entities where applicable (e.g., Orders + Order_Items)
- Implemented **incremental load** into the DWH from staging

---

## 📐 SSAS Tabular Model (Semantic Layer)

Built a semantic model using **SQL Server Analysis Services (SSAS Tabular)**:

- Defined relationships between tables
- Created **calculated columns**:
  - `Net Sales`, `Total Discounts`, `Manager Name`
- Developed **measures**:
  - `Order Count`, `Out-of-Stock Items`, `Late Shipments`, `Repeat Customer Rate`

---

## 📊 Power BI Dashboard

Connected Power BI directly to the **live SSAS Tabular model**:

- **Landing Page + Main Dashboard** with buttons/bookmarks for navigation
- **Slicers**: Date Hierarchy, Brand, Store, Category
- **KPIs & Visuals**:
  - Net Sales Over Time
  - Order Trends
  - Sales by Staff/Manager
  - Out-of-Stock Analysis
  - Repeat Customer Performance

---

## 🔁 Incremental Load Strategy

Implemented **incremental data loading** across all layers:

- ✅ **ODS**: Filtered by last modified timestamp or audit column  
- ✅ **Staging**: Only new/changed records processed  
- ✅ **DWH**: Lookup with surrogate keys for delta updates  

This reduces load time and ensures scalability for larger datasets.

---

## 🧰 Tech Stack

| Layer | Tool/Technology |
|-------|-----------------|
| Source | Azure SQL Database |
| ETL | SQL Server Integration Services (SSIS) |
| Semantic | SQL Server Analysis Services (SSAS Tabular) |
| Reporting | Power BI |
| Language | T-SQL, DAX |

---

## 📁 Suggested Folder Structure

```
📦 Car-Shop-BI-Project
├── 📂 SSIS_Packages
├── 📂 SQL_Scripts
├── 📂 SSAS_Model
├── 📂 PowerBI_Reports
└── README.md
```
