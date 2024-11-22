# Flask App CI/CD Pipeline on AWS using CodePipeline, ECS, and Docker

This project sets up a CI/CD pipeline for a Flask web application using **AWS CodePipeline**, **Amazon ECS**, **Amazon ECR**, and **Docker**. The pipeline automates the process of building, testing, and deploying the Flask app to ECS whenever there is a code change in the GitHub repository.

## Prerequisites

Before you start, ensure you have the following:

- **AWS Account**: An active AWS account with appropriate permissions.
- **GitHub Repository**: A GitHub repository containing the Flask application code.
- **Docker**: Installed and configured on your local machine to build and push Docker images.
- **AWS CLI**: Installed and configured with the necessary IAM permissions.
- **AWS CodeBuild**: To build the Docker images.
- **ECS Cluster and Service**: Amazon ECS setup to run the Flask app.
- **ECR Repository**: An Amazon ECR repository to store the Docker images.
- **IAM Roles**: IAM roles for AWS services like CodePipeline, CodeBuild, and ECS to interact with each other.

## Project Setup

### 1. **Create ECR Repository**
To store the Docker images, first create an Amazon ECR repository.

- Go to the **Amazon ECR** Console.
- Create a new repository (e.g., `flask-app-repo`).
- Set up the repository to store your Docker images.

### 2. **Create Docker Image for Flask App**

Ensure your Flask application is containerized using Docker. Here's an example `Dockerfile`:

```Dockerfile
# Use the official Python image from Docker Hub
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copy the Flask application
COPY . .

# Set the Flask environment
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0

# Expose the port the app runs on
EXPOSE 5000

# Start the Flask application
CMD ["flask", "run"]
