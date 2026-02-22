# Hybrid Physical Server Backup Architecture (AWS + VPN Offsite Copy)

Client: Confidential Multinational Publishing Company 
Industry: Book & Publishing  Size: 3000-4000 endpoints
Solution: Automated Physical Server Backup and Offsite Copy
Tool: AWS Backup
Cloud Platform: Amazon Web Services (AWS)

## Overview

This repository documents the implementation of a hybrid backup solution for a physical Windows Server environment.

The architecture combines:

- AWS Backup for cloud-based disaster recovery
- Encrypted backup vault storage (AWS Managed KMS)
- IAM least-privilege execution role
- SNS-based email failure notifications
- Site-to-Site VPN tunnel to secondary office
- Daily incremental offsite copy to external hard disk

This design provides dual independent backup paths for business continuity and disaster recovery.

---

## Architecture Diagram

![Hybrid Backup Architecture](https://github.com/avinashsinghhub/aws-physical-server-hybrid-backup-architecture/blob/08e9de12e1b33f2a533f6b6d5bc6c1c488d6dd29/architecture/aws-physical-server-hybrid-backup-architecture.png)

---

## Backup Flow Summary

### Cloud Backup Path
Windows Server → AWS Backup Agent → AWS Backup Service → Encrypted Backup Vault  
Failure notifications via SNS → Email Alert

### Offsite Backup Path
Windows Server → Scheduled Incremental Job → Site-to-Site VPN → Office B Windows Machine → External HDD

---

## Key Design Principles

- Encrypted transmission (HTTPS + IPSec VPN)
- Encrypted backup storage (AWS Managed KMS)
- Least-privilege IAM execution role
- Independent backup paths
- Offsite secondary storage
- Operational alerting

---

## Disaster Recovery Strategy

- Primary Recovery: Restore from AWS Backup Vault
- Secondary Recovery: Restore from Office B external HDD
- Backup jobs monitored via SNS email alerts

---
Author: Avinash Singh  
Hybrid Infrastructure | AWS Backup Strategy | DR Architecture
