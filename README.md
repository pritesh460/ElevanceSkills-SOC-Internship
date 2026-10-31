<div align="center">

# ElevanceSkills SOC Analyst Internship

### Cybersecurity | Security Operations | Threat Hunting | Incident Response

![Cybersecurity](https://img.shields.io/badge/Domain-Cybersecurity-blue)
![Role](https://img.shields.io/badge/Role-SOC%20Analyst-green)
![SIEM](https://img.shields.io/badge/SIEM-ELK%20%7C%20Wazuh-orange)
![Status](https://img.shields.io/badge/Internship-Project%20Work-success)

**Created by Pritesh Kalsariya**

</div>

---

## About This Repository

This repository contains my practical work, technical investigations, security reports, detection rules, and SIEM dashboard developed during my **SOC Analyst Internship at ElevanceSkills Technology Private Limited**.

The internship focuses on developing practical cybersecurity skills through hands-on activities involving Red Team operations, Blue Team investigations, Purple Team collaboration, SIEM monitoring, threat detection, incident response, and threat intelligence.

All six assigned tasks are organized and documented in this repository.

## Internship Objectives

- Understand Red Team, Blue Team, and Purple Team operations.
- Investigate security incidents using network traffic and system logs.
- Develop custom SIEM correlation and detection rules.
- Simulate and investigate multi-stage Advanced Persistent Threat (APT) attacks.
- Identify Indicators of Compromise (IoCs) and investigate suspicious activities.
- Build custom SIEM dashboards for security monitoring.
- Improve incident response, threat hunting, and security reporting skills.

## Tasks and Projects

### Task 01: Red Team | Blue Team | Purple Team

**Objective:** Analyze the HawkEye lab and prepare three security reports covering offensive, defensive, and collaborative security operations.

**Activities:**
- Red Team: Analyze attack techniques and the attacker's methodology.
- Blue Team: Investigate malicious activities and identify Indicators of Compromise.
- Purple Team: Combine offensive and defensive findings into a security handover report.
- Map relevant attack techniques to the MITRE ATT&CK framework.

**Tools:** Wireshark, CyberChef, MITRE ATT&CK, and network analysis tools.

**Deliverables:**
- Red Team Report
- Blue Team Report
- Purple Team Report

### Task 02: Custom SIEM Correlation Rules Using ELK Stack

**Objective:** Develop and test custom detection rules to identify common attack techniques using the ELK Stack.

**Detection Use Cases:**

1. Brute-Force / Credential Stuffing Detection
2. DNS Tunneling Detection
3. Suspicious PowerShell Execution Detection

**Activities:**
- Set up Elasticsearch and Kibana.
- Configure security log ingestion.
- Create custom detection rules using KQL.
- Configure rule severity, risk scores, and execution intervals.
- Generate test events and validate detection results.
- Review generated security alerts.

**Tools:** Elasticsearch, Kibana, ELK Stack, KQL, Kali Linux.

**Result:** Created and tested three custom SIEM detection rules.

### Task 03: Multi-Stage APT Attack Simulation and Investigation

**Objective:** Simulate a multi-stage Advanced Persistent Threat (APT) attack and investigate it using open-source SOC tools.

**Project Phases:**

**Phase 1 – Attack Simulation (Red Team)**
- Initial access simulation.
- Persistence establishment.
- Privilege escalation.
- Lateral movement.
- Data exfiltration simulation.

**Phase 2 – Detection and Investigation (Blue Team)**
- Monitor suspicious activities and security alerts.
- Investigate IoCs using SIEM queries.
- Analyze malicious files, URLs, and IP addresses.
- Correlate logs and reconstruct the attack timeline.
- Prepare a forensic investigation report.

**Phase 3 – Threat Intelligence and Mitigation**
- Extract and document IoCs.
- Integrate threat intelligence using MISP.
- Develop YARA and Sigma detection rules.
- Identify security gaps and recommend mitigation measures.
- Prepare an incident response report.

**Planned Tools:** Kali Linux, Ubuntu, ELK Stack, Wazuh, Security Onion, TheHive, Cortex, MISP, YARA, and Sigma.

**Deliverables:** Attack simulation documentation, detection evidence, IoC list, detection rules, and incident response report.

### Task 04: HawkEye Lab Investigation – CyberDefenders

**Objective:** Investigate the HawkEye Blue Team CTF challenge by analyzing network traffic and reconstructing a suspected keylogger data-exfiltration incident.

**Activities:**
- Analyze the provided PCAP file.
- Investigate network communication and suspicious connections.
- Identify affected systems and network information.
- Extract suspicious files and analyze their hashes.
- Investigate malware-related indicators.
- Identify command-and-control and exfiltration activities.
- Document findings and investigation steps.

**Tools:** Wireshark, CyberChef, MAC Vendors Lookup, AbuseIPDB, and IP Lookup tools.

**Deliverables:** Detailed HawkEye Lab Investigation Report with findings, IoCs, analysis steps, and supporting evidence.

### Task 05: HTB Brutus Lab Investigation

**Platform:** Hack The Box – Sherlocks

**Objective:** Investigate an SSH brute-force attack by analyzing Linux authentication logs and identifying post-compromise activities.

**Activities:**
- Analyze Linux authentication logs.
- Identify SSH brute-force attempts.
- Determine the compromised user account.
- Investigate suspicious login sessions.
- Reconstruct the attack timeline.
- Identify persistence and privilege escalation activities.
- Document attacker behavior and security findings.

**Tools:** Hack The Box, Linux, Authentication Logs, and Command-Line Utilities.

**Deliverables:** Detailed Brutus Lab Investigation Report with attack timeline, findings, and evidence.

### Task 06: Custom SIEM Security Dashboard Using ELK Stack

**Objective:** Design and implement a custom SIEM dashboard to visualize critical security events and support security monitoring.

**Dashboard Use Cases:**
- Brute-Force Attack Monitoring
- Authentication Failure Analysis
- Suspicious PowerShell Activity
- Privilege Escalation Monitoring
- Network Security Events
- Data Exfiltration Indicators
- Security Alert Monitoring

**Activities:**
- Configure the ELK Stack.
- Ingest and analyze security logs.
- Create visualizations using Kibana.
- Design a custom security monitoring dashboard.
- Organize security events into meaningful visual panels.
- Monitor and investigate suspicious activities.

**Tools:** Elasticsearch, Kibana, ELK Stack, KQL, and Security Logs.

**Deliverables:** Custom SIEM Dashboard with supporting configuration, visualizations, and screenshots.

## Tools and Technologies

| Category | Tools |
|---|---|
| SIEM | Splunk, ELK Stack, Wazuh, Security Onion |
| Network Analysis | Wireshark |
| Security Investigation | CyberChef, Linux Logs |
| Threat Intelligence | MISP, AbuseIPDB |
| Detection Engineering | KQL, Sigma, YARA |
| Incident Response | TheHive, Cortex |
| Operating Systems | Kali Linux, Ubuntu, Windows |
| Security Framework | MITRE ATT&CK |
| Platforms | CyberDefenders, Hack The Box |
| Version Control | Git, GitHub |

## Skills Developed

- Security Information and Event Management (SIEM)
- Security Monitoring and Alert Analysis
- Threat Hunting and Incident Investigation
- Network Traffic Analysis
- Log Analysis and Correlation
- Attack Detection and Mitigation
- Red Team and Blue Team Methodologies
- Threat Intelligence and IoC Analysis
- Detection Engineering
- Incident Response and Documentation

## Repository Structure

```text
ElevanceSkills-SOC-Internship/
│
├── README.md
│
├── Task-01-HawkEye-Red-Blue-Purple/
│   ├── Red-Team-Report/
│   ├── Blue-Team-Report/
│   └── Purple-Team-Report/
│
├── Task-02-ELK-Correlation-Rules/
│   ├── README.md
│   ├── Detection-Rules/
│   ├── Testing/
│   └── Screenshots/
│
├── Task-03-Multi-Stage-APT/
│   ├── README.md
│   ├── Attack-Simulation/
│   ├── Detection-Investigation/
│   ├── Threat-Intelligence/
│   └── Incident-Response-Report/
│
├── Task-04-HawkEye-Lab-Investigation/
│   ├── README.md
│   ├── Investigation-Report/
│   └── Screenshots/
│
├── Task-05-HTB-Brutus/
│   ├── README.md
│   ├── Investigation-Report/
│   └── Screenshots/
│
├── Task-06-SIEM-Dashboard/
│   ├── README.md
│   ├── Dashboard/
│   ├── Configuration/
│   └── Screenshots/
│
└── Internship-Report/
    └── README.md
```

*Note: The structure above is a suggested organization. Keep the folder names consistent with the actual files in your repository.*

## Learning Outcomes

Through these practical assignments, I developed hands-on experience in security monitoring, SIEM detection engineering, network investigation, attack analysis, threat hunting, and incident response.

The projects helped me understand how security teams identify, investigate, respond to, and prevent cyber threats using open-source security tools and frameworks.

## Evidence and Documentation

Each task includes relevant documentation, technical findings, configuration details, investigation steps, and screenshots wherever applicable.

All practical work and project documentation are maintained in this repository for learning, reference, and evaluation purposes.

## Acknowledgement

I would like to thank **ElevanceSkills Technology Private Limited** for providing this opportunity to work on practical cybersecurity assignments and improve my technical knowledge in Security Operations and Incident Response.

## Author

**Pritesh Kalsariya**

SOC Analyst | Cybersecurity Enthusiast

- GitHub: [pritesh460](https://github.com/pr itesh460)
- Internship Repository: [ElevanceSkills SOC Internship](https://github.com/pr itesh460/ElevanceSkills-SOC-Internship)

---

**Disclaimer:** All activities documented in this repository are intended for educational purposes and authorized cybersecurity lab environments only.
