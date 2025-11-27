# Topic 5 — Hands-On: Assign Role Access (Portal Only)

## 🎯 Objective
Combine Key Vault + RBAC + Managed Identity into one real workflow.

---

# 🧪 A — Create/Verify Secret in Key Vault
Key Vault → Secrets → `DbPassword`

---

# 🧪 B — Enable VM Managed Identity
VM → Identity → System-assigned → On → Save

---

# 🧪 C — Assign Key Vault Secrets User to VM

Key Vault → IAM → Add Role
- Role: **Key Vault Secrets User**
- Member: `lab-vm`

---

# 🧪 D — Validate Access (Portal)

Key Vault → Access Control (IAM) → **Check Access**
- Identity: `lab-vm`
- Permission: Secret Get = Allowed

---

# 🧪 E — (Optional) Validate from VM (Run Command)

VM → Run Command
- RunShellScript / PowerShell
- Request MSI token via IMDS endpoint

✔ Successfully authenticates → proves access.

---

# 🏁 Completion
You completed the full identity-based secure access workflow.

