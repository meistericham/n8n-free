# 🚀 BUILDS Module 2: Install & Deploy n8n using Docker + Update Guide (with Backup)

This guide helps you **install and deploy n8n** on your GCP VM quickly and avoid common installation errors, plus includes how to **update to the latest n8n image with backup**.

---

## 🔷 📌 Prerequisites

* GCP VM (e2-micro, Ubuntu 22.04 LTS recommended)
* Firewall open for TCP:5678
* Optional: swap file for micro VM stability

---

## ✅ Step 1: Update system & install Docker

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

---

## ✅ Step 2: Prepare n8n data directory

```bash
mkdir ~/.n8n
sudo chown -R 1000:1000 ~/.n8n
```

---

## ✅ Step 3: Pull n8n stable image

```bash
sudo docker pull n8nio/n8n:1.45.1
```

---

## ✅ Step 4: Test in interactive mode

```bash
sudo docker run -it --rm \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n:1.45.1
```

Press Ctrl+C to stop.

---

## ✅ Step 5: Run in detached mode

```bash
sudo docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -e N8N_SECURE_COOKIE=false \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n:1.45.1
```

---

## ✅ Step 6: Access n8n

Go to `http://[your-external-ip]:5678`

---

## 🔷 🔄 Step 7: Update to latest n8n image (with backup)

1. **Create backup first (important):**

```bash
cp -r ~/.n8n ~/.n8n-backup
```

2. **Stop & remove** old container:

```bash
sudo docker stop n8n
sudo docker rm n8n
```

3. **Pull latest image:**

```bash
sudo docker pull n8nio/n8n
```

4. **Run updated container:**

```bash
sudo docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -e N8N_SECURE_COOKIE=false \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

---

## ✅ Outcome

n8n is installed, backed up, and updated, ready for AI WhatsApp automation.

---

**Author:** Mohd Hisyamudin
**Mini Course:** BUILDS – Panduan Zero to Hero AI WhatsApp Automation
