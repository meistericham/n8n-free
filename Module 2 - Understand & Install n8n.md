# 🚀 BUILDS Module 2: Understand & Install n8n (Install & Deploy n8n using Docker + Update Guide - with Firewall, Backup & Explanations)

This guide helps you **install and deploy n8n** on your GCP VM quickly and avoid common installation errors, plus includes how to **update to the latest n8n image with backup**, with explanations for each command clearly placed **as notes below commands** to avoid copy-paste confusion.

---

## 🔷 📌 Prerequisites

* GCP VM (e2-micro, Ubuntu 22.04 LTS recommended)
* Optional: swap file for micro VM stability (to avoid out-of-memory issues)

---

## ✅ Step 0: Configure Firewall Rule

Before installing n8n, configure your firewall to allow public access:

1. Go to **VPC Network > Firewall rules** in GCP console.
2. Click **“CREATE FIREWALL RULE.”**
3. Name: `allow-n8n`
4. Targets: `All instances in the network` or specify your VM.
5. Source IP ranges: `0.0.0.0/0`
6. Protocols and ports: Select **“Specified protocols and ports”**, tick **tcp**, and enter `5678`.
7. Click **“Create.”**

**Note:** This allows external devices to access your n8n app running on port 5678. Ensure you use strong authentication and switch to HTTPS for production.

---

## ✅ Step 1: Update system & install Docker

```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

**Note:**

* `apt update` updates package list.
* `apt install docker.io -y` installs Docker.
* `systemctl start docker` starts Docker immediately.
* `systemctl enable docker` ensures Docker starts on reboot.

---

## ✅ Step 2: Prepare n8n data directory

```bash
mkdir ~/.n8n
sudo chown -R 1000:1000 ~/.n8n
```

**Note:**

* `mkdir ~/.n8n` creates data folder for workflows.
* `chown` changes ownership to allow Docker access without permission issues.

---

## ✅ Step 3: Pull n8n stable image

```bash
sudo docker pull n8nio/n8n:1.45.1
```

**Note:** Downloads specific stable version to your VM.

---

## ✅ Step 4: Test in interactive mode

```bash
sudo docker run -it --rm \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n:1.45.1
```

**Note:**

* Runs n8n interactively to check for errors.
* `-it` interactive mode.
* `--rm` auto deletes container when stopped.
* `-p` maps port 5678.
* `-v` mounts local folder for data persistence.

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

**Note:**

* Runs in background with auto restart.
* Disables secure cookie for HTTP testing (use HTTPS in production).

---

## ✅ Step 6: Access n8n

Go to `http://[your-external-ip]:5678` in browser.

---

## 🔷 🔄 Step 7: Update to latest n8n image (with backup)

1. **Create backup first (important):**

```bash
cp -r ~/.n8n ~/.n8n-backup
```

**Note:** Creates a backup copy of your workflows and credentials.

2. **Stop & remove old container:**

```bash
sudo docker stop n8n
sudo docker rm n8n
```

**Note:** Stops and removes current running container to avoid conflict with updated one.

3. **Pull latest image:**

```bash
sudo docker pull n8nio/n8n
```

**Note:** Downloads the newest available version.

4. **Run updated container:**

```bash
sudo docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -e N8N_SECURE_COOKIE=false \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

**Note:** Starts n8n with updated image while using the same data folder.

---

## ✅ Outcome

You now have **n8n installed, firewall configured, backed up, and updated** on your GCP VM, ready for your AI WhatsApp automation workflows.

---

**Author:** Mohd Hisyamudin
**Mini Course:** BUILDS – Panduan Zero to Hero AI WhatsApp Automation
