# 🚀 Self-Hosting n8n on a Linux Server Using Docker (External IP Setup)
By: Mohd Hisyamudin


This guide provides **step-by-step instructions** to self-host [n8n](https://n8n.io), a free and open-source workflow automation tool, on a Linux server using **Docker** and access it via your **external IP address** (no domain or SSL setup required).


---

## ✅ **Step 1: Installing Docker**

1. **Update the package index:**

```bash
sudo apt update
```

2. **Install Docker:**

```bash
sudo apt install docker.io -y
```

3. **Start Docker:**

```bash
sudo systemctl start docker
```

4. **Enable Docker to start at boot:**

```bash
sudo systemctl enable docker
```

5. **Check Docker version (optional):**

```bash
docker --version
```

---

## ✅ **Step 2: Starting n8n in Docker**

**Run the following command to start n8n in Docker.**

Since you are using **external IP (no domain)**, you do not need to set N8N\_HOST or SSL environment variables.

```bash
sudo docker run -d --restart unless-stopped \
--name n8n \
-p 5678:5678 \
-v ~/.n8n:/home/node/.n8n \
n8nio/n8n
```

### 🔎 **Explanation:**

* **`docker run -d --restart unless-stopped`**: runs container in background and restarts if server reboots
* **`--name n8n`**: names the container `n8n`
* **`-p 5678:5678`**: maps port 5678 on the server to n8n
* **`-v ~/.n8n:/home/node/.n8n`**: mounts a volume to persist n8n data
* **`n8nio/n8n`**: uses the official n8n Docker image

---

## ✅ **Step 3: Accessing n8n Web Interface**

Once the container is running, you can access n8n at:

```
http://[your-server-external-ip]:5678
```

### 💡 **Example:**

If your external IP is `34.123.45.67`, open:

```
http://34.123.45.67:5678
```

---

### 🛡️ **Important Note:**

* This setup uses **HTTP only**, suitable for **learning, testing, and development purposes**.
* For **production deployment**, you should set up **SSL with a domain name** for secure HTTPS access.

---

## ✅ **Step 4: Managing n8n Docker Container**

Here are **common commands** to manage your n8n container:

* **Check running containers:**

```bash
docker ps
```

* **Stop n8n container:**

```bash
docker stop n8n
```

* **Start n8n container again:**

```bash
docker start n8n
```

* **View container logs (optional troubleshooting):**

```bash
docker logs -f n8n
```

---

## 🎯 **Conclusion**

By following this guide, you have successfully:

* Installed Docker on your Linux server
* Started n8n using Docker
* Accessed n8n using your server’s external IP

---

✨ **You are now ready to build your workflows and automation with n8n!**

---

Let me know if you want this formatted into **your course slides and Notion notes** for immediate preparation this week.

---

*(End of Document)*
