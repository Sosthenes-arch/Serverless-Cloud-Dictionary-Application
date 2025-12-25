# Serverless Cloud Dictionary Application

This project is a **Serverless Cloud Dictionary** web application that allows users to search for definitions of various cloud-computing terms (specifically AWS). It is built using **React** for the frontend and integrates with a **serverless backend** on AWS (Lambda, API Gateway, and DynamoDB).

## Architecture

The application follows a serverless architecture pattern:

1.  **Frontend**: A React application hosted (can be on S3/Amplify) that provides the user interface.
2.  **API Layer**: Amazon API Gateway exposes REST endpoints to interact with the backend.
3.  **Compute**: AWS Lambda functions process requests (searching/fetching definitions).
4.  **Database**: Amazon DynamoDB stores the dictionary terms and their definitions.

![Architecture Diagram](Serverless%20cloud%20dict.%20architecture.svg)

## Features

*   **Search Functionality**: Real-time search for cloud terms.
*   **Responsive Design**: Clean and simple UI that works on desktop and mobile.
*   **Serverless Backend**: Scalable and cost-effective backend using AWS managed services.
*   **Pre-populated Data**: Includes JSON records for AWS-related terms.

## Tech Stack

*   **Frontend**: React.js, Axios, CSS
*   **Backend**: AWS Lambda, Amazon API Gateway
*   **Database**: Amazon DynamoDB
*   **Tools**: AWS CLI, Node.js, npm

## Prerequisites

*   **Node.js** (v14 or higher) and **npm** installed.
*   An **AWS Account**.
*   **AWS CLI** configured on your machine (for data seed).

## Setup Instructions

### 1. Backend Setup (Manual / Separate)

*Note: This repository primarily contains the Frontend code and Data records. You need to provision the backend infrastructure on AWS.*

1.  **DynamoDB Table**: Create a DynamoDB table (e.g., `CloudDictionary`).
    *   Partition Key: `term` (String)
2.  **Lambda Function**: Create a Lambda function to query the DynamoDB table.
    *   It should accept a `term` query parameter and return the item.
3.  **API Gateway**: Create a REST API with a `GET /get-definition` endpoint triggering the Lambda.
    *   Enable CORS.
    *   Deploy the API and get the **Invoke URL**.

### 2. Frontend Setup

1.  Clone the repository:
    ```bash
    git clone https://github.com/Sosthenes-arch/Serverless-Cloud-Dictionary-Application.git
    cd Serverless-Cloud-Dictionary-Application
    ```

2.  Install dependencies:
    ```bash
    npm install
    ```

3.  Configure API URL:
    *   Open `src/App.js`.
    *   Replace requests to `<ENTER_YOUR_API_URL>` with your actual **API Gateway Invoke URL**.
    ```javascript
    const apiUrl = 'https://xyz123.execute-api.us-east-1.amazonaws.com/prod';
    ```

4.  Start the application:
    ```bash
    npm start
    ```
    The app runs on `http://localhost:3000`.

## Data Population

The `records/` directory contains JSON files to populate your DynamoDB table.

1.  Open the JSON files in `records/` (e.g., `records-1.json`).
2.  Replace `<YOUR_TABLE_NAME>` with your actual DynamoDB table name (e.g., `CloudDictionary`).
3.  Use the AWS CLI to batch-write the items:

```bash
aws dynamodb batch-write-item --request-items file://records/records-1.json
aws dynamodb batch-write-item --request-items file://records/records-2.json
aws dynamodb batch-write-item --request-items file://records/records-3.json
aws dynamodb batch-write-item --request-items file://records/records-4.json
```

## Usage

1.  Open the web app.
2.  Type a term in the search bar (e.g., "AWS Lambda").
3.  Click **Search**.
4.  The definition will appear below.

## License

This project is open-source and available under the MIT License.