# Infrastructure Operations Automation Platform

> A Python Flask-based infrastructure operations platform that automated incident communication, standardized operational workflows, and streamlined infrastructure management across a hybrid on-premises and AWS production environment.

---

# Key Highlights

* Python Flask internal operations automation platform
* Hybrid active-active deployment across Red Hat Enterprise Linux and Amazon EKS
* Corporate F5 BIG-IP load balancing between on-premises and AWS environments
* Jenkins CI/CD with integrated Snyk vulnerability scanning
* Terraform-managed AWS infrastructure
* PostgreSQL-backed metadata management and operational reporting
* Cisco Webex API integration for standardized incident communication
* Automated form auto-population using infrastructure metadata
* Historical notification reporting and auditing
* Reduced manual operational effort through workflow automation

---

# Overview

Modern network operations require rapid communication and consistent processes during infrastructure incidents. Manual notification workflows often lead to inconsistent messaging, repetitive data entry, and delayed communication during critical outages.

To address these challenges, I developed an internal Infrastructure Operations Automation Platform using Python Flask. The platform centralized operational workflows by combining automated notification generation, infrastructure metadata management, historical reporting, and Cisco Webex integration into a single web application.

The application was deployed using a hybrid architecture spanning traditional Red Hat Enterprise Linux servers and Amazon Elastic Kubernetes Service (EKS), allowing the organization to modernize its infrastructure while continuing to support existing production environments.

---

# Problem

During production network outages, operations engineers needed a faster and more standardized way to communicate infrastructure events.

Challenges included:

* Manual notification creation
* Repetitive entry of static circuit information
* Slow communication during outages
* Inconsistent notification formatting
* Limited historical reporting
* Operational overhead during high-impact incidents

One example involved multiple datacenter circuit failures where engineers needed continuous visibility into remaining circuit utilization while coordinating incident response across multiple teams.

---

# Solution

The platform automated multiple operational workflows through a centralized web application.

Core capabilities included:

* Automated incident notification generation
* Circuit metadata management
* Database-driven form auto-population
* Cisco Webex notification integration
* Historical notification reporting
* Standardized operational communication
* Hybrid production deployment
* CI/CD automation with integrated security validation

---

# User Workflows

The platform supported multiple workflows depending on the engineer's operational task.

---

## Create Notification Workflow

![Create Notification Workflow](images/create-notification-workflow.png)

### Workflow

1. Engineer accesses the internal Operations Portal.
2. Engineer selects **Create Notification**.
3. Circuit ID is entered.
4. Flask queries PostgreSQL for circuit metadata.
5. Static fields are automatically populated.
6. Engineer enters incident-specific information.
7. Flask validates the request.
8. Notification is stored in PostgreSQL.
9. Cisco Webex API sends a standardized notification.

---

## Edit / Reply Notification Workflow

![Edit Reply Workflow](images/edit-reply-workflow.png)

### Workflow

The platform also supported ongoing incident communication.

Engineers could:

* Retrieve existing notifications
* Edit notification details
* Reply with operational updates
* Maintain communication throughout an incident

Updated notification history was stored in PostgreSQL while Webex messages were updated through the Cisco Webex API.

---

## Circuit Metadata Management Workflow

![Circuit Metadata Workflow](images/circuit-metadata-workflow.png)

### Workflow

To reduce repetitive manual data entry, the application included a dedicated metadata management interface implemented as a separate administrative section of the web application.

Authorized users could perform full CRUD operations on circuit metadata including:

* Create circuit records
* View existing metadata
* Update inaccurate information
* Remove obsolete records

Maintaining accurate metadata ensured notification forms remained automatically populated with reliable infrastructure information.

---

# Runtime Architecture

![Runtime Architecture](images/runtime-architecture.png)

The production environment utilized a hybrid active-active deployment architecture.

## User Access Layer

* Network / Operations Engineers
* Internal corporate URL
* Corporate F5 BIG-IP Load Balancer

The F5 load balancer distributed production traffic across both on-premises and AWS-hosted application environments.

---

## Application Hosting Layer

### On-Premises Environment

* Red Hat Enterprise Linux
* Apache Web Server
* mod_wsgi
* Python Flask Application

### AWS Environment

* Amazon Elastic Kubernetes Service (EKS)
* Kubernetes
* Flask Application Pods
* Kubernetes Services

Both environments actively served production traffic.

---

## Application Layer

Python Flask provided:

* Notification automation
* Business logic
* Input validation
* Database interactions
* Cisco Webex integration
* Metadata management

---

## Data Layer

Shared PostgreSQL Database

Logical tables:

### Circuit Metadata

Reference data used for form auto-population.

Stored:

* Circuit ID
* Circuit Bandwidth
* Device Name
* ISP Port
* Circuit Provider

---

### Notification History

Operational transaction records including:

* Timestamp
* Circuit ID
* Incident Details
* Notification Status

Used for:

* Reporting
* Auditing
* Historical analysis

---

## External Integrations

Cisco Webex API

Used for:

* Create notifications
* Update notifications
* Reply to existing communication threads

---

# Delivery Architecture

![Delivery Architecture](images/delivery-architecture.png)

Application delivery followed a controlled DevSecOps workflow.

## Development Deployments

Development (CDL) deployments were manually initiated through Jenkins, allowing engineers to validate functionality before production promotion.

---

## Production Deployments

Production deployments were automatically triggered through Git webhooks following approved code changes.

---

## Jenkins Pipeline

Pipeline stages included:

1. Source Checkout
2. Build
3. Validation
4. Security Scanning
5. Manual Approval
6. Production Deployment

---

## Security Validation

The pipeline integrated Snyk to perform dependency vulnerability scanning and enforce security policies before production releases.

---

## Deployment Targets

Following approval, Jenkins deployed application updates to:

* Red Hat Enterprise Linux production servers
* Amazon EKS production cluster

---

## Infrastructure Management

Terraform was used independently of the application deployment pipeline to manage AWS infrastructure through Infrastructure as Code.

Terraform responsibilities included:

* Infrastructure provisioning
* AWS configuration management
* Infrastructure consistency
* Version-controlled infrastructure changes

---

# Engineering Challenges

## Supporting Hybrid Infrastructure

The application operated across both traditional RHEL servers and Amazon EKS while maintaining a consistent user experience. A corporate F5 BIG-IP load balancer distributed production traffic between both environments, enabling gradual cloud adoption without disrupting existing operational workflows.

---

## Reducing Manual Data Entry

Instead of repeatedly entering static infrastructure information, engineers entered a Circuit ID and the application automatically retrieved circuit metadata from PostgreSQL. This reduced manual effort, improved consistency, and minimized human error during incident response.

---

## Standardizing Operational Communication

The platform generated consistent notification formats and integrated with the Cisco Webex API to improve communication during infrastructure incidents while supporting updates throughout the incident lifecycle.

---

# Design Decisions

## Why Terraform?

Terraform managed AWS infrastructure using Infrastructure as Code, reducing manual configuration, minimizing configuration drift, and providing repeatable infrastructure management through version-controlled configuration.

---

## Why Kubernetes / Amazon EKS?

Amazon EKS standardized deployment of containerized application workloads while providing orchestration, scalability, health management, and deployment consistency.

---

## Why Hybrid Deployment?

The hybrid architecture enabled continued support for existing production workloads while incrementally adopting cloud-native technologies. Running both on-premises and AWS environments behind a corporate F5 load balancer reduced migration risk and increased operational flexibility.

---

## Why PostgreSQL?

Separating reference data from transactional records simplified application logic and improved maintainability.

Benefits included:

* Automatic form population
* Reduced manual entry
* Consistent infrastructure metadata
* Historical reporting
* Operational auditing

---

# Technology Stack

| Category           | Technologies             |
| ------------------ | ------------------------ |
| Backend            | Python, Flask            |
| Web Server         | Apache, mod_wsgi         |
| Container Platform | Kubernetes, Amazon EKS   |
| Operating System   | Red Hat Enterprise Linux |
| Database           | PostgreSQL               |
| Infrastructure     | AWS, Terraform           |
| CI/CD              | Jenkins                  |
| DevSecOps          | Snyk                     |
| Messaging          | Cisco Webex API          |
| Networking         | F5 BIG-IP Load Balancer  |

---

# Results

The platform significantly improved operational efficiency by automating manual infrastructure workflows.

Key outcomes included:

* Reduced manual data entry through metadata auto-population
* Standardized incident communication
* Faster notification delivery during outages
* Improved operational visibility
* Historical reporting and auditing
* Hybrid production deployment across on-premises and AWS
* Automated CI/CD with integrated security validation
* Improved consistency across operational workflows

---

# Future Enhancements

Potential future improvements include:

* Role-based access control (RBAC)
* Automated notification templates
* Additional reporting dashboards
* Expanded infrastructure integrations
* Kubernetes-native deployment strategies
* Enhanced operational analytics
