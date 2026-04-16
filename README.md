# 🏗️ Finpay Technologies — DevOps Project

**Cloud-Native Fintech Platform — Full DevOps Implementation on AWS**

[![AWS](https://img.shields.io/badge/AWS-eu--west--2-FF9900?logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![IaC](https://img.shields.io/badge/IaC-CloudFormation-blue)](https://aws.amazon.com/cloudformation/)
[![ECS](https://img.shields.io/badge/Compute-ECS%20Fargate-orange?logo=amazonaws)](https://aws.amazon.com/fargate/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-CodePipeline%20%2B%20CodeBuild-purple?logo=amazonaws)](https://aws.amazon.com/codepipeline/)
[![PHP](https://img.shields.io/badge/Backend-PHP%208.2-777BB4?logo=php&logoColor=white)](https://www.php.net)
[![Docker](https://img.shields.io/badge/Container-Docker-2496ED?logo=docker&logoColor=white)](https://www.docker.com)
[![API](https://img.shields.io/badge/API-CoinGecko%20Live%20Prices-green)](https://www.coingecko.com/en/api)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## Overview

A fully automated, cloud-native DevOps solution for Finpay Technologies — a fintech platform simulating cryptocurrency wallet management with real-time market data. Built end-to-end on **AWS** using **Infrastructure as Code**, **containerised compute**, and **fully automated CI/CD pipelines**.

The entire infrastructure — VPC, ECS Fargate, ALB, RDS MySQL, IAM roles, Security Groups — is defined in a single **CloudFormation template** and deployed via a dedicated pipeline. The PHP application is containerised with **Docker**, stored in **ECR**, and deployed automatically on every commit. **Auto Scaling** was validated live — scaling from 1 to 4 Fargate tasks under load and back down automatically.

> ⚠️ Infrastructure decommissioned after project completion to manage AWS costs.

---

## Architecture

```
Internet
    │
    ▼
Application Load Balancer (ALB)
    │  Static DNS — distributes traffic, health checks
    ▼
ECS Fargate Service (Auto Scaling: 1–4 tasks)
    │  PHP Application Container (pulled from ECR)
    │  Multi-AZ: eu-west-2a + eu-west-2b
    │                    │
    ▼                    ▼
Amazon RDS MySQL    CoinGecko API
(Users, Wallets,    (Live BTC/ETH
 Transactions)       prices)
```

| Layer | Service | Purpose |
|-------|---------|---------|
| IaC | AWS CloudFormation | Declarative infrastructure provisioning |
| Networking | Amazon VPC + Internet Gateway | Isolated network, public access |
| Networking | Security Groups | Least-privilege traffic control |
| Compute | Amazon ECS Fargate | Serverless container orchestration |
| Registry | Amazon ECR | Docker image storage |
| Load Balancing | Application Load Balancer | Traffic distribution and health checks |
| Database | Amazon RDS MySQL | Relational data persistence |
| Scaling | Application Auto Scaling | CPU-based target tracking (50% threshold) |
| CI/CD | AWS CodePipeline + CodeBuild | Automated infra and app deployment |
| Monitoring | Amazon CloudWatch | Logs, metrics, and alarms |
| Security | AWS IAM | Least-privilege roles and policies |
| External API | CoinGecko | Live cryptocurrency market prices |

---

## Repositories

![Repos](screenshots/infra-repo-main.png)
*Infrastructure repository — main.yml CloudFormation template*

🔗 **Infrastructure:** [SWE7303-Infrastructure](https://github.com/khalidrehman3174/SWE7303-Infrastructure) — CloudFormation IaC, VPC, ECS, RDS, ALB, Auto Scaling

🔗 **Application:** [SWE7303-Application](https://github.com/khalidrehman3174/SWE7303-Application) — PHP app, Dockerfile, buildspec.yml, CoinGecko API

---

## Live Application

![Landing Page](screenshots/landing-page.png)
*Finpay Technologies — live on AWS via Application Load Balancer*

![ALB DNS](screenshots/alb-dns.png)
*Application served via ALB DNS endpoint*

### Application Features

| | |
|---|---|
| ![Signup](screenshots/signup-page.png) | ![Dashboard](screenshots/dashboard.png) |
| *User registration page* | *Dashboard — wallet balances* |
| ![Crypto Prices](screenshots/crypto-prices.png) | ![Transaction History](screenshots/transaction-history.png) |
| *Live CoinGecko API prices — BTC, ETH real-time* | *Transaction history — balance updated* |

| | |
|---|---|
| ![Add Payee](screenshots/add-payee.png) | ![Send Payment](screenshots/send-payment.png) |
| *Adding a new payee* | *Sending payment to registered payee* |

---

## Application Repository

![App Repo](screenshots/app-repo-main.png)
*Application repository — full project structure*

![App Commits](screenshots/app-repo-commits.png)
*Commit history — active development record*

### Dockerfile & Buildspec

| | |
|---|---|
| ![Dockerfile](screenshots/dockerfile.png) | ![Buildspec](screenshots/buildspec.png) |
| *Dockerfile — PHP-Apache base image* | *buildspec.yml — CodeBuild instructions* |

---

## CI/CD Pipelines

Two independent pipelines — infrastructure and application deploy separately, enforcing separation of concerns.

![Pipelines List](screenshots/pipelines-list.png)
*Both pipelines — finpay-infra-pipeline and finpay-app-pipeline — Succeeded*

### Infrastructure Pipeline

| | |
|---|---|
| ![Infra Pipeline](screenshots/infra-pipeline-running.png) | ![Infra Executions](screenshots/infra-pipeline-executions.png) |
| *finpay-infra-pipeline — all stages succeeded* | *Pipeline execution history* |

### Application Pipeline

```
GitHub Push → CodePipeline → CodeBuild → ECR → ECS Rolling Deploy ✅
```

| | |
|---|---|
| ![App Pipeline](screenshots/app-pipeline-detail.png) | ![App Execution](screenshots/app-pipeline-execution.png) |
| *finpay-app-pipeline — Source → Build → Deploy* | *Latest execution — timestamps and results* |

### CodeBuild

| | |
|---|---|
| ![CodeBuild Project](screenshots/codebuild-project.png) | ![CodeBuild History](screenshots/codebuild-history.png) |
| *CodeBuild project* | *Build history — succeeded builds* |

![CodeBuild Phases](screenshots/codebuild-phases.png)
*Build phase detail — all phases succeeded*

---

## Amazon ECR

| | |
|---|---|
| ![ECR Repo](screenshots/ecr-repo.png) | ![ECR Image](screenshots/ecr-image.png) |
| *ECR repository* | *Docker image — latest tag with push timestamp* |

---

## CloudFormation Stack

| | |
|---|---|
| ![CF Stack](screenshots/cloudformation-stack.png) | ![CF Resources 1](screenshots/cloudformation-resources-1.png) |
| *Stack — CREATE_COMPLETE* | *Stack resources — all services provisioned* |

| | |
|---|---|
| ![CF Resources 2](screenshots/cloudformation-resources-2.png) | ![CF Events](screenshots/cloudformation-events.png) |
| *Stack resources — continued* | *Stack events — deployment log* |

---

## ECS Fargate

| | |
|---|---|
| ![ECS Cluster](screenshots/ecs-cluster.png) | ![ECS Service](screenshots/ecs-service.png) |
| *ECS Cluster — Active* | *ECS Service — running tasks* |

![ECS Tasks](screenshots/ecs-tasks.png)
*ECS Tasks — Fargate launch type, Running status*

---

## Application Load Balancer

| | |
|---|---|
| ![ALB List](screenshots/alb-list.png) | ![ALB Detail](screenshots/alb-detail.png) |
| *Load Balancer — Active* | *ALB detail — listeners and AZ configuration* |

![ALB Target Group](screenshots/alb-target-group.png)
*Target Group — healthy targets registered*

---

## Amazon RDS MySQL

| | |
|---|---|
| ![RDS List](screenshots/rds-list.png) | ![RDS Detail](screenshots/rds-detail.png) |
| *RDS MySQL — Available* | *Database detail — engine, VPC, subnet group* |

---

## Networking (VPC, Subnets, IGW)

| | |
|---|---|
| ![VPC](screenshots/vpc.png) | ![Subnets](screenshots/subnets.png) |
| *VPC — Finpay isolated network* | *Two public subnets — eu-west-2a and eu-west-2b* |

![Internet Gateway](screenshots/internet-gateway.png)
*Internet Gateway — cost-optimised alternative to NAT Gateway*

---

## Auto Scaling — Full Lifecycle Evidence

### Configuration

| | |
|---|---|
| ![AS Defined](screenshots/autoscaling-defined.png) | ![AS Config](screenshots/autoscaling-config.png) |
| *Auto Scaling policy on ECS service* | *Target tracking — CPU 50% threshold* |

### Load Test

![Load Test](screenshots/autoscaling-load-test.png)
*hey HTTP load generator — 100,000 requests from AWS CloudShell*

### Scale-Out

| | |
|---|---|
| ![CPU Peak](screenshots/cloudwatch-cpu-peak.png) | ![CW Alarm](screenshots/cloudwatch-alarm.png) |
| *CloudWatch — CPU spiked to 100%* | *CloudWatch alarm triggered* |

![Autoscaling in Action](screenshots/autoscaling-in-action.png)
*ECS service — scaling event initiated*

![4 Containers](screenshots/4-containers.png)
*4 Fargate tasks running — maximum scale-out achieved*

![ALB 4 Targets](screenshots/alb-4-targets.png)
*ALB Target Group — 4 healthy containers registered and serving traffic*

### Scale-In

| | |
|---|---|
| ![CPU Low](screenshots/cpu-low.png) | ![Scaled Down](screenshots/scaled-down-to-1.png) |
| *CPU returned to baseline* | *Containers scaled back down to 1* |

![Activity Log](screenshots/autoscaling-activity-log.png)
*Auto Scaling activity log — full scale-out and scale-in cycle*

### Auto Scaling Results

| Metric | Result |
|--------|--------|
| Peak CPU utilisation | 100% |
| Fargate tasks at peak | 4 (max scale-out) |
| Scale-out trigger | CPU > 50% sustained |
| Scale-in cooldown | 120 seconds |
| ALB health status at peak | 4 healthy / 0 unhealthy |
| Average response time | 0.58 seconds |

---

## Key Design Decisions

**No NAT Gateway** — Public subnets with Internet Gateway eliminate ~£25/month NAT costs for a development deployment.

**Fargate over EC2** — No server management or patching. Per-task billing for precise cost control.

**Dual-pipeline architecture** — Infrastructure and application deploy independently. A code push never triggers infrastructure changes.

**RDS MySQL over DynamoDB** — Finpay requires relational data with ACID transactions across users, wallets, and payments.

**Dynamic IP + ALB** — Each Fargate task gets a new private IP on launch. The ALB provides a stable DNS endpoint, automatically registering and deregistering tasks as they scale.

---

## Tech Stack

`AWS CloudFormation` · `Amazon ECS Fargate` · `Amazon ECR` · `Amazon RDS MySQL` · `Application Load Balancer` · `AWS CodePipeline` · `AWS CodeBuild` · `Amazon CloudWatch` · `Amazon VPC` · `AWS IAM` · `Docker` · `PHP 8.2` · `MySQL` · `CoinGecko API`

---

## Team

| Role | Name |
|------|------|
| DevOps Engineer & Infrastructure | Khalid Rehman |
| Application Developer | Samuel Onyekwere |

---

## Author

**Khalid Rehman** — AWS Solutions Architect Associate | MSc Cloud Computing & Network Security, University of Greater Manchester

**Samuel Onyekwere** —  MSc Cloud Computing & Network Security, University of Greater Manchester


Deployed in `eu-west-2` (London)