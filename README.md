# Infrastructure Automation Platform

## Overview
Brief explanation of the problem:
- Manual infrastructure monitoring
- Slow incident communication
- Operational overhead during outages

## Architecture

[Architecture Diagram]

Description of:
- RHEL application environment
- Amazon EKS deployment
- Jenkins CI/CD pipeline
- Terraform-managed AWS infrastructure
- PostgreSQL database
- Webex notifications

## Problem

During network outages, operations teams needed better visibility into infrastructure impact and remaining capacity.

Example:
- Multiple datacenter circuits experienced failures
- Remaining circuit utilization became critical
- Manual status updates slowed response

## Solution

Built a Python Flask automation platform that:
- Collected infrastructure information
- Automated operational workflows
- Delivered real-time notifications through Cisco Webex
- Improved visibility during incidents

## Deployment Architecture

### Application Layer
- Python Flask
- Apache/mod_wsgi
- Kubernetes/EKS

### CI/CD
- Jenkins
- Automated deployments

### Infrastructure
- AWS
- Terraform
- Infrastructure as Code

## Design Decisions

### Why Terraform?
Explain repeatable AWS infrastructure management.

### Why Kubernetes/EKS?
Explain scalability, container orchestration, and deployment standardization.

### Why Hybrid Deployment?
Explain supporting existing environments while adopting cloud-native practices.

## Results

- Reduced manual operational effort
- Improved incident communication
- Standardized deployment workflows
- Increased visibility during infrastructure events

## Technologies

Python | Flask | AWS | EKS | Kubernetes | Terraform | Jenkins | RHEL | PostgreSQL
