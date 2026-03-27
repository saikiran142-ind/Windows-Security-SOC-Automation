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

### 🛡️ Advanced Security Audits

These advanced checks help identify more sophisticated attacks like privilege escalation and log tampering.

*   **⚡ Privilege Escalation (Event ID 4732):**
    Tracks when a user is added to the **Administrators** group. This is a common step for attackers to gain full control.
    ```powershell
    Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4732} -ErrorAction SilentlyContinue
    ```

*   **🧹 Log Tampering (Event ID 1102):**
    Detects if the **Security Log** was cleared. Attackers do this to hide their tracks (Anti-Forensics).
    ```powershell
    Get-WinEvent -FilterHashtable @{LogName='Security'; Id=1102} -ErrorAction SilentlyContinue
    ```

*   **🌐 Live Network Connections (C2 Detection):**
    Audits active TCP connections to identify potential **Command & Control (C2)** traffic or data exfiltration.
    ```powershell
    Get-NetTCPConnection -State Established | Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, OwningProcess | Format-Table -AutoSize
    ```


> [!TIP]
> **💡 Pro Tip:** If no events are found, it means no recent privilege escalation activities have occurred. You can test this by adding a user to the Local Administrators group to verify auditing is working correctly.



- **EDR Deployment:** Documented experience in deploying **SentinelOne (S1)** agent.
- **Real-time Alerts:** Integrated with **Telegram/WhatsApp API** for immediate mobile notifications.

## 🛠️ Tools & Technologies
- **SIEM/Monitoring:** Splunk (Learning), Windows Event Viewer
- **EDR:** SentinelOne
- **Scripting:** Python, PowerShell
- **Remote Access:** AnyDesk Security Monitoring

### 🛡️ Incident Response Workflow (IR Plan)

In a real-world security scenario, if any critical events like **4720** or **4625** are detected, I follow this structured Incident Response (IR) plan:

*   **🔍 Identification:** Use `Get-EventLog` or `Get-WinEvent` to identify unauthorized user creation (4720) or persistent brute-force attempts (4625).
*   **🚫 Containment:** Immediately **Isolate** the compromised endpoint from the network using the **SentinelOne (S1)** agent to prevent lateral movement.
*   **🕵️ Investigation:** Analyze the source IP, check for Privilege Escalation, and audit any unauthorized system changes made by the suspicious user.
*   **🛠️ Remediation:** Remove the unauthorized user account, reset local administrator passwords, and clear any persistent backdoors to restore system integrity.
*   

💡 Pro Tip: If no events are found, it means no recent privilege escalation activities have occurred. You can test this by adding a user to the Local Administrators group

## 🎯 Goal
My goal is to transition from IT Support to a professional SOC Analyst role by automating security workflows and protecting enterprise environments.
