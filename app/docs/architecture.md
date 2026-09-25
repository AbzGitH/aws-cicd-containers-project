# Project 3 — CI/CD & Containers Architecture

## Architecture Overview

This project demonstrates a containerised application deployed to AWS through an automated CI/CD pipeline.

The target deployment flow is:

Developer → GitHub → GitHub Actions → Docker → Amazon ECR → Amazon ECS/Fargate → Running Application

## Architecture Components

- **GitHub** — Stores the application source code and project history.
- **GitHub Actions** — Runs the CI/CD automation when changes are pushed to the repository.
- **Docker** — Packages the application and its required environment into a portable container image.
- **Amazon ECR** — Stores the Docker container images in AWS.
- **Amazon ECS** — Orchestrates and manages the running containerised application.
- **AWS Fargate** — Provides the compute capacity for the ECS containers without requiring us to manage EC2 servers.

## Environment Workflow

Application changes will move through the following environments:

Development → UAT/Staging → Production

- **Development** — Changes are built and tested during active development.
- **UAT/Staging** — Changes are validated in a production-like environment before release.
- **Production** — Approved changes are deployed to the live application.

## Application Scope

The application is a lightweight static web application consisting of HTML and CSS.

Its purpose is to provide a simple workload that can be containerised with Docker and deployed through the project's automated CI/CD pipeline.

The application itself is intentionally minimal so the project can focus on containerisation, AWS deployment, automation, environment promotion, and operational practices.

## Deployment Workflow

1. **Development** — Application changes are developed and tested locally.
2. **UAT/Staging** — Validated changes are deployed for pre-production testing.
3. **Production** — Changes that pass validation are promoted to the live environment.

The CI/CD pipeline will automate this progression while maintaining validation gates between environments.

## AWS Deployment and Cost Considerations

The AWS deployment will use Amazon ECR to store the Docker container image and Amazon ECS with AWS Fargate to run the containerised application.

The project will use the eu-west-2 (London) region. AWS identity and region will be verified before infrastructure is created.

To keep the project cost-efficient, only the resources required to demonstrate the CI/CD architecture will be deployed. Chargeable runtime resources, particularly ECS/Fargate workloads, will be stopped or removed when they are no longer required.

Amazon ECR storage will also be kept minimal by retaining only the container images required for the project.

## Implemented AWS Infrastructure

- **Amazon ECR** — Stores the Docker container image.
- **Amazon ECS** — Manages the container workload through the `cloud-cicd-cluster`.
- **AWS Fargate** — Runs the container without managing EC2 servers.
- **ECS Task Definition** — Defines the container image, CPU, memory and runtime configuration.
- **Security Group** — Allows temporary inbound HTTP traffic on TCP port 80.
- **Public Networking** — The Fargate task receives a public IP for deployment verification.

### Deployment Verification

The containerised application was successfully deployed to AWS Fargate and accessed through the task's public IP address over HTTP.

After verification, the Fargate task was stopped to avoid unnecessary runtime costs.

### Troubleshooting

The initial Fargate deployment failed because the Docker image was built for ARM64 while the ECS task required AMD64 (`linux/amd64`).

The image was rebuilt for `linux/amd64`, pushed to Amazon ECR, and the Fargate deployment was successfully repeated.

### Planned Improvement

Add an Application Load Balancer (ALB) in front of the ECS service to provide a stable public endpoint across task replacements and deployments.
