# 📲 Module 3: Integrate WhatsApp API (Wasapmatic)

Welcome to **Module 3** of the BUILDS Mini Course – Zero to Hero AI WhatsApp Automation.

In this module, you will:

* ✅ Understand what Wasapmatic is
* ✅ Register a Wasapmatic account
* ✅ Setup device and obtain API Key
* ✅ Test basic API call using `curl`

---

## 💡 What is Wasapmatic?

Wasapmatic is a **third party WhatsApp API provider** that:

* Provides REST API to send WhatsApp messages
* Easy to use and affordable for beginners
* Includes a **Free Tier** for testing (e.g. daily credits)

---

## 📝 Step 1: Register Wasapmatic Account

1. Go to [wasapmatic.com](https://wasapmatic.com)
2. Click **Sign Up / Register**
3. Enter your email and password
4. Verify your email to activate your account

---

## 🛠️ Step 2: Setup Device and Get API Key

1. Login to Wasapmatic Dashboard
2. Go to **Devices / My Devices**
3. Click **Add New Device**
4. Scan the QR code using your WhatsApp Business app
5. Once connected, **copy your API Key / Bearer Token**

---

## ⚠️ Step 3: Test API Call Using curl

Before integrating into n8n, test using curl in your terminal or SSH:

```bash
curl -X POST "https://app.wasapmatic.com/api/send/whatsapp" \
     -H "Content-Type: multipart/form-data" \
     -F "secret=YOUR_API_SECRET" \
     -F "account=WHATSAPP_ACCOUNT_UNIQUE_ID" \
     -F "recipient=RECIPIENT_PHONE_NUMBER" \
     -F "type=text" \
     -F "Hello, this is a test from Wasapmatic API!"
```

✅ Replace:

* `[YOUR_API_KEY]` with your Wasapmatic API Key
* `60123456789` with your phone number (in international format, no + sign)

---

### 💡 **Note:**

* `curl` can be used in **Linux Terminal, macOS Terminal, Windows CMD (Win10+), PowerShell, Git Bash, and WSL**.
* If `curl` is not installed, install with:

```bash
sudo apt update
sudo apt install curl -y
```

---

## 🌟 Outcome

By the end of this module, you should have:

✅ Registered a Wasapmatic account
✅ Connected your WhatsApp device
✅ Obtained your API Key
✅ Successfully sent a test message via API

---

### 🚀 **Next Module**

In **Module 4**, we prepare databse for the automation system for WhatsApp messaging.

---

* **Author:** Mohd Hisyamudin
* **Mini Course:** BUILDS – Panduan Zero to Hero AI WhatsApp Automation
