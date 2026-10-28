# Document Processing Pipeline for Regulated Industries

An event-driven document processing pipeline for PDF and image documents, designed to demonstrate automated OCR, natural language processing, document search, metadata management, and data lineage using AWS managed services.

## Overview

This project demonstrates how organizations can process unstructured documents while maintaining traceability between original files, extracted content, processing operations, and downstream search indexes.

The pipeline integrates Amazon Textract for optical character recognition (OCR), Amazon Comprehend for natural language processing (NLP), and Amazon Elasticsearch Service for searchable document content. AWS Lambda, Amazon S3, Amazon SQS, Amazon SNS, and Amazon DynamoDB support processing workflows, metadata management, and document lineage.

## Key Features

- **Document ingestion:** Accept PDF and image documents through Amazon S3.
- **OCR processing:** Extract document text, tables, and form information using Amazon Textract.
- **Natural language processing:** Identify entities and key phrases using Amazon Comprehend.
- **Search and analytics:** Index extracted text and metadata for querying through Elasticsearch and Kibana.
- **Document registry:** Maintain document registration and associated metadata in Amazon DynamoDB.
- **Data lineage:** Track relationships between original documents and generated processing outputs.
- **Pipeline monitoring:** Record processing stages, operations, and execution statuses.
- **Event-driven architecture:** Coordinate asynchronous processing using AWS Lambda, Amazon SQS, and Amazon SNS.
- **Extensible workflow:** Support additional processing stages and downstream integrations.

## Architecture

The pipeline consists of five main modules:

1. **Metadata Services:** Registers documents and tracks lineage and pipeline operations.
2. **Ingestion Module:** Receives documents and initiates processing workflows.
3. **OCR Module:** Uses Amazon Textract to extract text and structured document information.
4. **NLP Module:** Uses Amazon Comprehend to identify entities and key phrases.
5. **Analytics Module:** Indexes processed content and metadata for search and analysis.

### Processing Workflow

```text
Document Upload
      |
      v
Amazon S3
      |
      v
Document Registration
      |
      v
Event-Driven Processing
      |
      v
Amazon Textract (OCR)
      |
      v
Amazon Comprehend (NLP)
      |
      v
Amazon S3 Results + DynamoDB Metadata
      |
      v
Amazon Elasticsearch Service
      |
      v
Search and Analytics
```

Amazon SNS, Amazon SQS, and AWS Lambda coordinate the workflow and support pipeline operations and metadata tracking.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming | Python |
| Cloud Platform | Amazon Web Services (AWS) |
| OCR | Amazon Textract |
| Natural Language Processing | Amazon Comprehend |
| Object Storage | Amazon S3 |
| Serverless Computing | AWS Lambda |
| Messaging and Events | Amazon SNS, Amazon SQS |
| Metadata and Lineage | Amazon DynamoDB |
| Search and Analytics | Amazon Elasticsearch Service, Kibana |
| Infrastructure as Code | AWS Cloud Development Kit (AWS CDK) |

## Repository Structure

```text
document-processing-pipeline-for-regulated-industries/
├── code/
│   ├── build.sh
│   └── [processing modules and Lambda source code]
├── infrastructure/
│   ├── package.json
│   └── [AWS CDK infrastructure definitions]
├── images/
├── README.md
├── LICENSE
├── NOTICE
└── CONTRIBUTING.md
```

The exact source files and subdirectories are maintained in the upstream repository.

## Prerequisites

- An AWS account with appropriate permissions.
- AWS CLI installed and configured.
- Node.js and npm.
- Python and the dependencies required by the repository.
- AWS CDK installed and configured.
- A Linux or macOS-compatible environment, as specified by the original project.

Review the upstream documentation for compatible dependency versions and account requirements before deployment.

## Installation and Deployment

### 1. Clone the repository

```bash
git clone https://github.com/aws-samples/document-processing-pipeline-for-regulated-industries.git

cd document-processing-pipeline-for-regulated-industries
```

### 2. Configure AWS credentials

Configure your AWS CLI credentials using an appropriate profile or your organization's approved authentication method.

```bash
aws configure
aws sts get-caller-identity
```

Verify that the active identity belongs to the intended AWS account.

### 3. Build the processing code

```bash
cd code
bash build.sh
```

The build script prepares the Python dependencies and the directory structure needed by the infrastructure deployment.

### 4. Install infrastructure dependencies

```bash
cd ../infrastructure
npm install
```

Review the package versions and the upstream deployment guidance before upgrading dependencies.

### 5. Bootstrap and deploy

```bash
npx cdk bootstrap
npx cdk deploy --all
```

Review the proposed infrastructure changes and AWS costs before approving deployment. The application deploys multiple CloudFormation stacks and creates cloud resources.

## Testing the Pipeline

After deployment:

1. Locate the raw-document upload bucket created by the pipeline.
2. Upload a small, non-sensitive PDF document.
3. Verify document registration in the DynamoDB document registry.
4. Inspect the document lineage and pipeline operations records.
5. Confirm that OCR and NLP processing complete successfully.
6. Inspect the generated results in the corresponding S3 buckets.
7. Verify that extracted text and metadata are indexed and searchable through the configured Elasticsearch/Kibana interface.

Refer to the original repository's README for the expected resource names, output formats, and detailed validation procedure.

## Data Governance and Traceability

The pipeline demonstrates document registration, metadata management, lineage tracking, and processing-stage records. These capabilities help establish traceability between source documents and downstream processing outputs.

This reference implementation demonstrates governance-oriented architecture patterns; it should not be interpreted as proof of regulatory compliance or production security without an independent assessment and appropriate controls.

## Extending the Solution

Potential extensions include:

- Adding document classification and custom routing rules.
- Integrating additional OCR or NLP services.
- Adding validation and human-review stages.
- Developing a web interface for document upload and processing status.
- Implementing retrieval-augmented generation (RAG) over indexed document content.
- Building automated evaluation tests for retrieval quality and answer grounding.
- Adding authentication, access controls, monitoring, and alerting.
- Integrating CI/CD workflows for automated testing and infrastructure deployment.

These extensions are proposed enhancements, not features claimed to be implemented in the original repository.

## Deployment Cleanup

To remove the deployed CDK stacks when they are no longer needed:

```bash
cd infrastructure
npx cdk destroy --all
```

Review the resources and dependencies before confirming deletion. Verify the AWS account afterward for any remaining billable resources, data, or infrastructure that requires separate cleanup.

## License and Attribution

This project is based on the AWS Samples repository:

https://github.com/aws-samples/document-processing-pipeline-for-regulated-industries

The upstream project is distributed under the Apache License 2.0. Review the original LICENSE and NOTICE files and preserve applicable copyright and attribution notices when redistributing or modifying the code.

If you extend this project for a portfolio, clearly document your own modifications, additional components, tests, and deployment work.

## Disclaimer

This repository demonstrates an AWS-based document processing architecture. Deployment requirements, service availability, costs, and security configurations depend on the environment. Validate all resources and configurations before using the solution with sensitive or regulated data.
