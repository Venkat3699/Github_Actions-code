# Java Application CI/CD Pipeline

This repository contains a complete CI/CD pipeline for a Java application, managed through GitHub Actions. The pipeline automates the process of building, testing, scanning, and deploying the application to production using Docker, SonarQube, JFrog Artifactory, and a self-hosted EC2 runner.

## Overview

The pipeline performs the following steps:
1. **Checkout**: Pulls the latest code from the `main` branch.
2. **Compile**: Builds the Java application using Maven.
3. **Unit Testing**: Runs unit tests to ensure code quality.
4. **SonarQube Scan**: Performs static code analysis using SonarQube.
5. **Artifact Packaging**: Packages the application into a JAR file.
6. **Upload to JFrog Artifactory**: Publishes the artifact (JAR file) to JFrog Artifactory.
7. **Docker Build**: Creates a Docker image of the application.
8. **Docker Tag and Push**: Tags the image with the commit SHA and pushes it to DockerHub.
9. **Deployment**: Deploys the Docker container to a production EC2 instance using SSH.

## Pipeline Trigger

The pipeline is triggered when a developer pushes code to the `main` branch. No other branches will trigger this workflow.

## File Structure

- `.github/workflows/pipeline.yml`: The GitHub Actions workflow configuration file.
- `src/`: Source code for the Java application.
- `Dockerfile`: Defines how the Docker image is built for the application.

## Prerequisites

1. **GitHub Actions Setup**:
   - The pipeline is designed to run on a self-hosted runner (like an EC2 instance). Make sure the runner is set up and registered with your GitHub repository.
   - Secrets for DockerHub, JFrog, SonarQube, and SSH access must be configured in the repository settings.

2. **Maven**: Ensure `pom.xml` is properly configured for building and running unit tests.

3. **Docker**: Ensure that Docker is installed and running on the self-hosted runner.

4. **SonarQube**: Ensure SonarQube is set up and accessible for code scanning.

5. **JFrog Artifactory**: Ensure that you have JFrog Artifactory credentials for uploading artifacts.

## Required Secrets

Make sure the following secrets are set up in your GitHub repository:

- `SONAR_TOKEN`: Authentication token for SonarQube.
- `JFROG_USERNAME` and `JFROG_PASSWORD`: Credentials for uploading artifacts to JFrog.
- `DOCKER_USERNAME` and `DOCKER_PASSWORD`: DockerHub credentials to push Docker images.
- `PROD_SERVER_HOST`: The IP or domain of the production EC2 instance.
- `PROD_SERVER_USER`: The SSH user for the production EC2 instance.
- `PROD_SERVER_SSH_KEY`: The private SSH key for accessing the production EC2 instance.
- `PROD_SERVER_SSH_PASSPHRASE`: (Optional) Passphrase for the SSH key if needed.

## Workflow Steps

### 1. Checkout Code
Pulls the latest code from the `main` branch using:
```yaml
- uses: actions/checkout@v3
