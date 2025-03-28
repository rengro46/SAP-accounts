

---

## SAP Account consolidation across all customer SAP instances

The development of a web portal to create a consolidated matrix view of user accounts across all customer SAP instances to aid in the timely removal of accounts where access is no longer required for a user to a specific SAP instance

---

### Description

This project consists of a number of AWS platforms and components as follows:
1. Single VPC (VPC-A - Shared services)
3. Multiple EC2 instances (Grafana, Django Portal, Aurora DB, Strongswan host etc. )
4. An API Gateway

---

### Architecture

The System Architecure is depicted below:

<!-- ### <img src="./SAP-Accounts.png">

---

The system works as follows:
1.  

---

### System Diagrams

---

API Gatewat to Lambda Data Flow

<img src="./API2S3.png">
   
---

S3 bucket to Aurora DB data flow

<!-- ### <img src="./S3toAurora.png">

---