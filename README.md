# 🛡️ ThreatDetect-Lab: SSH Brute-Force Attack Detection using Wazuh SIEM

**A hands-on, end-to-end SOC Blue Team project focusing on detection, correlation, and analysis of a common intrusion technique in a controlled lab environment.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Technology: Wazuh SIEM](https://img.shields.io/badge/SIEM-Wazuh-007bff.svg)](https://wazuh.com/)
[![Framework: MITRE ATT&CK](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red.svg)](https://attack.mitre.org/)

---

## 📌 Project Overview & Objectives

This project is a detailed simulation of a real-world Security Operations Center (SOC) workflow, demonstrating the automated detection and professional analysis of an **SSH brute-force attack** against a Linux endpoint using **Wazuh SIEM**.

The lab is designed to be **reproducible, beginner-friendly, and interview-ready**.

### 🎯 Key Learning Objectives

* **Detect:** Implement rules to detect sequential SSH authentication failures.
* **Correlate:** Understand how Wazuh correlates individual failed logs into a high-severity brute-force incident.
* **Investigate:** Practice SOC L1 / early L2 triage and investigation skills.
* **Map:** Analyze alerts using the **MITRE ATT&CK Framework** (specifically **T1110: Brute Force**).
* **Document:** Produce professional SOC-style incident reports and analysis documentation.

---

## 🧪 Lab Architecture & Tools

The lab consists of three virtual machines connected via a **Bridged Network Adapter** to ensure proper inter-VM communication and simulation integrity.

| Category | Component | Description |
| :--- | :--- | :--- |
| **SIEM & Monitoring** | Wazuh Manager | Central correlation, rule engine, and alerting. |
| **Endpoint Agent** | Wazuh Agent | Collects and forwards logs from the victim machine. |
| **Victim OS** | Ubuntu Linux | Target endpoint running OpenSSH (log source). |
| **Attacker OS** | Kali Linux | Used to launch the attack. |
| **Attack Tool** | Hydra | Used for brute-force attack simulation. |
| **Framework** | MITRE ATT&CK | Used for incident classification and analysis. |

*----------------------- Visual proof of environment setup is available in: `screenshots/01_all_three_vm_running.png`* ------------------

---

## 🏗️ Implementation Flow & Technical Steps

The project follows a five-step professional workflow from deployment to final analysis.

### Step 1: Environment Preparation

* Deployed Wazuh Manager, Ubuntu Endpoint, and Kali Linux VMs.
* Configured the network and verified SSH service status on the victim.
* --------------- *Installation proof: `screenshots/03_wazuh_dashboard.png`* -------------------------

### Step 2: Endpoint Onboarding

* Installed and configured the **Wazuh Agent** on the Ubuntu endpoint.
* Verified the agent successfully connected to the Wazuh Manager dashboard, ensuring real-time log ingestion.
* ----------------- *Onboarding proof: `screenshots/04_adding_agent.png`* -------------------------------

### Step 3: Attack Simulation

The attack was launched from the Kali machine using the powerful multi-threaded brute-forcing tool, Hydra.

```bash
hydra -l root -P passwords.txt ssh://<victim-ip>

--------------------- Attack execution proof: screenshots/05_attacking-on_victim.png -------------------------------

### Step 4: Detection & Correlation

Wazuh detected numerous low-severity authentication failures (Rule 5712).

The Wazuh rule engine correlated these sequential failures into a single high-severity alert (Rule 5760) for SSH Brute Force Attack Detected.

---------------- Correlation and severity escalation proof: screenshots/07_Correlated_SSH_Bruteforce_Alerts.png --------------------------

### Step 5: Alert Analysis & Mapping
Analyzed the correlated alert details (Source IP, Target User, Log Source).

The activity was successfully mapped to the MITRE ATT&CK Initial Access tactic, specifically T1110: Brute Force.

---------------- Detailed analysis and MITRE mapping proof: screenshots/06_SSH_BruteForce_Detection_MITRE.png ----------------------------

### 🧾 Professional Deliverables (Proof of Work)
The core output of this lab is professional documentation, demonstrating the ability to communicate technical findings clearly.

Document,File Path,Content
Incident Report,docs/incident-report.md,"Executive summary, detection details, MITRE ATT&CK analysis, impact assessment, and remediation recommendations."
Attack Flow Diagram,docs/attack-flow.md,"A concise, 1-minute visual walkthrough of the entire lab (Setup, Attack, Log Generation, Detection, Analysis)."

 #####🧠 Skills Demonstrated

This project showcases core competencies essential for Security Analysts and Blue Team roles:

SIEM Administration: Deployment, configuration, and log source onboarding (Wazuh).

Threat Detection: Understanding rule logic and correlation techniques.

Alert Triage & Investigation: Analyzing alert details (source, target, time, rule ID).

Cybersecurity Frameworks: Practical application and mapping of MITRE ATT&CK.

Incident Documentation: Creating formal, structured reports.

## ⚙️ Troubleshooting & Resolution

This section highlights common technical hurdles encountered during the setup process and their professional resolutions, demonstrating real-world problem-solving skills.

| Issue | Root Cause | Professional Resolution |
| :--- | :--- | :--- |
| **Dashboard Inaccessibility** | Virtual machine network configuration using NAT. | Switched all VMs to a **Bridged Network Adapter** to ensure correct IP addressing. |
| **Agent Not Connecting** | Incorrect Wazuh Manager IP specified in the agent's configuration file. | Corrected the agent's `client.keys` or `ossec.conf` file. |
| **No Alerts Visible** | OpenSSH service was not running or firewall blocks existed. | Verified and enabled the OpenSSH service (`systemctl enable ssh`). |