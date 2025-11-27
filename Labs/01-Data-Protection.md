# Topic 1 — Data Protection (Azure Portal Only)

## 🎯 Objective
Protect data stored in Azure Storage and Azure SQL using built-in security features:
- Soft delete
- Versioning
- Immutable storage
- Defender for Storage
- SQL backups, LTR, PITR

---

## 🛠 Prerequisites
- Resource group: `rg-stream-lab`
- Azure subscription with contributor rights

---

# 🧪 A — Protect an Azure Storage Account

## 1. Create Storage Account
Azure Portal → Storage Accounts → **+ Create**
- RG: `rg-stream-lab`
- Name: `labstorage123`
- Default settings → Create

---

## 2. Enable Soft Delete
Storage Account → **Data protection**
- Soft delete for blobs → **Enable**
- Retention: `7` days → Save

---

## 3. Enable Blob Versioning
Storage Account → Data protection
- Blob versioning → **Enable** → Save

---

## 4. Create Immutable Container
Storage Account → **Containers**
- Add → Name: `immutable-container`
- Access: Private → Create

Container → **Access policy**
- Add immutability policy
- Mode: **Time-based retention**
- Days: `30` → Save

---

## 5. Test Soft Delete + Versioning
1. Upload a blob
2. Delete it
3. Storage account → Soft deleted blobs → Restore
4. Upload again with the same name → View **Version History**

---

# 🧪 B — Azure SQL Data Protection

## 1. Create SQL Server & DB
Portal → SQL Databases → **+ Create**
- DB name: `labdb`
- Server: `labsqlserver123`
- Create

---

## 2. Verify Automatic Backups / PITR
SQL DB → **Restore**
- Choose any restore point
- Create restored DB (example: `labdb-restore`)

---

## 3. Configure Long-Term Retention (LTR)
SQL Server → **Backups**
- Select DB → Long-term retention
- Weekly retention: `12 weeks` → Save

---

# ✔ Verification
- Soft delete enabled
- Versioning enabled
- Immutable container active
- PITR restore available
- LTR configured

