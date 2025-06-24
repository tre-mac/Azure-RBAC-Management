# Azure-RBAC-Management
In this lab, I explored how to manage access in Azure using **Role-Based Access Control (RBAC)** and **management groups**. I went hands-on with creating custom roles, assigning built-in roles, and using the Activity Log to monitor changes.

---

## 🎯 What I Did

### 1. Implemented Management Groups

To start, I created a **management group** called `az104-mg1` to group all my Azure subscriptions together. This helped me centralize access control across all subscriptions.

- I signed in to the Azure Portal and went to **Microsoft Entra ID > Properties** to make sure I had access management permissions.
- Then I searched for **Management Groups**, clicked **+ Create**, and used the following:
  - Management group ID: `az104-mg1`
  - Display name: `az104-mg1`
- After submitting, I refreshed the page to confirm the group was created.

I noticed the **root management group** already existed, which is the top of the hierarchy where all other groups and subscriptions roll up to.

---

### 2. Assigned a Built-In Azure Role

Next, I assigned the **Virtual Machine Contributor** role to a Help Desk group.

- From the `az104-mg1` management group, I opened the **Access Control (IAM)** blade and went to the **Roles** tab.
- I reviewed available built-in roles, then clicked **+ Add > Add role assignment**.
- I searched for **Virtual Machine Contributor** and selected it.
- On the **Members** tab, I chose a group called `New Hires`, which I had to create beforehand.
- I finished the role assignment and confirmed it under the **Role assignments** tab.

> 🔑 Pro tip I learned: Always assign roles to groups—not individuals—for better scalability.

---

### 3. Created a Custom RBAC Role

Since built-in roles don’t always match exactly what’s needed, I created a **custom RBAC role** that allows support ticket creation—but not provider registration.

Here’s what I did:

- Went to **Access Control (IAM)** on the same management group and selected **+ Add > Add custom role**.
- On the **Basics** tab, I entered:
  - Name: `Custom Support Request`
  - Description: `A custom contributor role for support requests`
  - Cloned from: `Support Request Contributor`

Then under the **Permissions** tab:
- I excluded the permission: `Microsoft.Support/register/action` so Help Desk couldn't register the support provider.

On the **Assignable scopes** tab:
- I set the scope to `az104-mg1`.

After reviewing the JSON, I created the role successfully.

---

### 4. Monitored Role Assignments

To wrap up, I checked the **Activity Log** for the management group to confirm my role changes were logged.

- I opened `az104-mg1` and selected **Activity Log**.
- I filtered the events to view recent **role assignments**.
- I was able to verify the actions I performed were recorded, which is helpful for auditing.

---

## 🧰 Tools & Services Used

- **Microsoft Azure Portal**  
- **Microsoft Entra ID**  
- **Management Groups**  
- **Role-Based Access Control (RBAC)**  
- **Activity Log**

---

## 📌 Key Takeaways

- Management groups simplify access and policy enforcement across subscriptions.
- Assigning roles to **groups** improves permission scalability.
- Creating **custom roles** ensures users only have the access they need.
- The **Activity Log** is essential for tracking access changes.

---


