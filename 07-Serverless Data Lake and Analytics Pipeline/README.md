# Serverless Data Lake and Analytics Pipeline

## Project Overview

This project demonstrates how to build a **fully serverless data lake and analytics platform on AWS** for a retail business. The solution ingests streaming transactional data into Amazon S3 using Amazon Kinesis Data Firehose, automatically discovers schemas with AWS Glue Crawlers, transforms raw JSON files into optimized Parquet datasets using AWS Glue ETL jobs, and enables serverless analytics with Amazon Athena. Business users can visualize key performance indicators through Amazon QuickSight dashboards powered by SPICE for fast, interactive reporting.

The architecture follows the modern **three-zone data lake design** consisting of Raw, Curated, and Aggregated layers while implementing encryption, fine-grained access control, and automated data processing.

---

# Architecture

```
Retail Application
        │
        ▼
Amazon Kinesis Data Firehose
        │
        ▼
Amazon S3 (Raw Zone)
        │
EventBridge Scheduler
        │
        ▼
AWS Glue ETL Job
        │
        ▼
Amazon S3 (Curated Zone)
        │
AWS Glue Crawler
        │
        ▼
AWS Glue Data Catalog
        │
        ▼
Amazon Athena
        │
        ▼
Amazon QuickSight Dashboard
```

---

# Architecture Components

### Amazon Kinesis Data Firehose

Receives streaming retail transaction records and delivers them directly to the Raw S3 bucket. Firehose provides automatic buffering, compression, retries, and scalable data ingestion without managing infrastructure.

---

### Amazon S3 Data Lake

The data lake is divided into three logical layers.

### Raw Zone

* Original JSON transaction files
* Immutable storage
* Encrypted with AWS KMS
* Lifecycle policies for long-term storage

### Curated Zone

* Cleaned datasets
* Converted to Parquet format
* Partitioned by Year / Month / Day
* Optimized for analytical queries

### Aggregated Zone

* Business-ready datasets
* Daily and monthly sales summaries
* Customer analytics
* Executive reporting datasets

---

### AWS Glue

AWS Glue automates metadata discovery and data transformation.

#### Glue Crawlers

* Detect new datasets
* Infer schema automatically
* Populate the Glue Data Catalog

#### Glue ETL Jobs

The ETL pipeline performs the following tasks:

* Read raw JSON files
* Validate records
* Remove invalid data
* Convert JSON to Parquet
* Partition data by date
* Store optimized datasets in the Curated zone

---

### AWS Glue Data Catalog

Provides a centralized metadata repository for all datasets stored in Amazon S3.

Benefits include:

* Centralized schema management
* Automatic table discovery
* Athena integration
* Reusable metadata across analytics services

---

### Amazon Athena

Athena enables serverless SQL queries directly against data stored in Amazon S3.

Example use cases:

* Daily sales analysis
* Revenue reports
* Customer behavior analytics
* Product performance analysis

Cost optimization techniques:

* Partition pruning
* Parquet format
* Compression
* Predicate pushdown
* Avoiding SELECT *

---

### AWS Lake Formation

Lake Formation secures the data lake using fine-grained permissions.

Implemented controls include:

* Database-level permissions
* Table-level permissions
* Column-level security
* Row-level security
* Centralized governance

Example:

Finance users can view Revenue columns while Customer Support users are restricted from viewing sensitive customer information.

---

### Amazon QuickSight

QuickSight provides interactive dashboards for business stakeholders.

Dashboard widgets include:

* Total Revenue
* Total Orders
* Sales by Region
* Revenue Trend
* Top Selling Products
* Average Order Value
* Customer Growth
* Monthly Sales Performance

SPICE is used to accelerate dashboard performance through in-memory caching.

---

### EventBridge Scheduler

EventBridge automates the analytics pipeline by scheduling:

* Glue Crawlers
* Glue ETL Jobs
* Daily aggregation workflows

This eliminates manual execution and keeps datasets up to date.

---

# Security

The solution implements multiple security best practices.

* IAM least privilege access
* AWS KMS encryption for data at rest
* HTTPS encryption in transit
* Amazon S3 Bucket Policies
* Lake Formation permissions
* Athena Workgroup controls
* CloudTrail logging for auditing

---

# Cost Optimization

Several techniques are used to minimize operational costs.

* Serverless architecture (no servers to manage)
* Parquet columnar storage
* Data partitioning
* Compression
* Athena pay-per-query model
* S3 Intelligent Tiering
* Lifecycle policies
* QuickSight SPICE caching

---

# Project Workflow

```
Retail Transactions
        │
        ▼
Kinesis Data Firehose
        │
        ▼
Amazon S3 Raw Zone
        │
        ▼
Glue Crawler
        │
        ▼
Glue Data Catalog
        │
        ▼
Glue ETL Job
        │
        ▼
Amazon S3 Curated Zone (Parquet)
        │
        ▼
Amazon Athena
        │
        ▼
Amazon QuickSight Dashboard
```

---

# AWS Services Used

| Service                      | Purpose                         |
| ---------------------------- | ------------------------------- |
| Amazon S3                    | Data Lake Storage               |
| Amazon Kinesis Data Firehose | Real-time Data Ingestion        |
| AWS Glue Crawlers            | Schema Discovery                |
| AWS Glue ETL                 | Data Transformation             |
| AWS Glue Data Catalog        | Metadata Repository             |
| Amazon Athena                | Serverless SQL Analytics        |
| AWS Lake Formation           | Data Governance                 |
| Amazon QuickSight            | Business Intelligence Dashboard |
| Amazon EventBridge Scheduler | Workflow Automation             |
| AWS IAM                      | Identity & Access Management    |
| AWS KMS                      | Data Encryption                 |

---

# Learning Outcomes

By completing this project, you will learn how to:

* Design a scalable serverless data lake architecture.
* Build a three-zone S3 data lake (Raw, Curated, Aggregated).
* Stream real-time data using Amazon Kinesis Data Firehose.
* Discover schemas automatically with AWS Glue Crawlers.
* Transform JSON into partitioned Parquet datasets.
* Query data efficiently using Amazon Athena.
* Apply fine-grained governance with AWS Lake Formation.
* Build executive dashboards with Amazon QuickSight.
* Secure data using IAM and AWS KMS.
* Optimize analytics costs using partitioning, compression, and serverless services.

---

# Future Improvements

* Integrate Amazon Redshift for enterprise-scale analytics.
* Add AWS Step Functions for advanced orchestration.
* Implement data quality validation with AWS Glue Data Quality.
* Enable near real-time dashboards using Amazon Managed Service for Apache Kafka (MSK).
* Configure CloudWatch alarms and notifications for pipeline monitoring.

---

# Conclusion

This project demonstrates a modern, fully managed, serverless analytics platform on AWS. By combining Amazon S3, Kinesis Data Firehose, AWS Glue, Athena, Lake Formation, and QuickSight, the solution delivers a secure, scalable, and cost-effective data lake capable of ingesting, transforming, governing, and visualizing large volumes of retail data with minimal operational overhead.
