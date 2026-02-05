# End-to-End FMCG Data Engineering Pipeline

## Overview
This project demonstrates a production-style end-to-end data engineering pipeline built using modern Lakehouse principles. The objective is to consolidate sales data from two merged FMCG companies that operate on different systems with inconsistent schemas, missing historical data, and data quality issues.

The project focuses on building a reliable, scalable, and maintainable data platform rather than emphasizing dashboard visuals. It closely mirrors real-world data engineering challenges such as schema mismatches, incremental processing, and pipeline automation.

---

## Business Context
A large FMCG manufacturer acquired a fast-growing nutrition brand. Post-acquisition, both companies continued operating on separate data systems and reporting workflows. Data was fragmented across flat files and spreadsheets, leading to inconsistent metrics, duplicated records, and manual reporting overhead.

Leadership required a unified analytics data layer that could serve as a single source of truth while supporting both historical backfill and ongoing daily data ingestion.

---

## Problem Statement
The solution needed to:
- Consolidate sales data from two companies with incompatible schemas  
- Resolve schema mismatches, missing history, and data quality issues  
- Support historical backfill and daily incremental ingestion  
- Avoid full reprocessing of data on each run  
- Provide analytics-ready datasets for dashboards and ad-hoc analysis  
- Be scalable, reliable, and easy to extend  

---

## Architecture

The pipeline follows a Lakehouse Medallion Architecture (Bronze → Silver → Gold) designed to separate raw ingestion, transformation, and analytics layers.

![Project Architecture](https://github.com/shonil24/Atlikon-fmcg-data-engineering-project/blob/master/resources/project_architecture.png)

### Bronze Layer
- Raw immutable data ingestion from source CSV files
- Minimal transformations
- Metadata added for traceability

### Silver Layer
- Data cleaning and validation
- Schema standardization across systems
- Deduplication and null handling
- Business rule application
- Surrogate key generation

### Gold Layer
- Aggregated and analytics-ready datasets
- Star schema implementation
- Optimized for BI and reporting use cases

This layered approach improves data quality isolation, simplifies debugging, and supports long-term scalability.

---

## Tech Stack
- Databricks (Free Edition)
- PySpark
- SQL
- Delta Lake
- AWS S3
- Databricks Jobs
- Databricks Dashboards / Genie

---

## Data Model
A **Star Schema** was implemented in the Gold layer.

### Fact Table
- Orders / Sales

### Dimension Tables
- Customers
- Products
- Pricing
- Date

Surrogate keys were generated using hashing to ensure consistent joins across heterogeneous source systems.

---

## Pipeline Workflow
1. Raw CSV data ingestion from AWS S3 into Bronze tables  
2. Data cleaning and validation in the Silver layer  
3. Schema alignment across multiple source systems  
4. Historical backfill processing  
5. Daily incremental ingestion using Delta Lake merge logic  
6. Monthly aggregations for analytics consumption  
7. Automated pipeline execution using Databricks Jobs  

---

## Incremental Processing Strategy
- Historical data is processed once during initial backfill  
- New data is ingested incrementally on a daily basis  
- Delta Lake merge logic is used to upsert records  
- Prevents full dataset reprocessing and improves performance  

---

## Data Quality Handling
The following data quality measures were implemented:
- Deduplication of records  
- Null handling and default value strategies  
- Trimming and normalization of string fields  
- Validation of key business fields  
- Schema consistency checks  

---

## Orchestration & Automation
- End-to-end pipeline orchestration implemented using Databricks Jobs  
- Jobs scheduled to run daily  
- Layer dependencies enforced to ensure correct execution order  
- No manual intervention required after deployment  

---

## Analytics & BI Enablement
- Gold-layer tables designed for direct BI consumption  
- Denormalized analytics views created for faster querying  
- Dashboards built using Databricks Dashboards and Genie  

---

## How to Run This Project
1. Create a Databricks Free Edition workspace  
2. Configure access to AWS S3  
3. Upload sample CSV files to S3  
4. Import notebooks into Databricks  
5. Execute notebooks in Bronze → Silver → Gold order  
6. Configure Databricks Jobs for automation  

---

## Learning Outcomes
- Designing Lakehouse architectures using the Medallion pattern  
- Handling real-world schema mismatches and dirty data  
- Implementing historical backfill and incremental pipelines  
- Using Delta Lake for reliable upsert operations  
- Automating pipelines using Databricks Jobs  
- Building analytics-ready data models  

---

## Credits
Project structure and learning inspiration adapted from Codebasics.
