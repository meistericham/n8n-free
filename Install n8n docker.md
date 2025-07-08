# 🚀 BUILDS Module 2: Install & Deploy n8n using Docker

This guide helps you **install and deploy n8n** on your GCP VM quickly and avoid common installation errors.

---

## 📾 **📌 Prerequisites**

* Google Cloud Platform (GCP) VM instance (e2-micro, Ubuntu 22.04 LTS recommended)
* Firewall rules open for **TCP port 5678**
* Swap file configured (optional but recommended for micro VM stability)

---

## ✅ **Step 1: Update system & install Docker**

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

---

## ✅ **Step 2: Prepare n8n data directory with correct permissions**

```bash
mkdir ~/.n8n
sudo chown -R 1000:1000 ~/.n8n
```

**Explanation:**
`.n8n` is used to store configuration and database. Changing ownership ensures Docker container can read/write without permission errors.

---

## ✅ **Step 3: Pull n8n stable Docker image**

```bash
sudo docker pull n8nio/n8n:1.45.1
```

> ℹ️ **Note:** Always use a specific stable version to avoid unexpected breaking changes.

---

## ✅ **Step 4: Test n8n in interactive mode**

```bash
sudo docker run -it --rm \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n:1.45.1
```

✔️ If successful, you will see:

```
n8n ready on 0.0.0.0, port 5678
```

🔴 **To stop:** Press `Ctrl + C`

---

## ✅ **Step 5: Run n8n in detached mode (production)**

```bash
sudo docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -e N8N_SECURE_COOKIE=false \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n:1.45.1
```

✔️ **Explanation:**

* `-d`: Runs container in background.
* `--restart unless-stopped`: Auto restarts on VM reboot.
* `N8N_SECURE_COOKIE=false`: Disables secure cookie warning for HTTP testing (enable HTTPS in production).

---

## ✅ **Step 6: Access n8n**

Open in browser:

```
http://[your-external-ip]:5678
```

🔒 **Important:** For production, setup HTTPS using **NGINX + Certbot**.

---

## 📾 **📝 Troubleshooting Tips**

* **Port not accessible:** Check GCP firewall rules (allow TCP:5678).
* **Permission errors:** Ensure correct ownership with `sudo chown -R 1000:1000 ~/.n8n`.
* **Slow install or stuck upgrade:** Create a swap file to supplement micro VM RAM.

---

## 🎉 **Outcome**

✅ You now have **n8n installed and running live** on your GCP server, ready for AI WhatsApp automation in the next module.

---

**Author:** Mohd Hisyamudin
**Mini Course:** BUILDS – Panduan Zero to Hero AI WhatsApp Automation

---
