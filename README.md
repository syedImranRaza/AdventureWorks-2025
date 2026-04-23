# AdventureWorks-2025
AdventureWorks 2025 — End-to-End BI Solution using Microsoft Fabric

🧠 PROJECT OVERVIEW

This project demonstrates a complete Business Intelligence solution using modern data architecture with Microsoft Fabric and Power BI Desktop.

The goal is to transform raw transactional data into an executive-level dashboard providing actionable insights.

🏗️ ARCHITECTURE
SQL Server
   ↓
Dataflow Gen2 (Cleaning)
   ↓
Lakehouse (Bronze/Silver)
   ↓
Warehouse (Gold - Star Schema)
   ↓
Semantic Model (Direct Lake)
   ↓
Power BI Dashboard

🔄 DATA PIPELINE
1. Data Source
AdventureWorks 2025 database hosted on SQL Server
2. Data Ingestion (Dataflow Gen2)
Connected SQL Server to Fabric
Imported tables into Lakehouse
Performed:
Data cleaning
Duplicate removal
Column standardization
3. Data Transformation (Silver Layer)
Merged customer and person tables
Flattened product hierarchy
Created cleaned analytical tables
4. Data Modeling (Warehouse - Gold Layer)

Created Star Schema:
Fact Table:
FactSales
Dimension Tables:
DimCustomer
DimProduct
DimDate
DimTerritory

📊 SEMANTIC MODEL
Built using Direct Lake (OneLake)
Defined relationships (1:M)
Optimized for performance
Measures created using DAX


📈 KEY MEASURES

Examples:

Total Sales = SUMX(FactSales, FactSales[UnitPrice] * FactSales[OrderQty])

Total Orders = DISTINCTCOUNT(FactSales[SalesOrderID])

Avg Order Value = DIVIDE([Total Sales], [Total Orders])

YoY Growth % =
DIVIDE(
    [Total Sales] - CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DimDate[Date])),
    CALCULATE([Total Sales], SAMEPERIODLASTYEAR(DimDate[Date]))
)

👥 CUSTOMER SEGMENTATION
Dynamic segmentation using DAX:

High Value (> 50K)
Medium Value (> 20K)
Low Value (< 20K)

📊 DASHBOARD FEATURES
Page 1 — Executive Summary
KPI Cards (Sales, Orders, Quantity, AOV)
Monthly Sales Trend
YoY Growth Analysis
Sales by Category
Sales by Country
Top Customers Table

🎯 KEY INSIGHTS
Identified top-performing regions (US leading revenue)
Detected seasonal sales trends
Highlighted high-value customer concentration
Revealed product category contribution

🔐 SECURITY
Row-Level Security (RLS) implemented
Column-level restrictions applied where necessary

⚡ PERFORMANCE OPTIMIZATION
Used Direct Lake for real-time analytics
Avoided unnecessary calculated columns
Centralized measures in semantic model

🚀 LEARNINGS
Importance of layered architecture (Bronze → Silver → Gold)
Efficient modeling in Fabric Warehouse
Benefits of Direct Lake vs Import mode
Designing executive-friendly dashboards
