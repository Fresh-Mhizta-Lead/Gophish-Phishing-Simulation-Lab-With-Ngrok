
```markdown
# 🛡️ Phishing Awareness Simulation Lab (GoPhish + Ngrok)

---

## 📌 OVERVIEW

This project is an educational cybersecurity lab that demonstrates how phishing simulation campaigns are built and analyzed using GoPhish and Ngrok.

It focuses on safe security awareness training, not real-world attacks.

---

## ⚠️ DISCLAIMER

### 🚨 Educational Use Only

This project is strictly for **learning and cybersecurity awareness**.

### ❌ Not for:
- Real phishing attacks
- Unauthorized data collection
- Malicious use

### ✔ For:
- Cybersecurity training
- Defensive research
- Awareness simulations

---

## 🎯 OBJECTIVES

- Deploy GoPhish phishing simulation tool
- Configure SMTP email delivery system
- Create phishing campaigns safely
- Track email opens and clicks
- Expose system using Ngrok tunneling
- Understand phishing detection techniques

---

## 🧰 TOOLS USED

- Kali Linux
- GoPhish v0.12.1
- Ngrok v3.39.1
- Gmail SMTP (App Password)
- Web Browser (Testing)

---

## 📂 PROJECT STRUCTURE

```

~/gophish-lab/
├── gophish
├── config.json
├── gophish.db
├── gophish_admin.crt
├── gophish_admin.key
├── templates/
├── static/
└── LICENSE

```

---

## 🏗️ SYSTEM ARCHITECTURE

```

Email Inbox
↓
SMTP Server (Gmail)
↓
GoPhish (Kali Linux)
↓
Ngrok Tunnel
↓
Landing Page Tracking System

````

---

## ⚙️ INSTALLATION & SETUP

### Step 1: Install Dependencies

```bash
sudo apt update
sudo apt install wget unzip curl git -y
````

---

### Step 2: Create Workspace

```bash
mkdir ~/gophish-lab
cd ~/gophish-lab
```

---

### Step 3: Install GoPhish

```bash
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
unzip gophish-v0.12.1-linux-64bit.zip
chmod +x gophish
sudo ./gophish
```

---

### Step 4: Login Credentials

* Username: `admin`
* Password: (auto-generated in terminal)

---

## 📧 CAMPAIGN CONFIGURATION

### Landing Page

* Name: Awareness-Test

---

### Email Template

```html
<p>Your account password will expire today.</p>
<p><a href="{{.URL}}">Reset Password</a></p>
```

---

### Target Users

* Engineer → [dianeally08@gmail.com](mailto:dianeally08@gmail.com)
* Manager → [delux6617@gmail.com](mailto:delux6617@gmail.com)

---

### SMTP Settings

* Host: smtp.gmail.com:587
* Username: Gmail account
* Password: App Password

---

## 🌐 NGROK SETUP

### Start Tunnel

```bash
ngrok http 80
```

---

### Public URL Example

```
https://your-subdomain.ngrok-free.app
```

---

## 📊 RESULTS

| Campaign       | Sent | Opened | Clicked | Status      |
| -------------- | ---- | ------ | ------- | ----------- |
| Local Test     | 2    | 0      | 0       | No tracking |
| Ngrok Campaign | 2    | 1      | 1       | Successful  |

---

## 🛡️ SECURITY INSIGHTS

### Tracking Methods

* Email tracking pixel (open detection)
* Unique URLs for click tracking

### Defensive Measures

* Detect Ngrok domains
* Monitor suspicious tunnels
* Enforce SPF, DKIM, DMARC

---

## 🧹 CLEANUP

```bash
sudo pkill ngrok
sudo pkill gophish
sudo lsof -i :80
sudo lsof -i :3333
```

---

## 🔍 KEY LEARNINGS

* Phishing simulation lifecycle
* SMTP configuration process
* Real-time tracking systems
* Reverse tunneling concepts
* Cybersecurity awareness techniques

---

## ⚠️ LIMITATIONS

* Ngrok URLs are temporary
* Email delivery may be rate-limited
* No real credential harvesting

---

## 🚀 FUTURE IMPROVEMENTS

* Add SSL (HTTPS)
* Use custom domain instead of Ngrok
* Improve analytics dashboard
* Add automated reporting system

---

## 📚 REFERENCES

* GoPhish Documentation
* Ngrok Documentation
* MITRE ATT&CK (T1566 Phishing)
* CISA Cybersecurity Guidelines

---

## 👤 AUTHOR

**Diane Ally Lamine**
Cybersecurity Awareness & Simulation Project

```

---

If you want next upgrade, I can make it look like a **top-tier GitHub cybersecurity repo (with banners, screenshots section, collapsible modules, and professional spacing like real pentest portfolios)**.
```

