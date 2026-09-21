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
