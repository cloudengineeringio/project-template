# TaskMaster: Serverless Todo List

Your manager gave you a task to design and implement a complete solution using AWS services.  
You are expected to plan, build, and validate the solution following best practices — step by step.

# Details

| Property | Value |
|---|---|
| **Difficulty** | Advanced |
| **Provider** | AWS |
| **Estimate** | 4–10 hours |
| **Labels** | Serverless, API, Compute, Data, Storage, Monitoring, Auth |

# Tech Stack

- [AWS Lambda](https://docs.aws.amazon.com/lambda/)
- [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/)
- [Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb/)
- [Amazon S3](https://docs.aws.amazon.com/s3/)
- [AWS IAM](https://docs.aws.amazon.com/iam/)
- [Amazon CloudWatch](https://docs.aws.amazon.com/cloudwatch/)
- [AWS Cognito](https://docs.aws.amazon.com/cognito/)
- [Amazon VPC](https://docs.aws.amazon.com/vpc/)

# Prerequisites

Before starting this project, make sure that:
- You have an AWS Account, if not create one with [AWS Account (Free Tier)](https://aws.amazon.com/free) that will cost you nothing
- You are familiar with the AWS Management Console and basic CLI operations
- You understand IAM roles and policies fundamentals
- You have AWS CLI installed and configured locally
- You have basic knowledge of JSON and YAML syntax
- You know how to interpret architecture diagrams
- You are familiar with basics of user authentication

# Project Overview

Your manager assigned you to design and deploy a serverless todo list application that allows logged-in users to create, retrieve, update, and delete tasks. This fully functional application will demonstrate a modern serverless architecture pattern using AWS services. The todo list will allow users to add task descriptions, set due dates, mark items as complete, and filter/sort their tasks.

**What You'll Build:**  
A fully functional serverless todo list application with a RESTful API backed by serverless functions and a NoSQL database, eventually adding a web frontend.

## Key Components

<table>
<tr>
<th>Component</th>
<th>Purpose</th>
<th>Technology</th>
</tr>
<tr>
<td>API Layer</td>
<td>Handles HTTP requests</td>
<td>Amazon API Gateway</td>
</tr>
<tr>
<td>Business Logic</td>
<td>Processes task operations (CRUD)</td>
<td>AWS Lambda with Lambda Powertools</td>
</tr>
<tr>
<td>Data Storage</td>
<td>Stores task information</td>
<td>Amazon DynamoDB (Single Table Design)</td>
</tr>
<tr>
<td>Network</td>
<td>Secure environment for Lambda functions</td>
<td>Amazon VPC with Endpoints</td>
</tr>
<tr>
<td>Frontend</td>
<td>User interface for the todo list</td>
<td>HTML, CSS, JavaScript hosted on S3</td>
</tr>
<tr>
<td>Authentication</td>
<td>Manages user identity and access</td>
<td>AWS Cognito</td>
</tr>
<tr>
<td>Monitoring</td>
<td>Tracks application performance</td>
<td>Amazon CloudWatch</td>
</tr>
</table>

# Architecture

The TaskMaster application follows a serverless architecture pattern where each component is fully managed by AWS. Lambda functions will run within a VPC for enhanced security, communicating with DynamoDB through a VPC endpoint. API Gateway will use Lambda Proxy integration to pass the full request to Lambda functions, allowing more flexibility in request handling.

The DynamoDB table will follow a single-table design pattern, where all application entities and relationships are stored in one table. This approach leverages DynamoDB's key schema and indexing capabilities to enable complex access patterns while minimizing the number of database operations needed.

## API Endpoints

<table>
<tr>
<th>Method</th>
<th>Endpoint</th>
<th>Description</th>
<th>Status Code</th>
<th>Response</th>
</tr>
<tr>
<td><strong>GET</strong></td>
<td><code>/tasks</code></td>
<td>List all tasks for the user</td>
<td>200</td>
<td>Array of task objects</td>
</tr>
<tr>
<td><strong>GET</strong></td>
<td><code>/tasks/{id}</code></td>
<td>Get a specific task</td>
<td>200, 404</td>
<td>Single task object</td>
</tr>
<tr>
<td><strong>POST</strong></td>
<td><code>/tasks</code></td>
<td>Create a new task</td>
<td>201</td>
<td>Created task object with ID</td>
</tr>
<tr>
<td><strong>PUT</strong></td>
<td><code>/tasks/{id}</code></td>
<td>Update an existing task</td>
<td>200, 404</td>
<td>Updated task object</td>
</tr>
<tr>
<td><strong>DELETE</strong></td>
<td><code>/tasks/{id}</code></td>
<td>Delete a task</td>
<td>204, 404</td>
<td>No content</td>
</tr>
<tr>
<td><strong>GET</strong></td>
<td><code>/tasks/status/{status}</code></td>
<td>Filter tasks by status</td>
<td>200</td>
<td>Array of filtered task objects</td>
</tr>
<tr>
<td><strong>GET</strong></td>
<td><code>/tasks/due/{date}</code></td>
<td>Get tasks due by date</td>
<td>200</td>
<td>Array of task objects</td>
</tr>
</table>

> **Diagram to Draw:**  
> Include components showing the flow from API Gateway, to Lambda functions in VPC that interact with DynamoDB through VPC endpoint. Show Cognito for authentication and CloudWatch for monitoring.

![Architecture](images/diagram.png "Architecture diagram")

# Learning Objectives

After completing this project, you will be able to:
- Design and implement a serverless application using multiple AWS services
- Create and configure RESTful APIs using Amazon API Gateway with Lambda Proxy integration
- Implement AWS Lambda Powertools for logging, tracing, and metrics
- Design a DynamoDB single-table architecture for efficient data access
- Configure Lambda functions to run within a VPC with appropriate security
- Set up VPC endpoints for secure service access
- Implement user authentication with Amazon Cognito
- Configure appropriate IAM roles and policies
- Monitor application performance using CloudWatch
- Deploy a static website to Amazon S3


# Success Criteria

To successfully complete this project:
- All API endpoints are properly secured and functioning
- Lambda functions are deployed in a VPC with appropriate security
- Each Lambda function was tested individually before moving to the next
- Data is correctly stored and retrieved from DynamoDB using single-table design
- Authentication is working correctly with Cognito
- Lambda Powertools are implemented for logging, metrics, and tracing
- The application has appropriate error handling and input validation
- A functional frontend allows users to manage tasks through a web interface
- The architecture follows serverless best practices
- All AWS resources are properly cleaned up after completion

# Bonus Challenges

Want to take it further? Try one or more of these:
- Implement task categories or tags using DynamoDB's secondary indexes
- Add due dates and reminder notifications using EventBridge and SNS
- Create a CI/CD pipeline using AWS CodePipeline for automated deployment
- Implement Infrastructure as Code using AWS CDK or SAM
- Add a GraphQL API using AWS AppSync as an alternative interface
- Implement task sharing capabilities between users
- Add real-time updates using WebSockets API and Lambda
- Implement CloudFront distribution for the frontend for better performance
- Perform advanced load testing using Apache JMeter for comprehensive performance analysis

# Resources

Useful AWS documentation and learning materials:
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [AWS Lambda Powertools Python](https://awslabs.github.io/aws-lambda-powertools-python/latest/)
- [Lambda Proxy Integration Response Format](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html#api-gateway-simple-proxy-for-lambda-output-format)
- [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [DynamoDB Single Table Design](https://www.alexdebrie.com/posts/dynamodb-single-table/)
- [Amazon DynamoDB Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [VPC Endpoints for AWS Services](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html)
- [AWS Cognito Developer Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [Amazon S3 Static Website Hosting](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html)