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
- [AWS Lambda Powertools](https://awslabs.github.io/aws-lambda-powertools-python/latest/)
- [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/)
- [Amazon DynamoDB](https://docs.aws.amazon.com/dynamodb/)
- [Amazon S3](https://docs.aws.amazon.com/s3/)
- [AWS IAM](https://docs.aws.amazon.com/iam/)
- [Amazon CloudWatch](https://docs.aws.amazon.com/cloudwatch/)
- [AWS Cognito](https://docs.aws.amazon.com/cognito/)
- [Amazon VPC](https://docs.aws.amazon.com/vpc/)

# Prerequisites

Before starting this project, make sure that:
- You have an active [AWS Account (Free Tier)](https://aws.amazon.com/free)
- You are familiar with the AWS Management Console and basic CLI operations
- You understand IAM roles and policies fundamentals
- You have AWS CLI installed and configured locally
- You have basic knowledge of JSON and YAML syntax
- You know how to interpret architecture diagrams
- You are familiar with basics of user authentication

# Project Overview

Your manager assigned you to design and deploy a serverless todo list application that allows logged-in users to create, retrieve, update, and delete tasks. This fully functional application will demonstrate a modern serverless architecture pattern using AWS services. The todo list will allow users to add task descriptions, set due dates, mark items as complete, and filter/sort their tasks.

The project follows a standard CRUD (Create, Read, Update, Delete) pattern and serves as an excellent introduction to building serverless applications that can scale automatically based on demand without maintaining any servers.

**What You'll Build:**  
A fully functional serverless todo list application with a RESTful API backed by serverless functions and a NoSQL database, eventually adding a web frontend.

## Key Components

| Component | Purpose | Technology |
|---|---|---|
| API Layer | Handles HTTP requests | Amazon API Gateway |
| Business Logic | Processes task operations (CRUD) | AWS Lambda with Lambda Powertools |
| Data Storage | Stores task information | Amazon DynamoDB (Single Table Design) |
| Network | Secure environment for Lambda functions | Amazon VPC with Endpoints |
| Frontend | User interface for the todo list | HTML, CSS, JavaScript hosted on S3 |
| Authentication | Manages user identity and access | AWS Cognito |
| Monitoring | Tracks application performance | Amazon CloudWatch |

# Architecture

The TaskMaster application follows a serverless architecture pattern where each component is fully managed by AWS. Lambda functions will run within a VPC for enhanced security, communicating with DynamoDB through a VPC endpoint. API Gateway will use Lambda Proxy integration to pass the full request to Lambda functions, allowing more flexibility in request handling.

The DynamoDB table will follow a single-table design pattern, where all application entities and relationships are stored in one table. This approach leverages DynamoDB's key schema and indexing capabilities to enable complex access patterns while minimizing the number of database operations needed.

## API Endpoints

| Method | Endpoint | Description | Status Code | Response |
|---|---|---|---|---|
| **GET** | `/tasks` | List all tasks for the user | 200 | Array of task objects |
| **GET** | `/tasks/{id}` | Get a specific task | 200, 404 | Single task object |
| **POST** | `/tasks` | Create a new task | 201 | Created task object with ID |
| **PUT** | `/tasks/{id}` | Update an existing task | 200, 404 | Updated task object |
| **DELETE** | `/tasks/{id}` | Delete a task | 204, 404 | No content |
| **GET** | `/tasks/status/{status}` | Filter tasks by status | 200 | Array of filtered task objects |
| **GET** | `/tasks/due/{date}` | Get tasks due by date | 200 | Array of task objects |

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

# Tasks

Each phase focuses on a separate part of the project.  
You will implement components gradually, testing after each phase.

## Phase 1: Foundation Setup

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-01** | **DynamoDB Table Setup**<br/>Create a DynamoDB table following single-table design principles. The table should use a composite primary key with PK (partition key) for user/task identification and SK (sort key) for item type or metadata. Create GSIs (Global Secondary Indexes) for querying tasks by status and due date. In a single-table design, all application data is stored in one table rather than separate tables for different entity types, which reduces API calls, maintains transactional integrity, simplifies scaling, and improves cost efficiency.<br/><br/>**💡 Hint:** Before creating the table, list all access patterns (single table design requirement).<br/><br/>Document your key design (e.g., PK format: "USER#<userId>", SK format: "TASK#<taskId>").<br/><br/>**📝 Note:** Initially treat this as a system without users - users will be added in the authentication phase. | ⬜ |
| **TASK-02** | **VPC Setup**<br/>Create a VPC with private subnets for Lambda functions. The VPC should have at least two private subnets across different availability zones for high availability. No public subnets are needed as Lambda functions will communicate with AWS services via VPC endpoints. | ⬜ |
| **TASK-03** | **VPC Endpoint Configuration**<br/>Set up a VPC endpoint for DynamoDB. This endpoint will allow Lambda functions in your private VPC to securely connect to DynamoDB without going through the public internet, enhancing security. | ⬜ |

## Phase 2: API Gateway Setup

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-04** | **API Gateway Structure**<br/>Create an API Gateway REST API with the complete resource structure. Define all resources: `/tasks`, `/tasks/{id}`, `/tasks/status/{status}`, and `/tasks/due/{date}`. Create methods (**GET**, **POST**, **PUT**, **DELETE**) for each resource according to the API endpoints table. Do NOT set up integrations yet - just create the API structure. This gives you the endpoint structure that your Lambda functions need to match. | ⬜ |
| **TASK-05** | **Mock Lambda Function**<br/>Create a mock Lambda function that returns a sample response. This function will help you understand the required response structure for Lambda Proxy integration. The function should return a response with statusCode, headers (including CORS headers), and a body (JSON stringified). Test this mock function directly in the Lambda console to verify the response format. Example response structure: `{"statusCode": 200, "headers": {"Content-Type": "application/json", "Access-Control-Allow-Origin": "*"}, "body": "{\"message\": \"Hello from Lambda\"}"}` | ⬜ |
| **TASK-06** | **Lambda Proxy Integration**<br/>Set up Lambda Proxy integration for one test endpoint (**GET** `/tasks`). Connect your mock Lambda function to the **GET** `/tasks` method using Lambda Proxy integration. Deploy the API to a test stage. Test the endpoint using the AWS console test feature or curl to verify the integration works and you understand the request/response format. | ⬜ |

## Phase 3: Build Lambda Functions Incrementally

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-07** | **IAM Role Setup**<br/>Set up the Lambda execution role and basic IAM policies. Create an IAM role for Lambda execution that includes permissions to create logs in CloudWatch, create network interfaces in VPC (EC2 permissions), and basic DynamoDB access. This role will be used by all your Lambda functions. Document the permissions granted. | ⬜ |
| **TASK-08** | **List Tasks Function**<br/>Implement the "List Tasks" Lambda function (**GET** `/tasks`). Create a new Lambda function that queries DynamoDB for all tasks belonging to a user. Use AWS Lambda Powertools for structured logging. Configure the function to run in your VPC. The function should parse the user ID from the request context (we'll add real authentication later, for now use a test user ID). Return tasks in the proper Lambda Proxy format. Deploy and test this function through API Gateway. | ⬜ |
| **TASK-09** | **Create Task Function**<br/>Implement the "Create Task" Lambda function (**POST** `/tasks`). Create a Lambda function that accepts task data in the request body, validates the input, generates a unique task ID, and stores it in DynamoDB. Include proper error handling for invalid input. Use Lambda Powertools for logging and metrics. Configure to run in VPC. Test through API Gateway by creating a task and verifying it appears in DynamoDB. | ⬜ |
| **TASK-10** | **Get Task by ID Function**<br/>Implement the "Get Task by ID" Lambda function (**GET** `/tasks/{id}`). Create a function that retrieves a specific task by its ID from DynamoDB. Handle the case where the task doesn't exist (return 404). Parse the task ID from the path parameters. Test through API Gateway with both valid and invalid task IDs. | ⬜ |
| **TASK-11** | **Update Task Function**<br/>Implement the "Update Task" Lambda function (**PUT** `/tasks/{id}`). Create a function that updates an existing task with new data. Validate that the task exists before updating. Handle partial updates (only update fields that are provided). Return the updated task. Test through API Gateway by updating a task's status or description. | ⬜ |
| **TASK-12** | **Delete Task Function**<br/>Implement the "Delete Task" Lambda function (**DELETE** `/tasks/{id}`). Create a function that deletes a task from DynamoDB. Return 204 (No Content) on success or 404 if the task doesn't exist. Test through API Gateway by deleting a task and verifying it's removed from DynamoDB. | ⬜ |
| **TASK-13** | **Filtering Functions**<br/>Implement filtering functions (**GET** `/tasks/status/{status}` and **GET** `/tasks/due/{date}`). Create Lambda functions that use DynamoDB GSIs to filter tasks by status or due date. These functions should demonstrate how to query using secondary indexes. Test both endpoints through API Gateway with various filter values. | ⬜ |

## Phase 4: Enhanced Monitoring and Error Handling

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-14** | **Enhanced Logging**<br/>Implement comprehensive logging with Lambda Powertools. Update all Lambda functions to use structured logging with correlation IDs. Add custom metrics for operation counts and latencies. Ensure all error cases are properly logged with context. | ⬜ |
| **TASK-15** | **X-Ray Tracing**<br/>Set up X-Ray tracing for request flow visualization. Enable X-Ray tracing on API Gateway and all Lambda functions. Use Lambda Powertools' tracing decorator to instrument your functions. Create a test scenario and view the service map in X-Ray console to understand the request flow. | ⬜ |
| **TASK-16** | **CloudWatch Dashboard**<br/>Create a CloudWatch dashboard for monitoring. Build a dashboard with widgets showing Lambda invocations, errors, duration, API Gateway request counts, latency, DynamoDB consumed capacity, and custom metrics. This dashboard should give you complete visibility into your application's health. | ⬜ |
| **TASK-17** | **Input Validation**<br/>Implement input validation and error handling. Add request validators in API Gateway for request bodies and parameters. Enhance Lambda functions with comprehensive error handling, returning appropriate HTTP status codes (400 for bad requests, 404 for not found, 500 for server errors). Test error scenarios through API Gateway. | ⬜ |

## Phase 5: Add Authentication

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-18** | **Cognito User Pool**<br/>Set up Amazon Cognito User Pool for authentication. Configure a User Pool with appropriate password policies, MFA settings (optional), and required attributes (email, name). Create an app client for your API. Set up email verification for user registration. Document the User Pool ID and App Client ID. | ⬜ |
| **TASK-19** | **API Gateway Authorization**<br/>Configure API Gateway to use Cognito authorizers. Create a Cognito User Pool authorizer for your API. Apply the authorizer to all API methods. Update CORS configuration to allow the Authorization header. | ⬜ |
| **TASK-20** | **JWT Token Integration**<br/>Update Lambda functions to extract user information from JWT tokens. Modify all Lambda functions to read the user ID from the Cognito JWT token passed in the request context. This ensures tasks are associated with the correct user. Test by creating a test user in Cognito and making authenticated API calls. | ⬜ |
| **TASK-21** | **Authentication Testing**<br/>Test the complete authenticated flow. Register a test user through Cognito. Obtain JWT tokens using the authentication flow. Test all API endpoints with the Authorization header containing the JWT token. Verify that unauthenticated requests are rejected and authenticated requests properly associate tasks with the user. | ⬜ |

## Phase 6: Frontend Implementation

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-22** | **S3 Static Hosting**<br/>Create an S3 bucket for static website hosting. Configure the bucket for static website hosting with appropriate bucket policies. Set up CORS configuration to allow requests from your API. Configure index and error documents. | ⬜ |
| **TASK-23** | **Frontend Structure**<br/>Develop the frontend HTML/CSS structure. Create a responsive UI with components for login/signup, task listing, task creation form, and task management (edit/delete). Style the interface to be user-friendly and professional. No JavaScript functionality yet - just the structure and styling. | ⬜ |
| **TASK-24** | **Frontend Authentication**<br/>Implement Cognito authentication in the frontend. Integrate the Cognito JavaScript SDK or Amazon Amplify for authentication. Create signup, signin, and signout flows. Implement token storage and management. Test the authentication flow independently before connecting to the API. | ⬜ |
| **TASK-25** | **API Integration**<br/>Connect frontend to API endpoints. Implement JavaScript functions to call all API endpoints with proper authentication headers. Add functionality to display tasks, create new tasks, update task status, and delete tasks. Implement client-side filtering and sorting. Test the complete flow from login to task management. | ⬜ |
| **TASK-26** | **Complete Application Testing**<br/>Deploy and test the complete application. Upload the frontend files to S3. Verify the website is accessible. Test the complete user journey from registration to task management. Verify all features work correctly end-to-end. | ⬜ |

## Phase 7: Performance and Optimization

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-27** | **CloudWatch Alarms**<br/>Set up CloudWatch alarms for critical metrics. Create alarms for API errors (4xx/5xx rates), Lambda errors and throttling, DynamoDB throttling, and high latency. Configure SNS notifications for alarm triggers. | ⬜ |
| **TASK-28** | **Load Testing**<br/>Perform load testing. Use a tool like Artillery to simulate multiple concurrent users performing various operations. Monitor CloudWatch metrics during the test. Identify any performance bottlenecks or errors under load. | ⬜ |
| **TASK-29** | **Performance Optimization**<br/>Optimize based on performance data. Analyze CloudWatch metrics and X-Ray traces to identify optimization opportunities. Adjust Lambda memory allocation, timeout settings, and DynamoDB provisioned capacity based on actual usage patterns. Re-test after optimizations. | ⬜ |

## Phase 8: Cleanup and Documentation

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-30** | **Architecture Documentation**<br/>Document the complete architecture and setup. Create a comprehensive README.md with architecture diagram, component descriptions, API documentation, setup instructions, and configuration details. Include example requests and responses for each API endpoint. | ⬜ |
| **TASK-31** | **Application Demonstration**<br/>Create a demonstration of the application. Prepare a demonstration script showcasing all key features. Record a short video or prepare a live demo showing user registration, authentication, and all task management features. | ⬜ |
| **TASK-32** | **Resource Cleanup**<br/>Clean up all AWS resources. Delete resources in the correct order to avoid dependency conflicts: API Gateway, Lambda functions, VPC endpoints, VPC (including subnets and security groups), DynamoDB table, S3 bucket contents and bucket, Cognito User Pool, CloudWatch logs and dashboards, IAM roles and policies. Verify all resources are removed to prevent unexpected charges. | ⬜ |

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