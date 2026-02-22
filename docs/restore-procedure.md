# Restore Procedure  
Hybrid Physical Server Backup Architecture

---

## Overview

This document describes restoration procedures for:

1. Cloud Restore (AWS Backup Vault)
2. Offsite Restore (External HDD – Office B)

---

# 1. Restore from AWS Backup Vault

## Use Case

- Hardware failure at Office A
- Ransomware infection
- Complete system corruption

---

## Steps

1. Log in to AWS Console
2. Navigate to AWS Backup → Backup Vault
3. Select recovery point
4. Choose "Restore"
5. Select target server
6. Initiate restore job

Monitor job status via:
AWS Backup Console

---

## Post-Restore Validation

- Verify restored files
- Confirm data integrity
- Validate application functionality

---

# 2. Restore from Office B External HDD

## Use Case

- Internet outage preventing AWS restore
- Partial file-level recovery
- Fast local recovery scenario

---

## Steps

1. Access Office B Windows Machine
2. Connect external hard disk
3. Identify latest incremental backup
4. Copy required data
5. Transfer via VPN back to Office A
   OR physically transport drive if needed

---

## Post-Restore Validation

- Confirm restored files match expected versions
- Validate checksum if required
- Verify application startup

---

# 3. Disaster Recovery Scenario Matrix

| Scenario | Recommended Restore Path |
|----------|--------------------------|
| Single file recovery | External HDD |
| Complete server failure | AWS Backup Vault |
| Ransomware | AWS Backup Vault |
| Internet outage | External HDD |
| Office A outage | AWS Backup Vault |

---

# 4. Restore Best Practices

- Perform quarterly restore drills
- Validate backup retention policy
- Monitor SNS alerts
- Periodically test VPN connectivity

---

# 5. Important Notes

- Cloud restore time depends on dataset size
- VPN restore speed depends on bandwidth
- Ensure encryption keys remain accessible
