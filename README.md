# ms-p2p-ticketing-service

## Goal:

> Provide a scalable, decoupled, automation-first ticketing intake layer for P2P operations, eliminating manual email triaging and improving SLA adherence.


## **Description**

**ms-p2p-ticketing-service** is a microservice designed for the **Procure-to-Pay (P2P)** domain that automatically converts incoming emails into structured tickets and routes them to the appropriate operational teams (AP, Payments, Vendor Management, Procurement, Inventory, etc.).

The service reads emails from configured mailboxes (IMAP, Office365/Graph API, Gmail), extracts relevant details (title, body, attachments), applies routing rules or NLP classification, and creates tickets inside an internal system or exposes APIs for external ticketing tools.

This microservice follows **Hexagonal Architecture (Ports & Adapters)** to ensure high maintainability, testability, and clean separation between domain logic and infrastructure layers.

----------

# **Key Features**

### **1. Email → Ticket Automation**

-   Poll inboxes or receive push notifications (Graph API webhooks)
    
-   Parse subject, body, sender, and attachments
    
-   Convert raw messages into structured ticket DTOs
    

### **2. Smart Ticket Routing**

-   Keyword-based routing (e.g., “invoice”, “payment”, “PO”)
    
-   Team assignment rules stored in config or DB
    
-   Optional integration with NLP classifiers for advanced routing
    

### **3. REST API for Ticket Operations**

-   Create, update, and retrieve tickets via DRF endpoints
    
-   Health-check and metrics endpoints for observability
    

### **4. Background Processing via Celery**

-   Email polling worker
    
-   Attachment extraction worker
    
-   Retry and idempotency support
    

### **5. Hexagonal Architecture**

-   **Domain Layer**: entities, domain services, business rules
    
-   **Application Layer**: use cases (ticket creation, assignment)
    
-   **Ports**: repository & email client interfaces
    
-   **Adapters**: Django ORM, IMAP adapter, API controllers, Celery workers
    

### **6. Cloud-Native Ready**

-   Docker & Kubernetes compatible
    
-   Health/Liveness probes
    
-   HPA auto-scaling
    

----------

# **Technology Stack**

| Layer             | Technology                             |
| ----------------- | -------------------------------------- |
| Framework         | Django 5.2+                            |
| API               | Django REST Framework                  |
| Background Tasks  | Celery + Redis/RabbitMQ                |
| Email Integration | IMAP / Microsoft Graph API / Gmail API |
| Database          | PostgreSQL                             |
| Architecture      | Hexagonal / Ports & Adapters           |
| Deployment        | Docker, Kubernetes                     |
| Monitoring        | Prometheus, Grafana, ELK, Sentry       |


## **Typical Use Cases**

-   Vendor emails “invoice missing”, “payment not processed”
    
-   Procurement approval escalations
    
-   AP exception handling
    
-   Supplier onboarding issues
    
-   GRN/Inventory mismatch alerts
    
-   Automated inbox workflow replacement

------

## 1. Run these commands in Git Bash / Linux / Mac

```bash
mkdir -p ms-p2p-ticketing-service
cd ms-p2p-ticketing-service

# Django project folder (already created by startproject)
mkdir -p config

# Django apps folder
mkdir -p apps

# Hexagonal Architecture folders
mkdir -p domain/entities
mkdir -p domain/services

mkdir -p application/use_cases

mkdir -p ports

mkdir -p infrastructure/api
mkdir -p infrastructure/email
mkdir -p infrastructure/persistence
mkdir -p infrastructure/tasks

# Required __init__.py files so Python can import these modules
touch apps/__init__.py

touch domain/__init__.py
touch domain/entities/__init__.py
touch domain/services/__init__.py

touch application/__init__.py
touch application/use_cases/__init__.py

touch ports/__init__.py

touch infrastructure/__init__.py
touch infrastructure/api/__init__.py
touch infrastructure/email/__init__.py
touch infrastructure/persistence/__init__.py
touch infrastructure/tasks/__init__.py

```

