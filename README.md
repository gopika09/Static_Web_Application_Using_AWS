# Static Web Application Using AWS

This project demonstrates the deployment of a basic static web application on AWS using **AWS Amplify**, **API Gateway**, **Lambda**, **IAM**, **S3** and **DynamoDB**. The application consists of a static front end, a serverless backend function, an API endpoint for communication, and a DynamoDB table for data persistence.

## Overview :

![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/overview.png)

## Features :

- **Serverless Architecture**: Utilizes AWS Amplify, API Gateway, and Lambda for a fully managed serverless stack.
- **Dynamic API Integration**: RESTful API for handling serverless requests between the web app and the backend.
- **Database Integration**: DynamoDB is used as a NoSQL database for efficient data storage and retrieval.
- **Scalability**: AWS handles scaling automatically, adapting to traffic and performance demands without manual intervention.
- **Cross-Origin Resource Sharing (CORS)**: Enables smooth interaction between the front-end app and backend services.

## Tools and Technologies :

- **AWS Amplify Console**: A continuous deployment and hosting service for web applications.
- **AWS Lambda**: Serverless computing platform for running backend functions without managing servers.
- **API Gateway**: Manages and routes API requests to Lambda functions.
- **DynamoDB**: NoSQL database for low-latency data storage.
- **IAM Policies**: For managing permissions and secure access to AWS resources.
- **HTML and JavaScript**: Used to create the static front end.
- **S3**: Used to store file

## Steps to Deploy :

### 1) Create a Static Web App with AWS Amplify

1. Write a static web app using HTML and JavaScript. Save the file in S3.
2. In the **AWS Amplify Console**, deploy the static web app by uploading the file.
3. Once deployed, go to **Domain Management** in the Amplify Console to retrieve the generated URL.
4. Open the URL in your browser to test the web app.

![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/s3.png)
![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/web%20app.png)

### 2) Build a Serverless Function with AWS Lambda

1. In the **AWS Console**, navigate to **Lambda** and create a new function.
2. Name the function, select Python as the runtime, and complete the setup.
3. Write your Lambda function code, save, and deploy the function.
4. Test the function by running it in the Lambda console to ensure it’s functioning correctly.


### 3) Link Serverless Function to Web App with API Gateway

1. Open **API Gateway Console** and create a new REST API with the protocol as **Edge-optimized**.
2. In the API dashboard, select the root resource (`/`) and choose **Create Method**.
3. Select **POST** as the method, then choose **Lambda Function** as the integration type, and link your Lambda function.
4. Enable **CORS (Cross-Origin Resource Sharing)** for the API:
   - Go to **Actions** and select **Enable CORS**.
   - Select **POST** and click **Enable CORS**.
5. Deploy the API:
   - Go to **Actions** > **Deploy API**.
   - Create a new deployment stage and give it a name.
6. Test the API:
   - Select the **POST** method, and enter a test payload in the request body.
   - Click **Test**; a 200 OK status confirms a successful response.

![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/lambda.png)
  
![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/cors.png)

### 4) Create a Data Table in DynamoDB

1. In the **DynamoDB Console**, click **Create table**.
2. Set the table name and the partition key.
3. Leave other settings as default and create the table. This table will be used to store data that the Lambda function interacts with.

![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/db.png)

### 5) Add IAM Policy to Lambda Function

1. Open the **Configuration** tab in Lambda and go to **Permissions**.
2. Under **Execution role**, click the link to open the IAM role in a new tab.
3. In the **Permissions policies** section, add a new inline policy:
   - Select the **JSON** tab and add the necessary permissions for DynamoDB access.
   - Save the policy to grant your Lambda function permission to interact with DynamoDB.

**Inline Policy :**


```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": "dynamodb:PutItem",
            "Resource": "arn:aws:dynamodb:ap-south-1:533267294631:table/table"
        }
    ]
}
```

### 6) Add Interactivity to the Web App

1. Update `index.html` file to include the API endpoint URL for interactivity.
2. This link will enable the front end to communicate with the Lambda function via API Gateway, allowing users to interact with backend services.

### Results :

Application level:

![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/success%20data.png)

Database level:

![diagram](https://github.com/gopika09/Static_Web_Application_Using_AWS/blob/main/images/table%20data.png)

## Conclusion :

In this project, a serverless web application was deployed using AWS services, showcasing the power of AWS’s serverless architecture. By leveraging AWS Amplify for hosting, Lambda for backend functions, API Gateway for API management, and DynamoDB for data storage, we achieved a scalable, cost-effective solution. This setup enables dynamic functionality without requiring traditional server management, making it ideal for modern applications that prioritize agility and efficiency.
