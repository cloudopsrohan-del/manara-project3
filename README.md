# Project 3: Serverless REST API with API Gateway, Lambda, and DynamoDB

## 📌 Description
This project implements a **serverless REST API** using AWS API Gateway, AWS Lambda, and DynamoDB to manage a simple to-do list. It supports full CRUD operations without managing any servers.

---

## 🏗️ Architecture Diagram
![Architecture Diagram](./architecture-diagram.png)

---

## 🧱 AWS Services Used
- **Amazon API Gateway** – exposes RESTful endpoints.
- **AWS Lambda** – backend logic for CRUD operations.
- **Amazon DynamoDB** – stores to-do records in a NoSQL table.
- **IAM** – secure Lambda access to DynamoDB.
- **Amazon S3** *(optional)* – host front-end UI.
- **Amazon CloudWatch** – logs and monitors API activity.

---

## ⚙️ How It Works
1. User sends HTTP requests (`POST`, `GET`, `PUT`, `DELETE`) to API Gateway.
2. API Gateway routes the request to a Lambda function.
3. Lambda performs CRUD operations on the DynamoDB table `TodosTable`.
4. Lambda returns JSON responses via API Gateway.
5. (Optional) S3 hosts a front-end web app to interact with the API.

---

## 📦 Deployment Steps
1. Create DynamoDB table:
   - Name: `TodosTable`
   - Partition Key: `id` (String)
2. Create Lambda function:
   - Runtime: Python 3.12
   - Set env var `TABLE_NAME=TodosTable`
   - Attach IAM policy for DynamoDB `GetItem`, `PutItem`, `UpdateItem`, `DeleteItem`
3. Create API Gateway REST API:
   - Methods: `GET`, `POST`, `PUT`, `DELETE`
   - Integrate each with Lambda.
4. Enable CORS for all methods.
5. Deploy the API.
6. (Optional) Host front-end on S3 with HTML/JS calling the API.

---

## 🧪 Example Requests (via Postman or curl)

### Create To-Do
```bash
curl -X POST https://<api-id>.execute-api.<region>.amazonaws.com/prod/todos \
  -H "Content-Type: application/json" \
  -d '{"id":"1","task":"Learn AWS","status":"pending"}'
