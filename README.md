
# 📌 To the Power of Math Using AWS

A **serverless web application** built using **AWS Amplify**, **API Gateway**, **AWS Lambda**, **DynamoDB**, and **IAM**.
The app calculates powers of numbers (`base^exponent`) and stores each calculation in a DynamoDB table.

---

![PowerOFMATH Web App](https://github.com/MahaLakshmi729/Power_Of_Math_Using_AWS/blob/71334e3852abd7d70811d159fefb753018867f3a/powerofmath.png)

## 🚀 Features

* **Frontend**: Hosted on **AWS Amplify**, with a clean UI to input values.
* **API Gateway**: Exposes a secure HTTP endpoint to interact with backend logic.
* **Lambda**: Performs the power calculation and manages database interactions.
* **DynamoDB**: Stores a history of all calculations.
* **IAM**: Manages permissions so Lambda can read/write to DynamoDB securely.

---

## 🏗 Architecture Overview

```
User → Amplify Frontend → API Gateway → Lambda → DynamoDB
```

* **Amplify**: Hosts the frontend and manages deployment.
* **API Gateway**: Routes requests from the frontend to the backend.
* **Lambda**: Calculates the power and stores results.
* **DynamoDB**: Persists calculations with timestamps.
* **IAM**: Controls access between AWS services.

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repo

```bash
git clone https://github.com/your-username/to-the-power-of-math.git
cd to-the-power-of-math
```

### 2️⃣ Setup DynamoDB Table

Create a DynamoDB table:

* **Table Name**: `PowerCalculations`
* **Primary Key**: `id` (String)

Example AWS CLI command:

```bash
aws dynamodb create-table \
  --table-name PowerCalculations \
  --attribute-definitions AttributeName=id,AttributeType=S \
  --key-schema AttributeName=id,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST
```

---

### 3️⃣ Deploy Lambda Function

* Create a new **AWS Lambda** function in the console.
* Runtime: **Node.js 18.x**
* Copy code from `/backend/lambda_function.js` into the function.
* Add an **IAM Role** with DynamoDB read/write access.

---

### 4️⃣ Setup API Gateway

* Create a **REST API** in API Gateway.
* Create a `POST /calculate` endpoint.
* Integrate it with the Lambda function.
* Enable **CORS**.
* Deploy the API and note the **Invoke URL**.

---

### 5️⃣ Connect Frontend

* Open `/frontend/script.js` and replace:

```javascript
const API_URL = "YOUR_API_GATEWAY_URL";
```

with your deployed API Gateway URL.

---

### 6️⃣ Host with AWS Amplify

* Create a new Amplify app.
* Connect your GitHub repo or upload `/frontend`.
* Deploy and open your live URL.

---

## 📊 Example API Request

```bash
curl -X POST \
  https://<api-id>.execute-api.<region>.amazonaws.com/prod/calculate \
  -H "Content-Type: application/json" \
  -d '{"base": 2, "exponent": 8}'
```

**Response:**

```json
{
  "result": 256,
  "message": "Calculation successful"
}
```

---

## 🔐 IAM Permissions

Example IAM policy to attach to Lambda:

```json
{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "YOUR-TABLE-ARN"
    }
    ]
}
```

---

## OUTPUT

![PowerOFMATH Web App](https://github.com/MahaLakshmi729/Power_Of_Math_Using_AWS/blob/71334e3852abd7d70811d159fefb753018867f3a/op1.png)


![PowerOFMATH Web APP](https://github.com/MahaLakshmi729/Power_Of_Math_Using_AWS/blob/71334e3852abd7d70811d159fefb753018867f3a/op2.png).
