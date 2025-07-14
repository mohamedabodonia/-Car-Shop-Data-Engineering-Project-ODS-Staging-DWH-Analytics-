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

The project follows a robust layered architecture using the Medallion approach (ODS → Staging → DWH), with incremental loads implemented at each layer.

1️⃣ ODS Layer (Operational Data Store)
Purpose: To ingest and store raw data from the source system as-is, without modifications.

Tables Loaded:
Brands, Categories, Customers, Order_Items, Orders, Products, Staff, Stocks, Stores, Date

Tool Used: SSIS (SQL Server Integration Services) for initial and incremental loads from Azure SQL Server.

2️⃣ Staging Layer
Purpose: To apply initial data transformations and ensure data quality.

Key Transformations:

Trimmed all string columns

Replaced null values with appropriate defaults

Result: Cleaned and standardized data ready for modeling

Tool Used: SSIS for transformation and incremental data loads into Staging DB

3️⃣ DWH Layer (Data Warehouse)
Purpose: To build analytical models using Fact and Dimension tables.

Key Actions:

Merged and transformed staging tables as needed

Created surrogate keys

Applied star schema modeling

Fact Table Example: Fact_Orders_item,Fact_Stock

Dimension Tables Examples: Dim_Products, Dim_Stores, Dim_Customers, Dim_Date, Dim_Staff

Tool Used: SSIS with incremental ETL for loading and managing dimensional data

4️⃣ Semantic Layer (SSAS Tabular Model)
Purpose: To create a semantic layer for analysis and visualization.

Key Features:

Created relationships between fact and dimension tables

Developed calculated columns like:

Net Sales, Total Discounts, Manager Name

Created measures like:

Order Count, Out-of-Stock Items, Late Shipments, Repeat Customer Rate

Tool Used: SQL Server Analysis Services (SSAS)

5️⃣ Visualization Layer (Power BI)
Purpose: To build dashboards and enable self-service analytics.

Connection Mode: Live connection to SSAS Tabular Model

Power BI Features:

📊 Landing Page + Main Dashboard

🔀 Navigation with buttons and bookmarks

🧩 Filters/Slicers: Date Hierarchy, Brand, Store, Category

📈 KPIs & Visuals: Net Sales, Order Trends, Sales by Staff/Manager



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
 **Data Modelling**
    <img src="https://github.com/mohamedabodonia/-Car-Shop-Data-Engineering-Project-ODS-Staging-DWH-Analytics-/blob/main/SSIS%20Package/Conceptual%20Modeling.jpeg?raw=true">

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
- **Cards**:
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

