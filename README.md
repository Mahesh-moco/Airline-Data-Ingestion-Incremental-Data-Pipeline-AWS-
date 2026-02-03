# ✈️ Airline Data Ingestion – Incremental Data Pipeline (AWS)

## Overview

This project implements an **end-to-end, event-driven incremental data ingestion pipeline** for airline data using AWS services. The pipeline processes **airport reference data** and **high-volume daily flight data (~500K records/day)** in a scalable, reliable, and production-ready manner.

## Tech Stack

* **Programming:** Python
* **Storage:** Amazon S3
* **ETL & Metadata:** AWS Glue, Glue Crawlers, Glue Data Catalog
* **Data Warehouse:** Amazon Redshift
* **Orchestration:** AWS Step Functions
* **Eventing & Alerts:** Amazon EventBridge, Amazon SNS

## Architecture

The architecture illustrates the **end-to-end airline data ingestion pipeline** using AWS services:

1. **Data Ingestion Layer:**  
   - Airport codes (reference data) and daily flight data are uploaded to Amazon S3.  
You can see the sample files in the repo:
    - [Airport Codes CSV]([data/airport_codes.csv](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/Data/airports_codes.csv))  
    - [Daily Flights CSV]([data/daily_flights_20250120.csv](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/Data/flights_part_1.csv))
2. **Metadata & Schema Management:**  
   - **AWS Glue Crawlers** automatically discover schemas and register tables in the **Glue Data Catalog** for S3 and Redshift.

3. **Data Processing Layer:**  
   - AWS Glue ETL jobs, created via **Glue Studio GUI**, process daily flight data incrementally using **Job Bookmarking**.
   - Redshift has a pre-loaded airport codes table, while daily flight data is processed incrementally and stored temporarily; a flight fact table is planned for the future.
   - [AWS Glue ETL jobs](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/glue_etl_job.py)
   - [Redshift Create Table Command](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/redshift_create_table_commands.txt)


4. **Orchestration Layer:**  
   - **AWS Step Functions** orchestrate the pipeline execution.
   - **Amazon EventBridge** triggers the Step Function based on schedule or events.
   - [AWS Step Functions Config](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/step_function_config.json)
   - [AWS Step Functions Flow](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/Screenshot%202026-02-03%20144142.png)
   - [Amazon EventBridge Rule](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/event_bridge_rule.json)

5. **Monitoring & Notifications:**  
   - **Amazon SNS** sends notifications for job success or failure, enabling real-time monitoring.

![Project Architecture](https://github.com/Mahesh-moco/Airline-Data-Ingestion-Incremental-Data-Pipeline-AWS-/blob/main/airline%20arhitecture%20flow.png)


## Data Flow

1. **Data Ingestion:** Airport codes (static) and daily flight data are ingested into Amazon S3.
2. **Schema Discovery:** AWS Glue Crawlers automatically infer schemas and register tables in the Glue Data Catalog for S3 and Redshift.
3. **Target Setup:** Pre-loaded airport codes dimension table and flight  table schema are created in Amazon Redshift.
4. **Incremental Processing:** AWS Glue ETL job processes only new flight data using **Glue Job Bookmarking** to ensure idempotent loads.
5. **Orchestration:** AWS Step Functions orchestrate the workflow execution.
6. **Triggering:** Amazon EventBridge triggers the Step Function on schedule or events.
7. **Monitoring:** Amazon SNS sends notifications for job success and failure.


## Use Case

This project simulates a **real-world airline analytics pipeline**, enabling efficient ingestion and analysis of flight operations data for reporting and business insights.

## Author

**Mahesh Choure**
