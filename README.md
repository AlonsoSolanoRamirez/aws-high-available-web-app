# AWS Highly Available Web Application Architecture

## Project Overview

This repository contains the architecture and deployment steps for a **Highly Available, Fault-Tolerant Web Application** built entirely within the AWS Free Tier limits. The goal of this projeect is to demonstrate baseline architectural redundancy across multiple data centers (Availability Zones) using automated infrastructure components.

## Architecture Components

-**IAM**: Utilized a dedicated principle (cloud-junior-admin) adhering to the least-privilege administrative boundary for deployment execution.
-**Application Load Balancer (ALB)**: Acts as the single public entry point, distributing incoming HTTP port 80 traffic evenly to backend instances.
-**Auto Scaling Group (ASG)**: Maintains high availability with a configured capacity matrix (min:2, desired:2, max: 4) across multiple Availability Zones to handle automated node recovery.
-**Launch Template**: Defines the baseline system blueprint using Amazon Linux 2023 (t3.micro) and includes automated Apache bootstrapping scripts (User Data).
-**Amazon CloudWatch**: Used for core resource visibility, tracking infrastructure metrics such as 'TargetResponseTime' to monitor operational health.

## Key Troubleshooting Milestones

During implementation, a routing mismatch caused a temporary node initialization failure where instances were flagged as 'Unhealthy' by the target group checks.
-**Root Cause Identified**: The initial bootstrap initialization script pointed to an incomplete target download URL string, preventing Apache from displaying the index payload.
-**Resolution Applied**: Designed a standalone robust script, modified the Launch Template version control matrix to Version 2, updated the ASG target reference, and successfully transitioned instances back into an active 'InService' healthy state.
 


