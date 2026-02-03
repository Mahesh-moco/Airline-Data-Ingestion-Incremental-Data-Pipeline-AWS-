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
