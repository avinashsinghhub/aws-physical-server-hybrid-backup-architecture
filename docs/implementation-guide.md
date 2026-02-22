# Implementation Guide  
Hybrid Physical Server Backup Architecture (AWS + VPN Offsite Copy)

---

## 1. Environment Overview

Primary Location: Office A  
Secondary Location: Office B  
Cloud Region: ap-south-1  

Source System:
- Physical Windows Server (Production Workload)

Backup Targets:
- AWS Backup Vault (Cloud)
- External Hard Disk (Offsite – Office B)

---

## 2. AWS Configuration

### 2.1 AWS Backup Setup

1. Created Backup Vault
   - Encryption: AWS Managed KMS
   - Public access: Not applicable
   - Region: ap-south-1

2. Created Backup Plan
   - Schedule: Daily
   - Retention: As per business requirement
   - Assigned resource via AWS Backup Agent

---

### 2.2 IAM Role Configuration

Created IAM execution role with:

- Least privilege permissions
- AWSBackupServiceRolePolicyForBackup
- No administrative permissions

Purpose:
Allows AWS Backup Service to perform backup operations securely.

---

### 2.3 SNS Notification Setup

1. Created SNS Topic
2. Subscribed email endpoint
3. Configured AWS Backup to send job status events
4. Verified email confirmation

Purpose:
Receive alerts for failed backup jobs.

---

## 3. AWS Backup Agent Installation (Office A)

1. Installed AWS Backup Agent on Windows Server
2. Registered server with AWS Backup
3. Assigned server to backup plan
4. Tested manual backup execution

Verified:
- Successful job completion
- Data visible in Backup Vault

---

## 4. VPN Configuration (Office A → Office B)

Network Type:
Site-to-Site VPN (IPSec Encrypted Tunnel)

Components:
- Cisco VPN Gateway (Office A)
- VPN Endpoint (Office B)

Purpose:
Secure encrypted data transfer between offices.

---

## 5. Offsite Incremental Backup Configuration

On Windows Server (Office A):

1. Created Scheduled Incremental Backup Job
2. Backup Target:
   Network path mapped via VPN
3. Destination:
   Windows Machine (Office B)
4. Final storage:
   External Hard Disk

Schedule:
- Daily
- Off-business hours

Purpose:
Maintain independent physical backup copy.

---

## 6. Backup Flow Summary

Cloud Path:
Windows Server → AWS Backup Agent → AWS Backup Service → Encrypted Backup Vault

Offsite Path:
Windows Server → Scheduled Incremental Job → VPN Tunnel → Office B Windows Machine → External HDD

Both paths operate independently.

---

## 7. Security Controls Implemented

- HTTPS encrypted cloud transmission
- IPSec encrypted VPN tunnel
- Encrypted Backup Vault (AWS Managed KMS)
- Least privilege IAM role
- No production workload at Office B
- Email alerting for job failures

---

## 8. Operational Monitoring

- AWS Backup job status monitored via SNS
- Email notifications for failed jobs
- Manual periodic validation of incremental copy integrity

---

## 9. Validation Performed

- Successful cloud restore test
- Successful external HDD restore test
- VPN connectivity validation
- Encryption verification

---

## 10. Final Outcome

The implemented architecture provides:

- Dual independent backup paths
- Cloud-based disaster recovery
- Offsite physical redundancy
- Secure encrypted transfer
- Minimal operational overhead
