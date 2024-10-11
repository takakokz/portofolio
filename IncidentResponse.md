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


- A malicious actor obtained the credential of a business user(Account A) to initiate remote access. 
- It is likely that the attacker enabled an audit policy to identify previleged accounts and search for databases containing sensitive information. 
- Following successful brute force attack, the attacker compromised the administrator's account.

- The firewall generated two alerts indicating attempts to access the router via vulnerable SMB and SSH protocol. - Additionally, application log shows suspicious activity, wtith potential malicious program running in the background of explorer.exe.
- The MSSQL server indicates I/O error, suggesting potential data curruption, while unknown applications communicating over port 80 raised concern about potential data exfilteration.
- Throughout logs, it indicated that the malicious actor traversed multiple internal network segments, suggesting successful lateral movement within the network. 

<h2>Containment Plans</h2>
A security incident has been detected in the healcare facility's IT infrastructure, potentially compromising patient data and system integrity. This plan outlines our immediate and long-term responses, focusing on minimizing business impact and financial risk.

<h3>Short Term Plan</h3>

| Control Identifier | Control Name | Control/Action to Take |
| --- | --- | --- |
| AC-2(3) | Disable Accounts | Disable business account A which was used in violation of organizational policy |
| IA-5 | Authenticator Management | Action: Force password reset for all admin accounts and users on affected systems |
| SC-7 | Boundary Protection | Disallow traffic on ports 445 and 22. Firewall reconfiguration helps to prevent future remote access attempts from malicious actors. |
| IR-4(3) | Incident Handling | Incident response actions - Shutdown affected system |
| IR-4(12) | Malicious Code and Forensic Analysis | Analyze malicious code and/or other residual artifacts remaining in the system after the incident. Identify & remove persistent backdoors to prevent future unauthorized access. |
| IR-4(15) | Public Relations and Reputation Repair | If more than 500 patients' PHI is compromised, manage public relations associated with the public |
| IR-7 | Information Spillage Response | Identifying the specific data involved in the system contamination. Isolating the contaminated system or system component. Eradicating the data from the contaminated system or component; |
| IR-7 | Incident Response Assistance | Utilize organization response support resources, including help desks, assistance groups, automated ticketing systems to open and track incident response tickets, and access to forensics or consumer redress services when required. |

<h2>Post Incident Review</h2>

<h3>Timeline to report executives what has happened</h3>

![image](https://github.com/user-attachments/assets/2805d720-c97b-4057-8588-80413435b7fe)


- By getting support from external cybersecurity experts from NoMoreAttack Inc. from Sep 22, forensic analysis was conducted to determine the extent of the breach, identify compromised data, and trace the attacker’s action within the network. 
- Communication with affected patients, regulators, and the public media was conducted to show transparency with timely updates on the incident, action taken, the hacker group involved
- Established the call center to respond to inquiries where individuals can learn if their information was involved in the breach and inform them of potential effects.  The toll-free phone number is listed on the website until Dec 20, 2023. 

<h3>Analyze Business Impact</h3>

![image](https://github.com/user-attachments/assets/f41e3e32-5c6d-4cfb-82ae-c92413e7d894)
Although cyber liability insurance covers most expenses, reputation damage hurt the facility's image. 

<h3>Lessons Learned and Preventitive Measure</h3>


- PEOPLE - Incident Response & Security Awareness Training
- PROCESS - Privilege Management
- TECHNOLOGY - System Monitoring
![image](https://github.com/user-attachments/assets/cb8e1193-dec4-487a-bd92-2f953b2f2553)


# Conclusion 
Throughout this project, I learned from other members that there are multiple ways to analyze an incident. The data provided was not enough to see full picture of the incident, which in a way, was beneficial as it required us to work with limited information. I felt it was similar to real-workd situations that comapnies often face. Our group presented to the instructer every session, and instructor's feedback helped us identify areas where we needed improvement. Initially, we approached the project with a technical mindset, but we soon realized that the final presentation needed to be tailored to executives, so we minimize technical words as much as possible. In the end, the instructor gave us positive feedback, and I am very happy with the overall experience. 



