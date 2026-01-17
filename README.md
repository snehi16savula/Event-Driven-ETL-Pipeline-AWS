Event-Driven-ETL-Pipeline-AWS
This project implements a serverless, event-driven ETL (Extract, Transform, Load) pipeline on AWS.
The pipeline is designed to automatically ingest data when events occur, process it at scale, and load the transformed data into an analytics-ready destination with minimal operational overhead.

The architecture leverages AWS managed services to ensure scalability, fault tolerance, and cost efficiency.


Architecture

The pipeline follows an event-driven design pattern:

Data Ingestion 

Raw data files  are uploaded to an Amazon S3 landing bucket.

Each upload triggers an event notification.

Event Processing

S3 events invoke an AWS Lambda function.

Lambda validates metadata, logs events, and routes processing logic.

Transformation Layer

Lightweight transformations are handled directly in Lambda.

For large datasets, Lambda triggers AWS Glue jobs for distributed processing.

Data Storage 

Transformed data is written to:

Amazon S3
Amazon Redshift

Monitoring & Logging

Amazon CloudWatch captures logs, metrics, and error alerts.

Dead-letter queues (DLQ) handle failed events gracefully.

 ETL Workflow
Source Event → S3 Upload
        ↓
S3 Event Notification
        ↓
AWS Lambda Triggered
        ↓
Data Validation & Transformation
        ↓
Curated S3
        ↓
Analytics & Reporting

Services Used

Amazon S3 – Data lake 

AWS Lambda – Event handling and lightweight transformations

AWS Glue – Scalable ETL for large datasets

Amazon EventBridge – Event routing 

Amazon CloudWatch – Logging and monitoring

IAM – Secure access control

 Project Structure
event-driven-etl/
│
├── lambda/
│   ├── handler.py          
│   ├── requirements.txt
│
├── glue/
│   ├── etl_job.py          
│
├── infrastructure/
│   ├── template.yaml       
│
├── data/
│   ├── sample_input.csv
│
├── README.md


This upload automatically triggers the ETL pipeline.

 Key Features

Fully serverless & scalable

Near real-time processing

Automatic failure handling

Cost-efficient (pay per execution)

Easy to extend with new data sources

Security Considerations

IAM roles follow least-privilege access

S3 buckets use encryption at rest

Sensitive data masked during transformation

VPC integration supported for private workloads

Use Cases

Real-time log processing

IoT event ingestion

Retail transaction pipelines

Clickstream analytics

Data lake automation

 Future Enhancements

Add schema validation using AWS Glue Data Catalog

Integrate Step Functions for complex workflows

Implement CI/CD with GitHub Actions

Add data quality checks
