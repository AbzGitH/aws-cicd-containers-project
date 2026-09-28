# Environment Setup Reference

## Environment Flow

Development → UAT/Staging → Production

### Development Environment

A separate ECS task definition and service were created for Development so changes can be tested independently before promotion.

Development resources:

- Task definition family: `cloud-cicd-dev-task`
- Task definition revision: `1`
- ECS service: `cloud-cicd-dev-service`
- ECS cluster: `cloud-cicd-cluster`
- Region: `eu-west-2`

The Development environment reuses the existing VPC, subnets, security group and ECR repository to keep the project cost-efficient while maintaining deployment separation.

Current flow:

Development → UAT/Staging → Production

### Development Setup Completed

These steps created an independent Development deployment path while reusing shared infrastructure to keep the environment simple and cost-efficient.

- Created `ecs-task-definition-dev.json` from the existing task definition.
- Changed the task family to `cloud-cicd-dev-task`.
- Registered `cloud-cicd-dev-task:1`.
- Created `cloud-cicd-dev-service`.
- Verified the Development service is `ACTIVE`.

### UAT / Staging Environment

A separate ECS task definition and service were created for UAT/Staging so release candidates can be validated before Production.

UAT resources:

- Task definition family: `cloud-cicd-uat-task`
- Task definition revision: `1`
- ECS service: `cloud-cicd-uat-service`
- ECS cluster: `cloud-cicd-cluster`
- Region: `eu-west-2`

The UAT environment reuses the existing VPC, subnets, security group and ECR repository to keep the project cost-efficient while maintaining deployment separation.

### Production Promotion Gate

Production deployment should only happen after:

- Development validation passes.
- UAT/Staging validation passes.
- Manual approval is given for Production.
