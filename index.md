

---

## SAP Account consolidation across all customer SAP instances

The development of a web portal to create a consolidated matrix view of user accounts across all customer SAP instances to aid in the timely removal of accounts where access is no longer required for a user to a specific SAP instance

---

### Description

This project consists of a number of AWS platforms and components as follows:
1. Single VPC
2. Multiple EC2 instances (Grafana, Django Portal, Aurora DB, Strongswan host etc. )
3. An API Gateway
4. Multiple Python based Lambda functions to perform a multitude of serverless compute functions
5. Multiple S3 buckets for data loading and updates
6. An Aurora Database

---

### Architecture

The System Architecure is depicted below:

<img src="./SAP-accounts.png">

---

The system works as follows:
1.  An 8 hourly shedule based Lambda function connects to each SAP instance and retrieves all account information which is written to an iterim storage S3 bucket
2.  A second Lambda function is triggered as soon and the new account file is written to the S3 interim storage bucket, which creates an account entry with a new time and datestamp entry in the merge table in Aurora
3.  A third lambda is triggered by any new entries into the merge table to do a lookup in the Aurora accounts table to see if the entry already exists, a comparison is created with the granted table to validate which accounts are allowed to have access to the specific SAP instance,
4.  If any anomalies are found to exist,  new Lambda is triggered via an API gatewat endpoint to oversee that an incident is logged to the ServiceNow platfom, for those accounts found to be in error and removed by an authorised person, after which the merge table is cleaned and cleared of any entries
5. This process repeats for each SAP instance which is retained as a separate list in a restricted S3 bucket

---

### System Component Diagrams

---

API Gateway to Lambda Data Flow

<img src="./API2S3.png">
   
---

S3 bucket to Aurora DB data flow

<img src="./S3toAurora.png">

---
