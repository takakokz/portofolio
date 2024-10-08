# Incident Response and Review Mini Sprint 

<b>Clicked provided this group project opportunity to work with others who are studying cybersecurity from Sep 23, 2024 to Oct 4, 2024. </b>
In this case study, the group worked the role of cybersecurity professionals tasked with identifying and mitigating threats using NIST Incident Response Profess Framework. After creating technical report, we developed an report and presentation to executives and related stakeholders. The content was designed to provide high-level insight fousing on the timeline, business impact, key takeaways, and future budget proposal to create proactive secure posture. 

# Overview
Unusual activity was detected on file transfer platform of the Healthcare facility.  
Senior management is taking this incident very sieriously since the medical data contained on the network. 
A total of 13 Windows logs were given to investigate what has happened, and we organized the logs into timeline shown below. 

# Technical Timeline all in PST
| Time | Description | Event ID |
| --- | --- | --- |
| 08:10:23 | Successful Remote Login by business user account A into DESKTOP-1234567 | Event ID 4624: Successful login via RDP (Remote Login, from IP 192.168.1.2) |
| 09:45:32 | Policy Change by ADMIN on DC-SERVER-01 | Event ID 4719: Modification of "Object Access" audit policy enabled by the Administrator account. |
| 10:32:17 -10:32:21 | 2 Failed Admin Login Attempts and 1 success  from IP 192.168.1.100 | Events ID 4624/4625: Two failed attempts followed by a successful login using DESKTOP-1234567 with Admin previlege |
| 10:33:45 | Firewall detected unusual access to SMB protocol | Event 2004: Warnig : Unusual behavior accessing from IP 192.168.1.100 to 192.168.1.1 over TCP port 445(SMB) |
| 12:01:15 | Application Error on DESKTOP-1234567 | Event 1000: Error in explorer.exe, indicating potential malicious activity. |
| 13:23:15 |  Firewall detected unusual access from DESKTOP-1234567 | Event ID 2004: Another modification allows traffic over TCP port 22 (SSH) from 192.168.1.25 to 192.168.1.1. |
| 14:10:12 | Blocked DNS Request | Event ID 861: An application running under business user account A on DESKTOP-1234567 attempted a UDP connection on port 53 (DNS), which was blocked. |
| 15:23:52 | MSSQL I/O Error on SQLSERVER-12345 | Event ID 823: I/O error indicates potential data corruption |
| 15:34:56 | Continued Failed Login Attempts | Event ID 4625: Another failed admin login attempt occurred on DESKTOP-1234567 from IP 192.168.1.50 |
| 16:45:32 | Inbound TCP connection attempt to SERVER-12345 over port 80 | Event ID 5156: Unknown application communicating over HTTP (port 80). |
| 17:34:56 |  Failed Local Logon Attempt on SERVER-12345 | Event ID 529: A failed local login attempt using Admin on SERVER-12345 |

<h2>Identification and Investigation</h2>
A malicious actor obtained the credential of a business user(Account A) to initiate remote access. It is likely that the attacker enabled an audit policy to identify previleged accounts and search for databases containing sensitive information. Following successful brute force attack, the attacker compromised the administrator's account.

The firewall generated two alerts indicating attempts to access the router via vulnerable SMB and SSH protocol. Additionally, application log shows suspicious activity, wtith potential malicious program running in the background of explorer.exe. The MSSQL server indicates I/O error, suggesting potential data curruption, while unknown applications communicating over port 80 raised concern about potential data exfilteration. Throughout logs, it indicated that the malicious actor traversed multiple internal network segments, suggesting successful lateral movement within the network. 

<h2>Containment Plans</h2>
A security incident has been detected in the healcare facility's IT infrastructure, potentially compromising patient data and system integrity. This plan outlines our immediate and long-term responses, focusing on minimizing business impact and financial risk.

<h3>Short Term Plan</h3>
| Control Identifier | Control Name | Control/Action to Take |
| --- | --- | --- |
| 08:10:23 | Successful Remote Login by business user account A into DESKTOP-1234567 | Event ID 4624: Successful login via RDP (Remote Login, from IP 192.168.1.2) |
