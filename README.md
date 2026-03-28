🚀 End-to-End Data Engineering Project on Azure
📌 Project Overview
This project demonstrates a complete end-to-end data engineering pipeline using Azure services. It covers data ingestion, transformation, storage, and visualization using a scalable architecture.

The project includes:

Data migration (Blob → SQL, Blob → Blob, GitHub → Blob)
Incremental data loading
Data transformation using Data Flows & Databricks
Medallion Architecture (Bronze, Silver, Gold)
Business insights using Power BI dashboards
🏗️ Architecture
Azure SQL (OLTP)
        ↓
Azure Data Factory (ADF)
        ↓
Azure Data Lake Gen2 (Bronze Layer)
        ↓
Azure Databricks (Transformation)
        ↓
Silver → Gold Layer (Delta Tables)
        ↓
Power BI Dashboard
⚙️ Technologies Used
Azure Data Factory (ADF)
Azure Blob Storage
Azure Data Lake Storage Gen2 (ADLS)
Azure SQL Database
Azure Databricks
Power BI
GitHub API
CSV / Parquet Data Formats
📂 Project Components
🔹 1. Blob to Azure SQL (Incremental Load)
Source: CSV files in Blob Storage
Target: Azure SQL Database
Tool: ADF Copy Activity

Key Features:

Incremental load using Upsert
Primary Key:
StudentID
FacultyID
Pipelines:
StudentPipeline
FacultyPipeline
🔹 2. Blob to Blob (Data Transformation)
Input: Multiple files (Customers, Products, Orders)
Output: Single transformed file

Transformations:

Filter (Incremental load using watermark)
Join (Customers + Orders)
Aggregate (Remove duplicates in Products)

Derived Column:

TotalAmount = Quantity * Price

Pipeline:

BlobToBlob

Key Concept:

Watermark-based incremental processing
🔹 3. GitHub to Blob
Fetch data from GitHub repository using API

Pipeline Components:

Web Activity (GET request)
ForEach (iterate files)
Copy Activity (store in Blob)

Pipeline Name:

GitHubPipeline
🔹 4. Azure SQL to Data Lake (Medallion Architecture)
📥 Bronze Layer
Raw data ingestion from Azure SQL
Stored in Parquet format
🔄 Silver Layer
Data cleaning & transformation using Databricks
🥇 Gold Layer
Business-ready dataset (gold_analytics)
📊 Power BI Dashboard
🔹 KPIs
Total Revenue
Total Appointments
Completed Appointments
Average Consultation Fee
🔹 Visualizations
Monthly Revenue Trend
Revenue by Specialization
Revenue by City
Top Doctors Performance
Appointment Status (Completed vs Cancelled)
🔹 Sample DAX Queries
Total Revenue = SUM(gold_analytics[consultation_fee])

Total Appointments = COUNT(gold_analytics[appointment_id])

Completed Appointments =
CALCULATE(
    COUNT(gold_analytics[appointment_id]),
    gold_analytics[status] = "Completed"
)

Avg Consultation Fee =
AVERAGE(gold_analytics[consultation_fee])
📦 Storage Structure
Blob Storage:
│
├── studentdata/
├── facultydata/
├── inputcontainer/
├── outputcontainer/
└── controlcontainer/ (watermark)

ADLS Gen2:
│
└── healthcare/
    ├── bronze/
    ├── silver/
    └── gold/
🔄 Incremental Load Strategy
Used Upsert in ADF for SQL loads
Used Watermark file for Blob processing

Filters applied:

OrderDate > lastProcessedDate
▶️ How to Run the Project
Create Azure resources:
Resource Group
Storage Account
Azure SQL Database
Data Factory
Databricks
Upload sample CSV files to Blob Storage
Create datasets & linked services in ADF
Run pipelines:
Blob → SQL
Blob → Blob
GitHub → Blob
Execute Databricks notebooks for transformations
Connect Power BI to Gold Layer
🎯 Objective

To build a scalable healthcare data platform that:

Ingests transactional data
Stores raw and processed data efficiently
Transforms data using modern architecture
Provides actionable insights through dashboards
📈 Key Learnings
End-to-end data pipeline design
Incremental data loading strategies
Data transformation using ADF & Databricks
Medallion Architecture implementation
Real-time analytics using Power BI
