# CarePlus – AWS End-to-End Data Engineering Project

## 📌 Project Overview
CarePlus is an imaginary BPO company that handles customer care operations for multiple clients. The company previously relied on multiple databases and separate dashboards, resulting in fragmented insights and operational inefficiencies.

This project solves these challenges by designing and implementing a fully automated AWS-based ETL pipeline that consolidates structured and unstructured data into a single source of truth, enabling unified reporting for ticket analytics and system log performance insights.

---

## 🎯 Problem Statement
CarePlus faced several business and technical issues:

- Operational insights were scattered across multiple OLTP sources.
- Ticket data was stored in MySQL, while system logs were stored separately on a cloud server.
- There was no centralized data warehouse for analytics.
- Dashboards were created independently across teams, leading to inconsistent KPIs.
- Manual processes delayed decision-making and made scalability difficult.

This project builds an automated ETL system using AWS to integrate all data, transform it, store it in a data warehouse, and expose it to BI tools—resulting in unified business insights.

---

## 🏗️ Data Engineering Architecture

### **1. Data Sources (OLTP Layer)** 
- **Cloud Server:** Stores system logs (semi-structured/unstructured data)
- **MySQL Database:** Contains tickets data (related structured data)

### **2. Data Lake Layer – Amazon S3**
Raw data from both sources is ingested in the S3 Data Lake:
- ***s3://careplus-stored-data/support-logs/raw/***
- ***s3://careplus-stored-data/support-tickets/raw/***

### **3. Data Processing & Transformation**

#### **a) Log Files Pipeline**
- Raw log files ingested into S3.  
- **AWS Lambda (serverless)** performs:
  - Data Cleaning  
  - Parsing JSON/text logs  
  - Data transformation  
- Output stored as Parquet in: ***s3://careplus-stored-data/support-logs/processed/***

#### **b) Tickets Pipeline**
- Tickets data in MySQL database exported as CSV files and ingested into S3. 
- **AWS Glue** transforms the data:
  - Cleaning & standardization  
  - Conversion to Parquet  
- Output stored as Parquet in: ***s3://careplus-stored-data/support-tickets/processed/***

### **4. Ad-hoc SQL Analysis – Amazon Athena**
- Run quick Ad-hoc queries directly on the parquet files in S3 processed directories. 
- Helps validate ETL output and perform exploratory analytics.

### **5. Data Warehouse Layer – Amazon Redshift Serverless**
- All cleaned and optimized processed data from S3 is loaded into Redshift. 
- Serves as the **single source of truth** for analytics and reporting.

### **6. Business Intelligence – Power BI**
- Connected Power BI to Redshift to build:  
  - **A System Logs Performance Dashboard**
  - **A centralized Ticket Insights Dashboard**

All dashboards reflect the latest data automatically.

### **7. Pipeline Automation**
The entire ETL process is automated:
- Any new data entering the OLTP system is:
    - Automatically ingested → transformed → stored
    - Loaded into Redshift
    - Reflected in Power BI
    - No manual intervention needed.

---

## 🖼️ Pipeline Architecture Diagram
![Pipeline Architecture](aws_project_pipeline.svg)

---

## 📊 Dashboard Preview

### System Log Performance Dashboard
![Log Dashboard](dashboards/logs_insights.png)

### Ticket Insights Dashboard
![Ticket Dashboard](dashboards/ticket_insights.png)
