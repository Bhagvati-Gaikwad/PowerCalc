# Serverless Power Calculator (AWS Amplify + API Gateway + Lambda)

A simple **serverless web application** that calculates the power of a number using AWS cloud services.

The user enters a **base** and an **exponent**, and the application returns the calculated result using a backend powered by AWS.

---

# Architecture Overview

This project follows a **serverless architecture** where the frontend interacts with backend AWS services through an API.

```
User → Frontend (Amplify Hosting)
      ↓
API Gateway
      ↓
AWS Lambda
      ↓
DynamoDB (store request/response data)
      ↓
Response returned to Frontend
```

### Services Used

* AWS Amplify – Hosts the frontend web application
* Amazon API Gateway – Provides the REST API endpoint used by the frontend
* AWS Lambda – Executes the backend logic for calculating the power of a number
* Amazon DynamoDB – Stores the calculation inputs and results
* GitHub – Version control and project repository

---

# Step 1: Create the Frontend Application

A simple **HTML + JavaScript frontend** was created to allow users to input:

* Base number
* Exponent number

When the **Calculate** button is clicked, the application sends a request to the backend API.

<img width="2880" height="1448" alt="image" src="https://github.com/user-attachments/assets/742dc5d3-beaf-4a37-ab7a-60b082724c78" />

---

# Step 2: Create an AWS Lambda Function

A Lambda function was created to handle the power calculation logic.

The Lambda function performs the following actions:

1. Receives input from API Gateway
2. Extracts the base and exponent values
3. Calculates the result
4. Stores the result in DynamoDB
5. Returns the response in JSON format

### Example Lambda Logic

```
result = base ** exponent
```

<img width="2880" height="1523" alt="image" src="https://github.com/user-attachments/assets/2a5eb9ac-4bfb-422c-9000-7cb4c62a494b" />

---

# Step 3: Create API Gateway Endpoint

An API endpoint was created to connect the frontend with the Lambda function.

### Steps performed

1. Created a new REST API
2. Added a **POST method**
3. Connected the method to the Lambda function
4. Deployed the API to the **dev stage**

<img width="2853" height="974" alt="image" src="https://github.com/user-attachments/assets/5a409cba-62ae-44fc-a458-e8cad0c4f50f" />

<img width="2848" height="1064" alt="image" src="https://github.com/user-attachments/assets/267cae82-0f1a-4612-ad2e-d3bde9a8a496" />

---

# Step 4: Enable CORS

Since the frontend is hosted on a different domain, **CORS (Cross-Origin Resource Sharing)** needed to be enabled.

### Actions performed

* Enabled CORS in API Gateway
* Added required headers
* Redeployed the API

This allows the frontend hosted on Amplify to communicate with the backend API without browser restrictions.

<img width="2879" height="1358" alt="image" src="https://github.com/user-attachments/assets/dd29089d-5bbf-48f2-bf48-a97e3f6f9bc0" />

---

# Step 5: Connect Frontend to API

The frontend JavaScript was updated to send a **POST request** to the API endpoint.

### Request Body

```
{
  "base": value,
  "exponent": value
}
```

The API processes the request using Lambda and returns the calculated result, which is then displayed on the frontend.

<img width="1465" height="823" alt="image" src="https://github.com/user-attachments/assets/fecc0484-0e45-47da-a473-0ee3f55b9771" />

---

# Step 6: Store Results in DynamoDB

To persist calculation data, a **DynamoDB table** was created.

The Lambda function stores the following information in the database:

* Base value
* Exponent value
* Calculated result
* Timestamp of the request

### Example Stored Record

```
{
  "base": 2,
  "exponent": 3,
  "result": 8
}
```

This allows the system to **store calculation history and enables future analytics or tracking**.

<img width="2880" height="1530" alt="image" src="https://github.com/user-attachments/assets/d415fb0d-04fd-4186-8877-1ed6aeba2ea6" />


---

# Step 7: Deploy Frontend Using AWS Amplify

The frontend application was deployed using Amplify Hosting.

### Deployment Steps

1. Uploaded the frontend files
2. Created a new Amplify app
3. Connected the GitHub repository
4. Deployed the application

Amplify automatically generated a **public URL** for accessing the application.

<img width="2880" height="1454" alt="image" src="https://github.com/user-attachments/assets/b53b80b4-a33a-43b1-b089-b4f8261e3fbd" />

<img width="2879" height="1308" alt="image" src="https://github.com/user-attachments/assets/0e8558c7-7c15-4672-affb-5c781384c567" />

---

# Step 8: Test the Application

The application was tested by entering different base and exponent values.

### Example Test

```
Base: 2
Exponent: 3
Result: 8
```

### Request Flow

```
Frontend → API Gateway → Lambda → DynamoDB → Response
```

<img width="2879" height="646" alt="image" src="https://github.com/user-attachments/assets/89882c9d-0524-42c0-8bde-2f5264dc3f7d" />

---

# Final Result

The serverless application successfully performs power calculations using AWS cloud services.

### Key Benefits

* No server management
* Fully scalable
* Cost efficient
* Event-driven computing

---

# Repository Structure

```
project-folder
│
├── index.html
├── script.js
└── README.md
```

---

# Future Improvements

Possible enhancements:

* Add input validation
* Improve UI styling
* Implement calculation history using DynamoDB queries
* Add authentication using Amazon Cognito
* Build a dashboard to visualize stored calculations

---

# Author

Created as part of a **serverless AWS learning project** to demonstrate how multiple AWS services can be combined to build scalable cloud applications.

---
