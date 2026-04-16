# Automating Secure Data Backup and Real-Time Notifications using Amazon S3, AWS Lambda, and Amazon SNS

## Project Title
Automating Secure Data Backup and Real-Time Notifications using AWS

## Objective
The primary objective of this project is to implement a fully automated, secure, and reliable backup solution for critical data using AWS native services. This ensures data durability via Amazon S3, automated processing with AWS Lambda, and real-time execution alerts via Amazon SNS, reducing manual operational overhead and increasing system resilience.

## Architecture Overview
The architecture is serverless and event-driven. File uploads to an Amazon S3 bucket automatically trigger an AWS Lambda function. This function validates the incoming files and securely manages the backup processes. Finally, upon completion (or failure) of the backup routine, Amazon SNS publishes an immediate notification to subscribed stakeholders via email/SMS.

## Workflow
1. **File upload to S3**: An authorized user or system uploads a file to the primary Amazon S3 bucket.
2. **Trigger AWS Lambda**: The upload event `s3:ObjectCreated:*` triggers an AWS Lambda function execution automatically.
3. **Process/validate backup**: The Lambda function inspects the event, validates the object details (e.g., file type, size), and performs any necessary backup processing like moving the file to archival storage or encrypting the data.
4. **Send notification via SNS**: After the backup is validated and processed, the Lambda function publishes a success/failure message to an Amazon SNS topic, sending an alert out to administrators.

## AWS Services Used
- **Amazon S3**: Used as the primary secure object storage layer. 
- **AWS Lambda**: Executes the serverless logic for data validation, routing, and processing without maintaining servers.
- **Amazon SNS**: Facilitates the pub/sub messaging infrastructure for real-time notifications.

## Features
- **Automated backup**: Eliminates the need for manual file transfers and cron jobs.
- **Real-time notifications**: Immediate visibility into the backup status ensures stakeholders know immediately if an operation fails.
- **Secure storage**: Employs AWS Key Management Service (KMS) for encryption-at-rest along with S3 Object Versioning to prevent accidental deletion or corruption.

## System Architecture Diagram
Below is the visual representation of our serverless architecture:

![Architecture Details](architecture/architecture-diagram.png)

## How to Run / Setup Steps
1. Create an **Amazon S3 Bucket** to receive the source files. Ensure versioning and default encryption are enabled.
2. Create an **Amazon SNS Topic** and subscribe your email/phone number to it for alerts.
3. Create an **AWS Lambda Function** (e.g., using Python/Boto3 or Node.js) with IAM permissions allowing access to S3 (Read/Write) and SNS (Publish).
4. Configure an **S3 Event Notification** on the bucket to trigger the Lambda function for all `PUT` and `POST` object events.
5. Upload a test file to the S3 bucket.
6. Verify the successful backup in S3 and check your email/mobile for the SNS notification!

## Author
**Yash Patil**
