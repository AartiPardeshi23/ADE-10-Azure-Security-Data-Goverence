# Topic 2 — Access Control / RBAC (Azure Portal Only)

## 🎯 Objective
Understand and implement:
- Role assignment
- Scope-based access
- Custom roles
- Least privilege model

---

## 🛠 Prerequisites
- Resource group: `rg-stream-lab`
- Test user/service principal

---

# 🧪 A — Assign Built-In Role (Reader)

1. Portal → Resource Groups → `rg-stream-lab`
2. Left menu → **Access control (IAM)**
3. + Add → **Add role assignment**
4. Role → **Reader**
5. Members → Select user → Assign

✔ User can view but cannot modify resources.

---

# 🧪 B — Assign Resource-Level Role

Example: Storage Blob Data Contributor

1. Storage Account → IAM
2. + Add role assignment
3. Role → **Storage Blob Data Contributor**
4. Select user → Assign

✔ User can only manage blobs, not the whole RG.

---

# 🧪 C — Create a Custom Role (Portal)

1. Subscription → IAM → + Add **Custom role**
2. **Start from scratch**
3. Name: `VM Read-Only Custom`
4. Permissions → Add:
   - `Microsoft.Compute/virtualMachines/read`
5. Scopes → Assignable Scope → RG: `rg-stream-lab`
6. Create

Assign to a user:
- Resource Group → IAM → Add role assignment

✔ Custom role works with limited permissions.

---

# 🧪 D — Remove Access
RG → IAM → Role Assignments → Remove selected user.

