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


