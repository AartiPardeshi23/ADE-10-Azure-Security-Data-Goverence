# 📘 **Azure Security, Compliance, and Data Governance — Hands-On Practical Lab**

**Mode:** Azure Portal Only — No CLI Required
**Topics Covered:**

1. Data Protection
2. Access Control / RBAC
3. Encryption (At Rest & In Transit)
4. Key Vault & Identities
5. Assign Role Access (Integrated Lab)

---

# 🚀 **Prerequisites**

* Azure Subscription
* Resource Group: **rg-stream-lab**
* At least one VM (optional but recommended)
* Permission: **Contributor** + **User Access Administrator**

---

# ------------------------------------------------------------

# **1. Data Protection (Portal Only)**

# ------------------------------------------------------------

## **1.1 Create a Storage Account**

1. Portal → Storage accounts → **+ Create**
2. Resource group → `rg-stream-lab`
3. Name → `labsecurity123`
4. Review + Create → Create

---

## **1.2 Enable Soft Delete for Blobs**

1. Storage account → **Data protection**
2. Soft delete for blobs → **Enable**
3. Retention: **7 days** → Save

---

## **1.3 Enable Blob Versioning**

1. Storage account → Data protection
2. Blob versioning → **Enable** → Save

---

## **1.4 Create an Immutable Container (Optional)**

1. Storage → Containers → + Container
2. Name: `immutable`
3. Access → Private → Create
4. Open container → **Access policy**
5. Select **Time-based retention** → 30 days → Save

---

## **1.5 Test Data Protection**

1. Upload a file into any container
2. Delete the file
3. Restore using:
   Storage → Data protection → **Recover deleted blobs**

✔ Verifies soft delete + versioning.

---

## **1.6 Enable Microsoft Defender for Storage**

Portal → Defender for Cloud → Environment settings → Your subscription
→ Enable **Microsoft Defender for Storage**

---

# ------------------------------------------------------------

# **2. Access Control / RBAC (Portal Only)**

# ------------------------------------------------------------

## **2.1 Assign Reader Role at Resource Group Level**

1. RG → `rg-stream-lab` → **Access control (IAM)**
2. Add → **Add role assignment**
3. Choose **Reader**
4. Select user/service principal → Assign

---

## **2.2 Assign Resource-Level Role**

Example: Storage Blob Data Contributor

1. Storage account → Access control (IAM)
2. Add role assignment → **Storage Blob Data Contributor**
3. Select user → Assign

✔ User can manage blobs but not the whole RG.

---

## **2.3 Create a Custom Role (Portal Only)**

1. Subscription → Access control (IAM)
2. Add → **Add custom role**
3. Start from scratch
4. Name → *VM Read-Only Custom Role*
5. Permissions → Add:

   * `Microsoft.Compute/virtualMachines/read`
6. Scope → Assignable to `rg-stream-lab`
7. Create

---

## **2.4 Assign Custom Role**

1. RG → IAM
2. Add role assignment
3. Choose your custom role → Assign

✔ User can view VMs but cannot modify them.

---

# ------------------------------------------------------------

# **3. Encryption (At Rest & In Transit)**

# ------------------------------------------------------------

# **3.1 Storage Account Encryption (Default)**

Storage → Encryption → Shows:

* Encryption type: **Microsoft-managed keys**

✔ Enabled by default.

---

# **3.2 Customer-Managed Keys (CMK) for Storage**

### **Step A — Create Key Vault**

Portal → Key vaults → + Create

* Name: `labkv123`
* Access: RBAC
* Create

### **Step B — Create Key**

Key vault → Keys → + Generate → RSA 2048 → Create

### **Step C — Grant Storage Account Access to Key**

Key vault → IAM → Add role assignment →

* **Key Vault Crypto Service Encryption User**
* Assign to *storage account managed identity*

### **Step D — Enable CMK**

Storage → Encryption →

* Switch to **Customer-managed key**
* Select Key Vault + key
* Save

✔ Storage now uses your own key.

---

# **3.3 SQL Encryption (TDE)**

SQL DB → Transparent Data Encryption →

* Status: **On** (default)

Optional: Choose Customer-Managed Key using your Key Vault.

---

# **3.4 Azure VM Disk Encryption**

VM → Disks → OS Disk → Encryption
✔ Shows encrypted with **platform-managed keys** (default).

---

# **3.5 Encryption In Transit (HTTPS / TLS)**

### **Enforce HTTPS for Storage**

Storage → Configuration →

* **Secure transfer required = Enabled**

### **Enforce HTTPS for App Service**

App Service → TLS/SSL settings →

* **HTTPS Only = On**

### **Verify SQL TLS**

SQL Server → Networking →
✔ Encrypt connections = Enabled

---

# ------------------------------------------------------------

# **4. Key Vault & Identities**

# ------------------------------------------------------------

## **4.1 Create Key Vault**

Portal → Key vaults → + Create

* Name: `labkv123`
* RG: `rg-stream-lab`
* Access model: RBAC

---

## **4.2 Add a Secret**

Key vault → Secrets → + Generate/Import

* Name: `DbPassword`
* Value: `P@ssw0rd123!`
  → Create

---

## **4.3 Enable System-Assigned Managed Identity on VM**

VM → Identity → System-assigned → **On** → Save

---

## **4.4 Give VM Access to Key Vault**

Key vault → IAM → Add role assignment

* Role: **Key Vault Secrets User**
* Member: `lab-vm` (VM identity)

✔ VM can now read secrets securely.

---

## **4.5 Validate Access**

Key vault → IAM → **Check access**

* Search for VM
* Should show: **Secret Get: Allowed**

---

# ------------------------------------------------------------

# **5. Assign Role Access (Integrated Lab)**

# ------------------------------------------------------------

### 🔹 **Goal:**

Let a VM use Managed Identity to read a Key Vault secret.

---

# **5.1 Assign RBAC Role**

Key vault → Access control → + Add role assignment

* Role: **Key Vault Secrets User**
* Member: VM identity

---

# **5.2 Verify Using Portal Test**

Key vault → Access control → **Check access**
Search VM → See **Allowed** permissions.

---

# **5.3 Test Token Retrieval (Portal Only)**

VM → Operations → **Run Command** → RunShellScript

Linux VM:

```
curl -H "Metadata:true" \
"http://169.254.169.254/metadata/identity/oauth2/token?resource=https://vault.azure.net&api-version=2018-02-01"
```

Windows VM:

```
Invoke-RestMethod -Method GET -Uri "http://169.254.169.254/metadata/identity/oauth2/token?resource=https://vault.azure.net&api-version=2018-02-01" -Headers @{Metadata="true"}
```

✔ Token returned = VM identity working.

---

# ------------------------------------------------------------

# 🎯 **Final Verification Checklist**

| Topic                               | Verified |
| ----------------------------------- | -------- |
| Data protection features enabled    | ✔        |
| RBAC roles assigned                 | ✔        |
| Custom role created                 | ✔        |
| Storage/SQL/VM encryption validated | ✔        |
| Key Vault + Managed Identity setup  | ✔        |
| Integrated RBAC lab completed       | ✔        |

---

# 🏁 **Lab Completed**

You have successfully completed:

* Data Protection
* RBAC
* Encryption
* Key Vault & Identities
* Full integrated Role Assignment lab

---
