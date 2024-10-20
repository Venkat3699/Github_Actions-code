# Terraform CI/CD Pipeline with GitHub Actions

This repository contains a GitHub Actions pipeline to automate the deployment and management of infrastructure using Terraform. 

# The pipeline includes the following steps:
1. Terraform Initialization
2. Terraform Plan
3. Approval Process (for production deployments)
4. Terraform Apply (on main branch)

The workflow is triggered on push and pull_request events, and the actual infrastructure changes (terraform apply) require manual approval from a designated reviewer before execution in the production environment.

# Pipeline Overview
The GitHub Actions pipeline is defined in .github/workflows/terraform.yml.

# Workflow Steps
1. Checkout Code: The pipeline checks out the repository to ensure access to the Terraform files.
2. Set Up Terraform: It installs the specified version of Terraform.
3. Terraform Init: Initializes the working directory that contains the Terraform configuration files.
4. Terraform Plan: Generates an execution plan that details the changes Terraform will make without applying them.
5. Approval Process: When changes are detected, the terraform apply step is held until a manager (or designated reviewer) approves the changes.
6. Terraform Apply: After approval, the pipeline applies the changes to the infrastructure.

# Trigger Events
The pipeline is triggered on the following events:

1. push: When code is pushed to the main branch.
2. pull_request: When a pull request is opened or updated targeting the main branch.

# Requirements
To run this pipeline, you need:

1. Terraform: Ensure you have Terraform configurations in a directory, specified in the workflow (TF_WORKING_DIR).

2. GitHub Secrets: The pipeline assumes the presence of required secrets (e.g., AWS credentials) to execute Terraform scripts. 

# Add the following secrets in your repository:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
Or other cloud provider credentials based on your infrastructure.

# Approval Permissions: To enforce approval, set up GitHub Environments for the terraform apply step. Ensure that the manager or reviewer is assigned in the environment settings under repository Settings > Environments.