# Red Team Report

## 1. Executive Summary

This report analyzes the HawkEye Keylogger lab using Wireshark and the captured network traffic. The investigation identified a suspicious executable download and SMTP messages containing password-log information associated with HawkEye Reborn v9.

The findings indicate potential credential theft and data exfiltration. However, further endpoint investigation is required to confirm malware execution and establish the complete attack chain.

## 2. Objectives

- Analyze potential initial access and malware delivery.
- Identify evidence of credential theft and information collection.
- Investigate possible email-based data exfiltration.
- Document indicators of compromise (IoCs).
- Evaluate attack opportunities and security weaknesses from a Red Team perspective.

## 3. Lab Environment

| Item             | Details           |
| ---------------- | ----------------- |
| Analysis tool    | Wireshark         |
| Target hostname  | `BEIJING-5CD1-PC` |
| Internal IP      | `10.4.10.132`     |
| Operating system | Windows NT 6.1    |

## 4. Attack Analysis

### 4.1 Initial Access and Payload Delivery

The network capture showed a DNS query for `proforma-invoices.com`, resolving to `217.182.138.150`. The target then requested `tkraw_Protected99.exe` over HTTP, and the server returned `200 OK`.

From a Red Team perspective, a suspicious executable delivered through an invoice-themed lure could provide an initial access opportunity if a user executes it. However, the PCAP confirms the download activity, not execution or the precise delivery method.

### 4.2 Credential Theft

SMTP messages in the capture contained password-log information associated with HawkEye Reborn v9.

This indicates potential exposure of credentials and sensitive account information. Such information could be abused to access affected accounts if the credentials remain valid. Additional endpoint evidence is required to confirm how the information was collected.

### 4.3 Potential Data Exfiltration

Two SMTP messages containing password-log information were identified at separate times. This activity is consistent with potential email-based data exfiltration.

The original SMTP streams should be examined to verify message contents, recipients, timestamps, and whether the transfers were unauthorized.

## 5. Attack Timeline

| Time (UTC) | Observed activity                        |
| ---------- | ---------------------------------------- |
| 20:37:53   | DNS query for `proforma-invoices.com`    |
| 20:37:54   | Domain resolved to `217.182.138.150`     |
| 20:37:54   | HTTP request for `tkraw_Protected99.exe` |
| 20:38:15   | HTTP server returned `200 OK`            |
| 20:38:16   | First recorded password-log email event  |
| 20:48:20   | Second recorded password-log email event |

## 6. Indicators of Compromise (IoCs)

| Indicator          | Value                              |
| ------------------ | ---------------------------------- |
| Domain             | `proforma-invoices.com`            |
| External IP        | `217.182.138.150`                  |
| Executable         | `tkraw_Protected99.exe`            |
| MD5 hash           | `71826ba081e303866ce2a2534491a2f7` |
| Target hostname    | `BEIJING-5CD1-PC`                  |
| Internal IP        | `10.4.10.132`                      |
| SMTP software      | Exim 4.91                          |
| Associated malware | HawkEye Reborn v9                  |

## 7. Red Team Findings

The investigation highlights the following potential attack opportunities:

- **Payload delivery:** A suspicious executable was requested over HTTP.
- **Credential exposure:** Password-log information was present in SMTP messages.
- **Data exfiltration:** Email traffic may have been used to transfer sensitive information.
- **Security control assessment:** The activity provides a basis for testing endpoint protection, credential security, and outbound traffic monitoring.

The available evidence does not independently confirm persistence, privilege escalation, lateral movement, or successful unauthorized account access.

## 8. Recommendations

- Investigate the executable's origin and execution history.
- Validate the malware identification and file hash.
- Examine the SMTP messages and determine whether the transfers were authorized.
- Assess the potential impact of exposed credentials.
- Review endpoint protection, email security, and outbound traffic monitoring controls.

## 9. Conclusion

The HawkEye Lab investigation identified a suspicious executable download and SMTP messages containing password-log information associated with HawkEye Reborn v9. These findings support a potential attack scenario involving malware delivery, credential theft, and email-based data exfiltration.

From a Red Team perspective, the lab demonstrates how an attacker could potentially exploit weaknesses in payload delivery defenses, credential protection, and outbound traffic monitoring. Further endpoint and mail-server evidence is required to confirm execution, causality, and the full extent of compromise.
