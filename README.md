# 🛡️ Phishing Awareness Simulation Lab (GoPhish + Ngrok)

> **Educational cybersecurity awareness and phishing simulation laboratory.**[cite: 2]

---

## 📊 REPOSITORY BADGES
![Platform](https://img.shields.io/badge/Platform-Kali_Linux-blue)
![Tool](https://img.shields.io/badge/GoPhish-v0.12.1-green)
![Tunnel](https://img.shields.io/badge/Ngrok-v3.39.1-orange)
![License](https://img.shields.io/badge/Purpose-Educational-red)

---

## ⚠️ DISCLAIMER
> **IMPORTANT:** This project is strictly for educational cybersecurity awareness, defensive research, and authorized simulation training purposes only[cite: 2].
>
> It demonstrates how phishing simulation campaigns operate in highly controlled sandbox environments to help users and organizations understand, recognize, and report social engineering vectors[cite: 2].
>
> *   ❌ **No real credentials are harvested**[cite: 2]
> *   ❌ **No malicious payloads are served**[cite: 2]
> *   ✔ **Only simulated test data is used for learning evaluation**[cite: 2]

---

## 📚 TABLE OF CONTENTS
*   [⚠️ DISCLAIMER](#%EF%B8%8F-disclaimer)
*   [📌 Project Overview](#-project-overview)
*   [🎯 Objectives](#-objectives)
*   [🧰 Tools Used](#-tools-used)
*   [📂 Project Structure](#-project-structure)
*   [🏗️ System Architecture & Attack Flow](#%EF%B8%8F-system-architecture--attack-flow)
*   [⚙️ Detailed Setup Process](#%EF%B8%8F-detailed-setup-process)
    *   [Phase 1: Environment & Tool Setup](#phase-1-environment--tool-setup)
    *   [Phase 2: Launching Server & Admin Setup](#phase-2-launching-server--admin-setup)
    *   [Phase 3: Building Campaign Components](#phase-3-building-campaign-components)
    *   [Phase 4: Run 1 - Baseline Simulation (Local Loopback)](#phase-4-run-1---baseline-simulation-local-loopback)
    *   [Phase 5: WAN Tunneling Integration (Ngrok)](#phase-5-wan-tunneling-integration-ngrok)
    *   [Phase 6: Run 2 - Live Simulation & Metric Capture](#phase-6-run-2---live-simulation--metric-capture)
*   [📊 Results & Observations](#-results--observations)
*   [🛡️ Post-Simulation Debrief (Defensive Engineering)](#%EF%B8%8F-post-simulation-debrief-defensive-engineering)
*   [🧹 Clean-Up Operations](#-clean-up-operations)
*   [🔍 Key Learnings](#-key-learnings)
*   [⚠️ Limitations](#%EF%B8%8F-limitations)
*   [🚀 Future Improvements](#-future-improvements)
*   [📚 References](#-references)
*   [👤 Author](#-author)

---

## 📌 PROJECT OVERVIEW
This portfolio project focuses on building an active, end-to-end phishing simulation laboratory environment[cite: 2]. In an enterprise environment, training programs utilize platforms like GoPhish to safely run simulated attacks, allowing security teams to measure click-through rates, gather baseline risk metrics, and design training material for vulnerable employees[cite: 2].

This project demonstrates both **network-isolated loopback sending checks** and **internet-accessible reverse proxy tunneling** to track interaction analytics in real-time[cite: 2].

---

## 🎯 OBJECTIVES
*   **Build an Enterprise Phishing Simulation Framework:** Successfully deploy GoPhish on Kali Linux[cite: 2].
*   **Establish Mail Transfer Agent (MTA) Relays:** Configure SMTP profiles to send secure, simulated mail templates[cite: 2].
*   **Implement Ingress Tunneling:** Bypass NAT and firewall configurations safely using Ngrok to allow inbound response tracking[cite: 2].
*   **Measure Human Vulnerability Risks:** Monitor live engagement metrics (Email Opens, Link Clicks, Timelines, User-Agents) safely inside the administrative console[cite: 2].
*   **Implement Defensive Controls:** Define detections, signatures, and configuration settings (SPF/DKIM/DMARC) to defend against malicious attempts[cite: 2].

---

## 🧰 TOOLS USED

| Tool | Category | Purpose |
| :--- | :--- | :--- |
| 🐉 **Kali Linux** | Operating System | Host deployment, local execution, and log verification[cite: 2] |
| 🛡️ **GoPhish v0.12.1** | Phishing Engine | Core simulation backend, dashboard metrics, and landing page management[cite: 2] |
| 🌐 **Ngrok v3.39.1** | Reverse Tunneling | Creating secure HTTPS tunnels to route external internet traffic back to local port 80[cite: 2] |
| 📧 **Gmail SMTP Relay** | Mail Transfer Agent | Safe outbound mail dispatch using Google Account App Passwords[cite: 2] |
| 🦊 **Firefox / Chrome** | Browser Testing | Testing dashboard administrative configurations & simulated user endpoints[cite: 2] |

---

## 📂 PROJECT STRUCTURE
The following tree describes the state of the active server workspace directory (`~/gophish-lab`) after initial installation and database schema creation[cite: 2]:

```text
~/gophish-lab/
├── gophish                             # Main compiled binary executable[cite: 2]
├── config.json                         # Configuration for port bindings (Admins: 3333, Phish: 80)[cite: 2]
├── gophish.db                          # SQLite local database (stores campaigns, users, templates)[cite: 2]
├── gophish_admin.crt                   # Auto-generated TLS administration certificate[cite: 2]
├── gophish_admin.key                   # Auto-generated private key for TLS[cite: 2]
├── templates/                          # Front-end user HTML designs[cite: 2]
├── static/                             # Web interface styles, images, and scripting files[cite: 2]
└── LICENSE / VERSION                   # System documentation[cite: 2]

---

🏗️ SYSTEM ARCHITECTURE & ATTACK FLOW
The network flow chart below outlines how the components work together to direct external targets through the reverse tunnel back to your local environment:

               +--------------------------------------------------------+
               |                    External Target                     |
               |                (Recipient Inbox Client)                |
               +--------------------------------------------------------+
                     |                                            ^
             (1) Recovers Email                            (3) Requests Phishing
             via SMTP Relay                                     Landing Page
                     |                                            |
                     v                                            v
     +-------------------------------+             +------------------------------+
     |   Gmail SMTP Relay Servers    |             |       Ngrok Edge Node        |
     |       (smtp.gmail.com)        |             |   (*.ngrok-free.dev)         |
     +-------------------------------+             +------------------------------+
                     ^                                            ^
                     | (Dispatches Phishing Mail)                 | (Proxies Inbound HTTPS)
                     |                                            |
     +----------------------------------------------------------------------------+
     |                       Your Kali Linux Local Machine (Ally)                 |
     |                                                                            |
     |  +--------------------+   (2) Establish Tunnel   +---------------------+   |
     |  |   Gophish Engine   |------------------------->|     Ngrok Agent     |   |
     |  |   (Port 80/3333)   |<-------------------------|    (Port 80 HTTP)   |   |
     |  +--------------------+  (4) Captures Metrics    +---------------------+   |
     +----------------------------------------------------------------------------+

---

## ⚙️ DETAILED SETUP PROCESS
🔹 Phase 1: Environment & Tool Setup
Ensure that dependency download utilities are updated inside your Kali system:

sudo apt update
sudo apt install wget unzip curl git -y
Construct your dedicated project workspace and move into it:

mkdir ~/gophish-lab
cd ~/gophish-lab
Download the official Gophish Linux 64-bit release zipped archive:

wget [https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip](https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip)
Extract the zip files:

unzip gophish-v0.12.1-linux-64bit.zip
🔹 Phase 2: Launching Server & Admin Setup
Add executable permissions to the binary, and start Gophish using sudo privileges (this is necessary to bind the web interface to HTTP port 80):

chmod +x gophish
sudo ./gophish
During initialization, check your stdout console logs to capture the temporary admin password generated:

time="2026-05-11T09:53:12-04:00" level=info msg="Please login with the username admin and the password f5fd937c07098e9c"

Navigate to the local admin interface: https://127.0.0.1:3333

At the login page, enter the default credentials:

Username: admin

Password: f5fd937c07098e9c

Click Sign in.

You will immediately be routed to the Reset Your Password page. Enter the temporary password, choose a strong custom password, and click Save Password.

Once saved, you will land on the main Gophish Dashboard.

🔹 Phase 3: Building Campaign Components
To execute a phishing simulation campaign, the four modular blocks of Gophish must be configured sequentially.

1. Landing Page Setup
Navigate to Landing Pages and click + New Page.

Set Name: Awareness-Test.

Click Save. (In real simulations, educational alerts or informational banners are designed here).

2. Email Template Setup
Navigate to Email Templates and click + New Template.

Set Name: Awareness-Email.

Set Envelope Sender: awareness@lab.local.

Set Subject: Security Awareness Exercise.

Navigate to the HTML tab and use:

  <p>Your account password will expire today.<br>
  Please reset it immediately.</p>
  <p><a href="{{.URL}}">Reset Password</a></p>
Save the template.
3. Users & Groups Configuration
Navigate to Users & Groups and click + New Group.

Set Name: Awareness-Test-Group.

Add the target simulation users:

User 1: First: text | Last: user | Email: dianeally08@gmail.com | Position: Engineer

User 2: First: text | Last: user | Email: delux6617@gmail.com | Position: Manager

Click Save changes.

4. Sending Profile (SMTP Relay) Configuration
Navigate to Sending Profiles and click + New Profile.

Set Name: gmail SMTP lab.

Set Interface Type: SMTP.

Set SMTP From: dianeally08@gmail.com.

Set Host: smtp.gmail.com:587.

Set Username: dianeally08@gmail.com.

Set Password: (Use your dedicated 16-character Google App Password).

Click Save Profile.

🔹 Phase 4: Run 1 - Baseline Simulation (Local Loopback)
The first test verified the configurations without external exposure.

Navigate to Campaigns ➔ + New Campaign.

Set Name: Awareness-Email (Baseline run).

Select Template: Awareness-Email.

Select Landing Page: Awareness-Test.

Set URL: http://127.0.0.1:3333 (Points internally).

Select Sending Profile: gmail SMTP lab.

Select Target Group: Awareness-Test-Group.

Click Launch Campaign.

Baseline Campaign Results: Outbound SMTP delivery successfully passed through Google. The Gophish dashboard showed 2 Emails Sent. However, because the target link pointed to a localized administrative IP, the emails could not reach back to the host.

Result Metrics: 2 Sent | 0 Opened | 0 Clicked | 0 Data Submitted.

🔹 Phase 5: WAN Tunneling Integration (Ngrok)
To solve the external routing restriction, Ngrok was used to configure a secure egress proxy.

Confirm Gophish is running and listening on port 80:

sudo ./gophish
Install and extract the Ngrok package:

tar -xvzf ngrok-v3-stable-linux-amd64.tgz
sudo mv ngrok /usr/local/bin/
ngrok version
Authenticate your Ngrok terminal agent using your private token:

ngrok config add-authtoken 3DcsX9wWraGOwXn1ZHIcf...
Expose local HTTP port 80 over the public WAN interface:

ngrok http 80
Ngrok Connection Telemetry Output
Session Status      online
Account             dianeally08@gmail.com (Plan: Free)
Version             3.39.1
Region              United States (us)
Latency             431ms
Forwarding          [https://available-spotter-sharpie.ngrok-free.dev](https://available-spotter-sharpie.ngrok-free.dev) -> http://localhost:80

The URL https://available-spotter-sharpie.ngrok-free.dev is the public forwarding URL.

🔹 Phase 6: Run 2 - Live Simulation & Metric Capture
Now a second campaign was created utilizing the active Ngrok forwarding link.

Navigate to Campaigns ➔ + New Campaign.

Set Name: Awareness-Test 2.

Select Template: Awareness-Email.

Select Landing Page: Awareness-Test.

Set URL: https://available-spotter-sharpie.ngrok-free.dev (Ngrok Forwarding Domain).

Set Launch Date: May 12th, 2026, 9:50 AM.

Select Sending Profile: gmail SMTP lab.

Select Target Group: Awareness-Test-Group.

Click Launch Campaign.

---

📊 RESULTS & OBSERVATIONS
Once the campaign was launched, external targets opened their simulated emails and clicked the links. GoPhish tracked and analyzed these live metrics:

2026-05-12 10:08:35  [Campaign Setup] Campaign Created - Awareness-Test 2
2026-05-12 10:08:39  [SMTP Relay] Dispatching outbound simulated emails...
2026-05-12 10:08:39  [Email Sent] Successfully delivered to dianeally08@gmail.com
2026-05-12 10:10:15  [Tracking Inbound] Target clicked tracking link (dianeally08@gmail.com)
                     └ Device: Android (OS Version: 10) | Browser: Chrome (Version: 138.0.0.0)

Campaign Comparison Matrix
Campaign	Target Count	Sent	Opened	Clicked	Submitted Data	Conversion Rate
Awareness-Test 1 (Local)	2	2	0	0	0 (None)	0%
Awareness-Test 2 (Tunnel)	2	2	1	1	0 (Disabled)	50%
Conclusion of Run 2: The second campaign verified that the attack chain worked, confirming the target clicked the link. Both the Gophish logs and Ngrok console verified real-time inbound requests.

🛡️ POST-SIMULATION DEBRIEF (DEFENSIVE ENGINEERING)
1. Mechanics of Tracking
Open Rate (1x1 Pixel): Gophish inserts an invisible image into HTML templates: <img src="https://available-spotter-sharpie.ngrok-free.dev/track?rid=unique_id" />. When the email client loads this pixel, the transaction maps back to that recipient in the database.

Click-Through (Link Modification): Gophish converts the {{.URL}} placeholder into a unique URL string: https://available-spotter-sharpie.ngrok-free.dev/?rid=unique_id. This registers the click on our server before loading the landing page.

2. Detections and System Protections
Network Detection (Spotting Tunneling Software)
Security Operations Centers (SOC) can locate unauthorized tunneling tools inside their environments using these detection concepts:

DNS Monitoring: Creating alerts for DNS queries containing known hosting subdomains (e.g., *.ngrok.io, *.ngrok-free.dev).

Process Spawning Analysis: Checking system events for executing commands like ngrok http or other tunnel patterns.

Persistent Outbound Connections: Firewalls can look for persistent outbound TCP connections to external proxies that don't match standard server traffic.

Technical Email Hardening
To prevent domain spoofing in live environments, configure correct email authentication tags on corporate domains:

SPF (Sender Policy Framework): Specifies which IP addresses are authorized to send mail for your domain.

DKIM (DomainKeys Identified Mail): Uses cryptographic keys to verify the email headers weren't altered in transit.

DMARC: Specifies how receiving servers should treat failed authentication checks (e.g., dropping the message or routing to spam).

---

🧹 CLEAN-UP OPERATIONS
After completing your simulation, it is critical to tear down the environment to prevent unauthorized access or reuse of exposed ports:

1. Terminate Active Ngrok Sessions: Press Ctrl+C in your terminal window running the Ngrok agent, or run the following command to kill any orphaned processes:

sudo pkill ngrok
2. Stop Gophish Engine: Stop the local web-listening process on port 80:

sudo pkill gophish
3. Clean Temporary Network Rules: Verify your listening ports are clear of active HTTP servers:

sudo lsof -i :80
sudo lsof -i :3333

---

🔍 KEY LEARNINGS
✔ Gophish Administration: Learned how to deploy, configure, and maintain a centralized phishing simulation platform.

✔ Ingress Tunneling: Handled reverse HTTP routing to route public web traffic safely back to local servers.

✔ SMTP Routing Integration: Experienced SMTP mail transfer setups, custom headers, and App Password configurations.

✔ Interaction Engineering: Analyzed user-agent metadata and timeline details to measure risk response rates.

---


