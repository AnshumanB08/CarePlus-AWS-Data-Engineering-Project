# 🏢 CarePlus – AWS End-to-End Data Engineering

## 📌 Project Overview

CarePlus is an imaginary BPO company that manages customer support operations for multiple clients. As the business scaled, operational data such as support tickets and system logs were scattered across multiple databases and dashboards. This fragmentation made it difficult for stakeholders to get a unified view of customer issues, agent performance, and system health.

To address this challenge, this project focuses on designing and implementing a fully automated, cloud-native data engineering pipeline on AWS that consolidates structured and unstructured data into a single source of truth. The transformed data is stored in a centralized data warehouse and consumed by analytical tools to generate unified dashboards for business and operational insights.

---

## 🎯 Problem Statement

- Operational data was distributed across multiple OLTP systems and dashboards.
- Support tickets (structured data) resided in a MySQL database, while system logs (semi-structured/unstructured data) were stored on a cloud server.
- Lack of a centralized analytics layer resulted in inconsistent metrics, delayed insights, and limited visibility into system performance and support operations.

The objective was to build an end-to-end ETL pipeline that converts OLTP data into an OLAP-friendly format, creates a single source of truth, and enables scalable analytics through dashboards.

---

## 🏗️ Data Engineering Architecture

The solution is built using a modern AWS serverless architecture:

- ### **Data Sources (OLTP)** 
  - Support Tickets stored in MySQL
  - Support Logs stored on a cloud server

- ### **Data Lake (Amazon S3)**
  - **Raw Zone:** Stores incoming ticket CSV files and raw log files
  - **Processed Zone:** Stores cleaned and transformed data in Parquet format

- ### **Data Processing & Transformation**
  - **AWS Lambda:** Cleans and transforms raw log files and writes optimized Parquet data to S3
  - **AWS Glue:** Processes ticket data extracted from MySQL, applies transformations, and stores it in Parquet format

- ### **Analytics & Storage**
  - **Amazon Athena:** Enables ad-hoc SQL analysis directly on processed data in S3
  - **Amazon Redshift Serverless:** Acts as the centralized data warehouse

- ### **Visualization**
  - **Power BI** connected to Amazon Redshift to generate interactive dashboards

- ### **Automation**
  - The pipeline is fully automated. Any new data arriving from the **OLTP systems** is automatically **ingested, transformed, loaded** into **Redshift**, and reflected in the **Power BI dashboards**.

---

## 🖼️ Pipeline Architecture Diagram

![Pipeline Architecture](aws_project_pipeline.svg)

---

## 📊 Dashboard Preview

### Support Tickets Insights

![Tickets Dashboard](tickets_ss.png)

Key insights include:
- Total, resolved, open, and escalated tickets
- Agent-wise ticket distribution
- Resolution time analysis by issue category and priority
- Channel-wise ticket status breakdown

### Support Logs Insights

![Logs Dashboard](logs_ss.png)

Key insights include:
- System CPU usage trends
- Average response times
- Log distribution by severity and user agent
- Correlation between response time ranges and logged tickets

🔗 [**Interactive Dashboard Web View**](https://app.powerbi.com/view?r=eyJrIjoiMTc0MjlkMjEtMWU5My00ZWY0LWJmMzAtZjc5NTVhYzVmZGVhIiwidCI6ImM2ZTU0OWIzLTVmNDUtNDAzMi1hYWU5LWQ0MjQ0ZGM1YjJjNCJ9)

---

## 🚀 Outcome and Business Impact

- Established a single source of truth for both support tickets and system logs.
- Reduced manual reporting and eliminated dependency on multiple dashboards.
- Enabled faster, data-driven decision-making for operations and management teams.
- Improved visibility into system performance, agent productivity, and customer support efficiency.
- Built a scalable and cost-efficient serverless data platform using AWS managed services.

---

## 🧩 Problems Solved

- Data silos across multiple systems were consolidated into a centralized analytics platform.
- Inefficient querying of raw data was replaced with optimized Parquet-based analytics.
- Lack of real-time visibility was resolved through automated data ingestion and refresh.
- Operational metrics became consistent, reliable, and easily accessible.

---

## 🧠 Skills and Concepts Learned

- Designing end-to-end ETL pipelines on AWS
- Working with data lakes and zone-based architectures (raw vs processed)
- Serverless data processing using AWS Lambda and AWS Glue
- Data modeling for OLAP and analytics
- Querying large datasets using Amazon Athena
- Loading and optimizing data in Amazon Redshift Serverless
- Building production-ready dashboards using Power BI
- Automating data pipelines for reliability and scalability

---

## 🙏 Acknowledgement

A special thank you to **Codebasics**.
This project was built as part of their [**Data Engineering Basics Course**](https://codebasics.io/courses/data-engineering-basics-for-data-analysts), and their guidance was instrumental in helping me design and implement this end-to-end AWS pipeline.

---

## 🧰 Tech Stack

- AWS S3
- AWS Lambda
- AWS Glue
- Amazon Athena
- Amazon Redshift Serverless
- Power BI
- MySQL

---
