# Serverless API

## Purpose

The site includes a serverless AWS backend for API functionality using AWS SAM (Serverless Application Model).

## Requirements

### Requirement: AWS SAM Application Structure

The backend SHALL be defined as an AWS SAM application in `backend/template.yaml`.

#### Scenario: SAM template configuration

- **WHEN** deploying the backend
- **THEN** AWS CloudFormation provisions resources from `backend/template.yaml`
- **AND** includes S3, CloudFront, Lambda, and API Gateway resources

### Requirement: Lambda Function Runtime

Lambda functions SHALL use Node.js 20.x runtime with ESM module format.

#### Scenario: Lambda handler format

- **WHEN** a Lambda function is created
- **THEN** it uses `.mjs` file extension
- **AND** exports handlers using `export const`
- **AND** the handler is an async function

### Requirement: Hello World API Endpoint

The backend SHALL provide a `/hello` GET endpoint that returns a simple JSON response.

#### Scenario: Hello endpoint response

- **WHEN** a GET request is made to `/hello`
- **THEN** a JSON response is returned with status 200
- **AND** the response body contains a message

### Requirement: CloudFront CDN Distribution

The backend SHALL use CloudFront for content delivery and API routing.

#### Scenario: CDN content delivery

- **WHEN** requests are made to the site
- **THEN** CloudFront serves static content from S3
- **AND** routes API requests to API Gateway

### Requirement: Local Development Testing

The backend SHALL support local testing via SAM CLI.

#### Scenario: Local API testing

- **WHEN** running `sam local start-api` in the backend directory
- **THEN** a local API server starts
- **AND** Lambda functions can be invoked locally

#### Scenario: Unit testing

- **WHEN** running `npm test` in `backend/hello-world/`
- **THEN** Mocha/Chai tests execute
- **AND** test results are reported

### Requirement: Manual Deployment

The backend SHALL be deployed manually using SAM CLI, separate from frontend deployment.

#### Scenario: Backend deployment

- **WHEN** running `sam deploy` in the backend directory
- **THEN** CloudFormation stack is created or updated
- **AND** AWS resources are provisioned
