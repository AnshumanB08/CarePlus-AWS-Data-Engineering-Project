# CarePlus – AWS End-to-End Data Engineering

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
  - A **System Logs Performance** Dashboard
  - A centralized **Ticket Insights** Dashboard

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

### System Logs Performance Dashboard
![Logs Dashboard](logs_ss.png)

### Tickets Insights Dashboard
![Tickets Dashboard](tickets_ss.png)

🔗 [**Interactive Dashboard Web View**](https://app.powerbi.com/view?r=eyJrIjoiMTc0MjlkMjEtMWU5My00ZWY0LWJmMzAtZjc5NTVhYzVmZGVhIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

---

## 🚀 Project Outcomes
This project successfully delivered:

**✔ A unified data ecosystem:** All structured and unstructured data is centralized into one data warehouse **(Redshift)**.

**✔ Single Source of Truth:** Redshift now holds clean, transformed, analytics-ready datasets.

**✔ Automated ETL Pipeline:** Reduced manual handling by 100% through Lambda, Glue, and S3 event triggers.

**✔ Consistent KPIs Across the Organization:** Power BI dashboards provide unified metrics shared across teams.

**✔ Improved Operational Efficiency:**
  - Faster report generation
  - Reduced data duplication
  - Enhanced visibility into ticket handling & system performance

**✔ Scalability:** Serverless AWS components automatically scale with business needs.

---

## 🧠 Skills Learned
Through this project, I strengthened my expertise in:

### AWS Cloud Services
- Amazon S3 (Data Lake)
- AWS Lambda (Serverless ETL)
- AWS Glue (Data Transformation Jobs)
- Amazon Athena (SQL on Data Lake)
- Amazon Redshift Serverless (Data Warehousing)
- IAM Role-based access policies (Permissions & Security)

### Data Engineering Concepts
- ETL/ELT workflows
- OLTP → OLAP processing
- Data pipeline orchestration
- Schema design & data modeling
- Parquet optimization
- Handling unstructured logs data
- Building fully automated pipelines

### Analytics & Visualization
- Power BI data modeling
- Creating enterprise-grade dashboards

---

## 🙏 Acknowledgement
A special thank you to **Codebasics**.

This project was built as part of their [**Data Engineering Basics**](https://codebasics.io/courses/data-engineering-basics-for-data-analysts) course, and their guidance was instrumental in helping me design and implement this end-to-end AWS pipeline.

---

## ⭐ If you like this project

Consider giving the repository a star 🌟 to support its visibility!
