# Task Management Application

## Task Management Application Overview

The Task Management Application is a comprehensive tool designed to help users efficiently organize, track, and manage their tasks and projects. The application is built using a React frontend and an AWS-based backend, ensuring a scalable, secure, and highly available solution. The application has some keys features that are describe bellow.

Technical Architecture

    Frontend: Built with React, providing a dynamic and responsive user interface.
    Backend: Utilizes AWS services including API Gateway for routing, Lambda for serverless computing, DynamoDB for data storage, and Cognito for user authentication. Deployment: The React app is deployed to S3 and served via CloudFront, ensuring fast content delivery with global edge locations.

This Task Management Application is designed to streamline task management processes, improve productivity, and enhance collaboration, making it an essential tool for individuals and teams alike.

### Key Features

#### 1. User Authentication and Authorization:

    One of the features is the ability to authenticate and authorize users to securely Secure sign-up, login, and logout of the application.
    The authentication systems should give users a personalize view user profile and task

#### 2. Task Management:

    The task management section allows users to create, delete, read and view detailed information about a task.
    It also allows you to organize task into projects

#### 3. Notifications and Reminders:

    The notification feature allows users to receive email or push notifications for task deadlines and updates to ensure timely completion of tasks.

#### 4. Collaboration:

    The Collaboration  feature allows users share  tasks with other users and assign tasks to team members to facilitate collaborative work environments

#### 5 Search and Filtering:

    Search tasks by keywords and apply filters based on status, due date, or project to quickly find relevant tasks.

#### other features to be considered in the feature are

1. Analytics and Reporting:

   Dashboard with visual analytics to provide insights into task progress, completion rates, and overall productivity

2. Third-Party Integration:

   Integrate with calendar apps like Google Calendar for scheduling tasks and communication tools like Slack for notifications

3. Offline Support:

   Access and manage tasks offline with automatic synchronization when reconnected to the internet.

<!-- ====================================== BACKEND ===================================================================================== -->

## Backend:

The backend of the Task Management Application makes use of a number of Amazon Web Services (AWS) in order to develop an architecture that is robust, scalable, and secure. Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and Amazon Cognito are the most important components of this backend architecture. Here is a detailed breakdown of each component function and their interactions:

### 1. Amazon API Gateway:

    API Gateway serves as the entry point for client requests that comes from the frontend. It handles all HTTP requests from the frontend and routes the traffic to the appropriate AWS Lambda function to handle the business logic. The endpoints of the API gate are:

1. /task (POST): Creates a new task.
2. /tasks (GET): Retrieve all tasks for a user.
3. /task/{id} (GET): Retrieve a specific task for a user .
4. /task/{id} (PUT): Update a specific task for a user.
5. /task/{id} (DELETE): Delete a specific task for a user.

Each endpoint or http method is configured to work with a corresponding Lambda function. Cognito User Pool Authorizer is used to secure the endpoints, ensuring that only authenticated users can access the API.

### 2 AWS Lambda:

Lambda functions contain the core business logic for the application. Each Lambda function is triggered by the API Gateway and interacts with DynamoDB to perform CRUD operations.

Functions:

    Create Task Function:
        Trigger: POST request to /task.
        Logic: Parse request body, generate a unique task ID, and store task details in DynamoDB.
    Get Tasks Function:
        Trigger: GET request to /tasks.
        Logic: Query DynamoDB for all tasks associated with the authenticated user.
    Get Task by ID Function:
        Trigger: GET request to /task/{id}.
        Logic: Retrieve a specific task from DynamoDB using the task ID.
    Update Task Function:
        Trigger: PUT request to /task/{id}.
        Logic: Update task details in DynamoDB.
    Delete Task Function:
        Trigger: DELETE request to /task/{id}.
        Logic: Remove the task from DynamoDB.

### 3. Amazon DynamoDB

DynamoDB is a NoSQL database used to store task data. It is chosen for its scalability and performance.

Configuration:

    Table Name: Tasks
    Primary Key: taskId (string, unique for each task)
    Attributes: Additional attributes for each item include userId, taskName, taskDescription, status, and dueDate.

### 4. Amazon Cognito

Amazon Cognito manages user authentication and authorization. It allows users to sign up, log in, and securely access the backend APIs.

Configuration:

    User Pool: Create a user pool to handle user registration and authentication.
    Configure attributes like email, password policies, and multi-factor authentication (if required).
    Cognito User Pool Authorizer: Integrate the user pool with API Gateway to secure the API endpoints.

Steps to Set Up Cognito:

    Create User Pool:
        Go to the Cognito console and create a new user pool.
        Configure sign-up and sign-in options, including required attributes and verification settings.
    Configure App Client:
        Create an app client within the user pool without a client secret (for web applications).
        Note the App Client ID for use in the frontend configuration.
    Set Up Authentication Flow:
        Configure the frontend React app to use AWS Amplify for authentication.
