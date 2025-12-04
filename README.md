**ETL Sales Pipeline on Databricks (Bronze → Silver → Gold)
**

A fully automated ETL pipeline built on Databricks Serverless + Unity Catalog, implementing the Medallion Architecture to process retail sales data and generate analytics-ready tables.

This project is designed for Data Engineering + Analytics portfolio use and follows real-world production standards.

**Architecture Overview**

flowchart LR

A[Raw Dataset (Uploaded to Databricks)] --> B[Bronze Layer \n Clean Column Names]
B --> C[Silver Layer \n Data Cleaning, Validation, Type Casting, Calculated Fields]
C --> D[Gold Layer \n Aggregations & BI Tables]

D --> E1[Daily Revenue Dashboard]
D --> E2[Top Products Dashboard]
D --> E3[Customer Value Dashboard]


**⭐ Features**
🔹 Bronze Layer (Raw Standardized)

Cleaned column names

Loaded from Databricks workspace dataset

Stored as Managed Delta table

Zero business logic; raw preservation

🔹 Silver Layer (Cleaned + Validated)

Detects missing/incorrect field names dynamically

Casts data types (int/double/date/string)

Recalculates totals

Flags mismatches & bad rows

Adds audit columns (ingested_at, etl_batch_id, year, month)

🔹 Gold Layer (Analytics Layer)

Daily revenue table

Top-selling products

Customer lifetime value (LTV) table

Used for BI dashboards in Power BI / QuickSight

**🧩 Technologies Used**
Layer	Technology
Compute	Databricks Serverless
Storage	Unity Catalog Managed Delta Tables
Transformation	PySpark, Spark SQL
Workflow	Databricks Jobs
Version Control	GitHub + Databricks GitHub App
BI	Power BI / QuickSight
📁 Repository Structure
etl-sales-pipeline-databricks/
│── notebooks/
│   ├── 01_bronze_ingest.ipynb
│   ├── 02_silver_cleaning.ipynb
│   └── 03_gold_analytics.ipynb
│
│── docs/
│   ├── architecture.md
│   └── data_model.md
│
│── jobs/
│   └── databricks_job.json
│
└── README.md

**📝 ETL Pipeline Summary**
Bronze

Input: workspace.default.retail_sales_dataset

Cleans column names

Saves to: etl_demo.bronze_retail_sales

Silver

Detects columns automatically (regex-based)

Cleans and standardizes schema

Recomputes totals

Adds audit metadata

Saves to: etl_demo.silver_retail_sales

Gold

Daily Revenue → etl_demo.gold_daily_revenue

Top Products → etl_demo.gold_top_products

Customer Value → etl_demo.gold_customer_value

📊 BI Dashboards (Power BI / QuickSight)

Use the Gold Layer tables:

1. Daily Revenue Dashboard

Metrics:

Revenue (with/without tax)

Number of orders

Trend by day, month, year

2. Top Products Dashboard

Metrics:

Quantity sold

Revenue

Order counts

Top 10 products

3. Customer Value Dashboard

Metrics:

Total spent

Avg order value

Orders per customer

High-value customers

****🏁 How to Run the Pipeline****
Option A — Manual

Run 01_bronze_ingest

Run 02_silver_cleaning

Run 03_gold_analytics

Option B — Automated using Databricks Jobs

Pipeline order:

bronze_ingest → silver_cleaning → gold_analytics

**🧠 2. Architecture Explanation**
Bronze Layer

Purpose: Store raw data with minimal transformation

Guarantees reproducibility and auditability

Only column name cleaning is applied

Silver Layer

Main data quality layer

Detects and maps varying column names

Recalculates derived metrics

Fixes incorrect totals

Adds ETL metadata

Provides a business-ready clean table

Gold Layer

Final reporting layer

Optimized for analytics

Used directly by BI tools

Pre-aggregated for performance
