# Topic 3 — Encryption (Azure Portal Only)

## 🎯 Objective
Implement:
- Storage Encryption (PMK & CMK)
- SQL TDE verification
- VM Disk encryption verification
- HTTPS / TLS enforcement
- Key Vault CMK integration

---

# 🧪 A — Storage Account Encryption

## 1. Check Default Encryption
Storage Account → **Encryption**
- Type: Microsoft-managed keys (default)

---

## 2. Switch to Customer-Managed Keys
### Create Key Vault
Key Vaults → + Create
- RG: `rg-stream-lab`
- Name: `labkv123`

### Create Key
Key Vault → Keys → Generate
- Name: `storage-key1`

### Assign RBAC to Storage Account
Key Vault → IAM
- Add role → **Key Vault Crypto Service Encryption User**
- Member: Storage Account

### Apply CMK
Storage Account → Encryption
- Choose **Customer-managed key**
- Select Key Vault & key → Save

---

# 🧪 B — SQL Encryption (TDE)

SQL Database → **Transparent Data Encryption**
- Status: **On** (default)

(Optional) Use CMK:
- Choose Key Vault → Select key → Save

---

# 🧪 C — VM Disk Encryption

VM → Disks → OS Disk
- Encryption: Platform-managed keys (default)

---

# 🧪 D — Data in Transit (TLS)

### Storage HTTPS
Storage → Configuration
- Secure transfer required = **Enabled**

### App Service HTTPS
App Service → TLS/SSL
- HTTPS only = **On**

### SQL
SQL Server → Networking
- Enforce encrypted connections = **On**

