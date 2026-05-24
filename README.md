1. Project Overview
This document outlines the data ingestion layer of the PulsePoint pipeline. The goal of this stage is to
integrate multiple wearable sensor datasets, standardize and clean the data, ingest the data into AWS
using a serverless architecture, and store the data in a centralized raw data lake (S3). This stage
serves as the foundation for downstream machine learning, processing, and dashboard development.

2. Pipeline Architecture
Colab (Data Cleaning & Integration) ® API Gateway (POST /ingest endpoint) ® AWS Lambda
(processing & ingestion) ® Amazon S3 (raw data storage)

3. What Has Been Implemented
Data Integration: Combined UCI Heart, PMData, and WESAD datasets into a unified schema.
Data Cleaning: Handled missing values and converted NaN to null for JSON compatibility.
Payload Generation: Exported data as JSON batches with batch_id and records.
AWS Ingestion Pipeline: Configured API Gateway, Lambda, and S3 raw zone storage.

4. AWS Resources
API Gateway Endpoint:
https://0tcvknirlc.execute-api.us-east-1.amazonaws.com/ingest
Lambda Function: pulsepoint-ingestion-lambda
S3 Bucket: pulsepoint-raw-zone-mena (raw/)

5. Data Format Specification
{
"batch_id": "pulsepoint_batch_001",
"records": [
{
"record_id": 1,
"participant_id": "H1",
"source_dataset": "uci_heart",
"age": 63,
"sex": 1,
"resting_bp": 145,
"chol": 233,
"max_hr": 150,
"avg_hr": null,
"avg_steps": null,
"avg_calories": null,
"avg_sleep_score": null,
"eda_mean": null,
"bvp_mean": null,
"temp_mean": null,
"ecg_mean": null,
"cardio_risk_label": 1,
"stress_label_mean": null
}
]
}

6. How to Access the Data
Use sample_data.json for real pipeline output.
Use payload_format.json as schema reference.

7. Shared Files
sample_data.json, payload_format.json, lambda_function.py, README.docx

8. Access Considerations
Due to AWS Learner Lab limitations, direct IAM sharing may not be possible. Use shared files and
documentation for collaboration.

9. Key Design Decisions
Serverless architecture, JSON format, batch ingestion, separation of raw and processed layers.

10. Summary
The ingestion layer is fully implemented and operational. The pipeline is ready for PCA, logistic
regression, AWS Fargate deployment, and Streamlit dashboard development
