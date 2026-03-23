# Windows-Security-SOC-Automation
Python and PowerShell scripts to monitor 41+ Endpoints for Security Events like Brute Force (4625) and New User Creation (4720).

# 🛡️ Windows Security SOC Automation

This project focuses on real-time security monitoring and incident response for a corporate environment with **41+ endpoints**. It uses a combination of **PowerShell** for log extraction and **Python** for automated alerting.

## 🚀 Key Features
- **Brute Force Detection:** Monitors **Event ID 4625** (Failed Logons) to identify unauthorized access attempts.
- **Persistence Monitoring:** Tracks **Event ID 4720** (New User Creation) to prevent hacker backdoors.
- **EDR Deployment:** Documented experience in deploying **SentinelOne (S1)** agents across 41 systems.
- **Real-time Alerts:** Integrated with **Telegram/WhatsApp API** for immediate mobile notifications.

## 🛠️ Tools & Technologies
- **SIEM/Monitoring:** Splunk (Learning), Windows Event Viewer
- **EDR:** SentinelOne
- **Scripting:** Python, PowerShell
- **Remote Access:** AnyDesk Security Monitoring

## 📂 Project Structure
- `monitor_logins.ps1`: Script to fetch failed/success login events.
- `alert_system.py`: Python script to send alerts to mobile devices.
- `network_scan.bat`: Basic network port auditing script.

## 🎯 Goal
My goal is to transition from IT Support to a professional SOC Analyst role by automating security workflows and protecting enterprise environments.
