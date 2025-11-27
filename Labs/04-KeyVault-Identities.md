# Topic 4 — Key Vault & Identities (Azure Portal Only)

## 🎯 Objective
Implement secure identity-based secret access using:
- Key Vault
- Managed Identity
- RBAC
- Secret retrieval testing (Portal only)

---

# 🧪 A — Create Key Vault

Portal → Key Vaults → + Create
- RG: `rg-stream-lab`
- Name: `labkv123`
- Access config: **Azure RBAC**

---

# 🧪 B — Add Secret

Key Vault → Secrets → + Generate
- Name: `DbPassword`
- Value: `P@ssw0rd123!`

---

# 🧪 C — Enable VM Managed Identity

VM → Identity → System-assigned → **On** → Save

---

# 🧪 D — Grant VM Access to Secrets

Key Vault → IAM → Add role assignment
- Role: **Key Vault Secrets User**
- Member: `lab-vm` (managed identity)

---

# 🧪 E — Verify Access

Key Vault → IAM → **Check Access**
- Search identity: `lab-vm`
- Permission: Secret Get → **Allowed**

---

# 🧪 F — (Optional) Test Identity via VM Run Command
VM → Run Command → RunShellScript / PowerShell  
Use IMDS endpoint to retrieve token.

✔ Confirms VM identity works.

