# 🚀 Module 1: Build Your Server - Setting up GCP VM with External & Internal IP
by: Mohd Hisyamudin

This guide provides **step-by-step instructions** to set up a **Google Cloud Platform (GCP) VM**, configure **external and internal IP addresses**, and prepare it for your projects.

---

## ✅ **Step 0. Prerequisites**

* Google account
* Credit card for account verification (no charges if within free tier)
* Decide your project name (e.g. my-first-server)

---

## ✅ **Step 1. Sign up for GCP Free Tier**

1. Go to **Google Cloud Free Tier**.
2. Click “Get started for free.”
3. Sign in with your Google account.
4. Follow setup:

   * Fill in personal details.
   * Verify identity using credit card.

✔️ You will receive **\$300 free credit (valid 90 days)** plus **Always Free usage resources**.

---

## ✅ **Step 2. Create a New Project**

1. Go to **Google Cloud Console**.
2. At top navbar, click project dropdown.
3. Click **“NEW PROJECT.”**
4. Name your project (e.g. my-free-tier-vm).
5. Click **Create**.

---

## ✅ **Step 3. Enable Compute Engine API**

1. In left sidebar, go to **Compute Engine > VM instances**.
2. Click **“Enable”** to activate API for your project.

✔️ Wait a few seconds for initialization.

---

## ✅ **Step 4. Create a Free Tier VM Instance**

1. Click **“Create Instance.”**

**Key configurations to stay within free tier:**

* **Name:** e.g. my-free-vm
* **Region:** us-west1 (Oregon) or us-central1 (Iowa)
* **Machine Configuration:**

  * Series: E2
  * Machine type: e2-micro (free tier eligible)
* **Boot Disk:**

  * Click “Change.”
  * OS: Ubuntu LTS (e.g. Ubuntu 22.04 LTS)
  * Disk type: Standard Persistent Disk (HDD)
  * Size: Default 10GB (free tier allows up to 30GB)
* **Firewall:**

  * ✅ Allow HTTP traffic
  * ✅ Allow HTTPS traffic

---

## ✅ **Step 5. Networking (Optional – Static External IP)**

To reserve a **static external IP**:

1. Under **Networking > Network interfaces**.
2. Under External IP, select **“Create IP address.”**

Otherwise, leave as **Ephemeral IP** (changes on VM restart).

---

## ✅ **Step 6. Create the Instance**

1. Review configuration.
2. Click **“Create.”**
3. Wait for VM to initialize (green checkmark when ready).

---

## ✅ **Step 7. Connect to Your Server**

### **Option A: Browser SSH**

* In Compute Engine VM list, click **“SSH.”**

### **Option B: Local Terminal**

Using your SSH key:

```bash
ssh -i ~/.ssh/your_key username@external_ip
```

---

## ✅ **Step 8. First-time Setup Commands**

Update server:

```bash
sudo apt update
```

Install common packages (example nginx):

```bash
sudo apt install nginx
```

---

## ✅ **Step 9. Monitor Free Tier Usage**

* Go to **Billing > Reports** to monitor usage.
* Free tier includes:

  * 1 e2-micro VM (750 hours/month)
  * 30 GB HDD storage
  * 1 GB snapshot storage

❌ **Charges apply if exceeded.**

---

## ✅ **Step 10. Fix (Reserve) External IP Address**

By default, external IP is **ephemeral** (changes on stop/start). To fix:

1. Go to **VPC Network > External IP addresses**.
2. Find your VM with ephemeral IP.
3. Click **“RESERVE.”**
4. Fill in:

   * Name: e.g. my-static-external-ip
   * Type: Static
   * Region: same as your VM
5. Click **“Reserve.”**

✔️ Your VM now has a **fixed static external IP**.

### ⚠️ **Billing Note**

* Static external IP is free **when attached to a running VM**.
* ❌ If reserved but **not attached**, incurs small monthly charge.

---

## ✅ **Step 11. Fix (Reserve) Internal IP Address**

### **Option A: During VM Creation**

1. Under **Networking > Network interfaces**, click **“Default.”**
2. Under Internal IP, click **“Reserve static internal IP address.”**
3. Fill in:

   * Name: e.g. my-static-internal-ip
   * Subnet: default subnet in your selected region
4. Click **Reserve.**

### **Option B: For Existing VM**

1. Stop the VM.
2. Go to **VPC Network > Internal IP addresses**.
3. Click **“Reserve static address.”**
4. Choose:

   * Region and Subnet matching your VM
   * IP address (optional, auto-assigned if left blank)
   * Name: e.g. my-static-internal-ip
5. Detach current ephemeral IP and attach reserved static IP via **Network interfaces**.
6. Restart the VM.

✔️ Your VM now has a **fixed internal IP**.

---

## ✅ **Why Fix Both IPs?**

* **Static External IP:** Consistent public address for DNS, APIs, production apps.
* **Static Internal IP:** Useful when multiple servers communicate internally, or you have firewall rules based on fixed internal IP.

---

## ✅ **Final Reminder**

* **Static external IP incurs cost if unused (not attached).**
* **Internal static IP is free** under current usage limits.

---

## 🎯 **Outcome**

✅ Fully working GCP VM with:

* Static external IP (for public access)
* Static internal IP (for internal networking)

Ideal for:

* Learning & development
* Hosting small websites
* Running automation tools like n8n

---

* Author: Mohd Hisyamudin
* Mini Course: BUILDS – Panduan Zero to Hero AI WhatsApp Automation

