# Blue Team Report&#x20;

## 1. Executive Summary

The HawkEye Lab investigation focused on analyzing network traffic using Wireshark to identify a phishing-related malware infection and investigate potential credential theft and data exfiltration.

The analysis revealed a suspicious domain, an executable downloaded over HTTP, and SMTP messages containing collected password logs associated with HawkEye Reborn v9. These findings indicate potential exposure of sensitive information.

**Incident Severity:** High

## 2. Incident Details

| Field               | Details                 |
| ------------------- | ----------------------- |
| Affected Host       | BEIJING-5CD1-PC         |
| Operating System    | Windows NT 6.1          |
| Internal IP Address | `10.4.10.132`           |
| DNS Server          | `10.4.10.4`             |
| Suspicious Domain   | `proforma-invoices.com` |
| External IP Address | `217.182.138.150`       |
| Downloaded File     | `tkraw_Protected99.exe` |
| Analysis Tool       | Wireshark               |
| Malware Identified  | HawkEye Reborn v9       |

## 3. Detection and Initial Findings

The investigation identified the following suspicious activities in the captured network traffic:

- **Suspicious DNS activity:** The victim queried `proforma-invoices.com`, which resolved to `217.182.138.150`.
- **Malware delivery:** The victim requested `tkraw_Protected99.exe` from the external server over HTTP.
- **Successful download response:** The server returned HTTP `200 OK` for the executable.
- **Credential exposure in SMTP messages:** SMTP messages contained password logs and browser and email account information.
- **Data exfiltration:** Two captured SMTP messages indicated repeated transmission of collected information.

These findings are consistent with the HawkEye phishing scenario, in which a malicious executable is used to collect sensitive information and transmit it to an external destination.

## 4. Incident Timeline

The timeline is based on the provided Wireshark evidence. Packet timestamps are in UTC, while SMTP timestamps are taken from the email `Date` headers.

| Timestamp (UTC) | Event                                                  |
| --------------- | ------------------------------------------------------ |
| 20:37:53        | DNS query for `proforma-invoices.com`.                 |
| 20:37:54        | DNS response resolved the domain to `217.182.138.150`. |
| 20:37:54        | HTTP request for `tkraw_Protected99.exe`.              |
| 20:37:56        | Server returned HTTP `200 OK` for the executable.      |
| 20:38:08        | First SMTP message containing a password log.          |
| 20:48:18        | Second SMTP message containing a password log.         |

The two SMTP message dates are approximately 10 minutes and 10 seconds apart, indicating repeated reporting of collected information.

## 5. Technical Investigation and Analysis

### 5.1 Attack Classification

The HawkEye Lab represents a **phishing-initiated malware attack** involving HawkEye Keylogger – Reborn v9, an information-stealing malware variant. Its observed behavior is consistent with credential harvesting and SMTP-based data exfiltration.

### 5.2 Phishing and Malware Delivery

The lab scenario describes an invoice-themed phishing lure containing a download link. The captured traffic shows the victim requesting `tkraw_Protected99.exe` from `217.182.138.150` over HTTP. The server returned `200 OK`, confirming a successful response to the file request.

### 5.3 Credential Theft and Data Exfiltration

The captured SMTP messages contained password logs identified with HawkEye Reborn v9, including browser and email account information. This indicates that sensitive information was transmitted through email.

Two captured message `Date` headers were approximately 10 minutes and 10 seconds apart. This is consistent with repeated exfiltration activity; however, the two messages alone do not establish a regular transmission schedule.

**Attack Flow:**
Phishing lure → Executable download → Credential collection → SMTP-based data exfiltration

## 6. Indicators of Compromise (IOCs)

| Indicator Type         | Value                            |
| ---------------------- | -------------------------------- |
| Suspicious Domain      | `proforma-invoices.com`          |
| External IP Address    | `217.182.138.150`                |
| Executable             | `tkraw_Protected99.exe`          |
| MD5 Hash               | 71826ba081e303866ce2a2534491a2f7 |
| Victim IP Address      | `10.4.10.132`                    |
| SMTP Server Software   | Exim 4.91                        |
| Malware Identification | HawkEye Reborn v9                |

## **7. Impact Assessment**

The captured network traffic indicates that sensitive browser and email account information was included in SMTP messages associated with HawkEye Reborn v9.

- **Potential data exposure:** Account credentials and related information may have been compromised.
- **Affected endpoint:** `BEIJING-5CD1-PC` (`10.4.10.132`).
- **Potential risk:** Unauthorized account access and further compromise if exposed credentials remain valid.
- **Investigation limitation:** The PCAP does not establish the full extent of endpoint compromise or whether the credentials were successfully misused.



## 8. Containment, Eradication, and Recovery Recommendations

The following actions are recommended for a real-world incident:

1. **Isolate the affected endpoint** to prevent further suspicious communication.
2. **Preserve forensic evidence**, including the PCAP, executable, and relevant system and email logs.
3. **Block verified malicious indicators** using firewall, DNS, and web-filtering controls.
4. **Reset exposed credentials** and revoke affected sessions where appropriate.
5. **Investigate the endpoint** for malware execution, persistence, and additional compromise.
6. **Review network and email logs** to identify other affected systems and potential data exposure.

## 9. Security Recommendations

- Strengthen email filtering and scan attachments before delivery.
- Educate users to verify unexpected invoice attachments and suspicious senders.
- Deploy EDR to detect malicious executable activity and suspicious processes.
- Monitor unusual DNS queries and outbound HTTP/SMTP connections.
- Use multifactor authentication to reduce the risk from stolen credentials.
- Integrate endpoint, DNS, firewall, and email logs into a SIEM for correlated detection.

## 10. Conclusion

The HawkEye Lab investigation identified network activity consistent with a phishing-related malware incident involving HawkEye Reborn v9. The key findings included a suspicious domain resolution, an executable download over HTTP, and SMTP messages containing sensitive account information.

The investigation demonstrates how Blue Team analysts use Wireshark to identify indicators of compromise, reconstruct suspicious activity, assess potential credential exposure, and recommend containment and monitoring improvements.
