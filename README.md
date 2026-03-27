# Windows-Security-SOC-Automation
PowerShell scripts to monitor for Security Events like Brute Force (4625) and New User Creation (4720).

# 🛡️ Windows Security SOC Automation

"This project focuses on real-time security monitoring and incident response for corporate environments. It leverages PowerShell for advanced log extraction and automated auditing of critical security events, specifically tracking:

## 🚀 Key Features
## Brute Force Detection: 
   
Monitors **Event ID 4625 (Failed Logons)** to identify unauthorized access attempts or brute-force attacks, and tracks **Event ID 4624 (Successful Logons)** to audit valid user access.

  **Command:**
  
          Get-EventLog -LogName Security -InstanceId 4624, 4625 -Newest 20
  
<img width="915" height="542" alt="image" src="https://github.com/user-attachments/assets/c370e33b-8306-4c9f-898f-60c07aaafac2" />

 ## Persistence Monitoring: 
 
Tracks **Event ID 4720 (New User Creation)** and **Event ID 4726 (User Deletion)** to detect and prevent unauthorized hacker backdoors. This ensures that every account lifecycle event is recorded for security forensic analysis.
  
  ### Windows User Auditing (Event ID 4720 & 4726)

This project demonstrates how to monitor **Persistence** on a Windows system by tracking user account creation and deletion. Monitoring these events is crucial to           prevent hackers from creating backdoor accounts.

## 🛠️ Persistence Monitoring Workflow

###  Enable Auditing (Prerequisite)
Ensure that "User Account Management" auditing is enabled to record these events:

     auditpol /set /subcategory:"User Account Management" /success:enable

***1. Create a Test User:*** Use this command to simulate a new user creation:

      New-LocalUser -Name "CheckAudit4720" -NoPassword
  
 ***2. Audit New User Creation (Event ID 4720):** Verify if the system successfully logged the account creation:

      Get-EventLog -LogName Security -InstanceId 4720

-<img width="735" height="356" alt="image" src="https://github.com/user-attachments/assets/ee62812c-6146-4f7d-9685-b67af1a62496" />

***3. Remove the Test User:*** Clean up by deleting the test account:

      Remove-LocalUser -Name "CheckAudit4720"

***4. Audit User Deletion (Event ID 4726):*** Verify that the system logged the account removal:

      Get-EventLog -LogName Security -InstanceId 4726

  
<img width="732" height="184" alt="image" src="https://github.com/user-attachments/assets/b8789690-d4fa-467d-b377-7ff231fb8bcb" />

<img width="842" height="130" alt="image" src="https://github.com/user-attachments/assets/53f14da1-9c13-4dfb-8f94-82e3803170f4" />


- **EDR Deployment:** Documented experience in deploying **SentinelOne (S1)** agent.
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
