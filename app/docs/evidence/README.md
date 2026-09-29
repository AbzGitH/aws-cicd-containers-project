# Project Evidence

This folder contains selected evidence demonstrating the successful implementation of the CI/CD and container deployment workflow.

## ECS Environment Verification

![Environment services active](screenshots/development-environment-active.png)

![ECS environment CLI verification](screenshots/ecs-environments-cli-verification.png)

**What it shows:**
Development, UAT/Staging and Production ECS services are active and running successfully, verified through both the AWS Console and AWS CLI.

**What it proves:**
The project implements separate deployment environments and confirms their healthy state through two independent verification methods.

## Amazon ECR Verification

The `cloud-cicd-app` Amazon ECR repository stores the container images produced by the CI/CD pipeline.

![Amazon ECR container image](screenshots/ecr-container-image.png)

The AWS Console confirms that multiple container images were pushed successfully, with image tags, digests, creation timestamps and image sizes visible.

![Amazon ECR CLI verification](screenshots/ecr-cli-image-verification.png)

The AWS CLI independently confirms that the repository contains image records with digests and push timestamps.

**What this proves:**
The pipeline successfully publishes Docker images to Amazon ECR, where they are stored and made available for deployment to Amazon ECS/Fargate.

## CI/CD Automation

![GitHub Actions CI build steps](screenshots/github-actions-ci-build-steps-success.png)

The GitHub Actions workflow completed the automated CI stages successfully, including checkout, validation, Docker image build and container testing.

![Production approval gate](screenshots/production-approval-gate-waiting.png)

The deployment pipeline paused at the Production environment and required manual approval before release.

![Production deployment approval review](screenshots/production-deployment-approval-review.png)

The Production deployment review confirms that the release was explicitly approved before the deployment continued.

![Production application verification](screenshots/production-application-verification.png)

The deployed application was then verified successfully through the Production Application Load Balancer endpoint.

**What it proves:**
The project implements an automated CI/CD workflow that builds and validates the application, enforces a manual Production approval gate, deploys the approved release, and successfully serves the updated application in AWS.
