# Blue Team Report

## 1. Executive Summary

This report analyzes the HawkEye Lab network traffic using Wireshark to investigate suspicious executable delivery and potential credential theft.

The investigation identified a suspicious domain, an HTTP executable download, and SMTP messages containing password-log information associated with HawkEye Reborn v9. These findings indicate potential credential exposure and data exfiltration.

**Incident Severity: High (Provisional)** — based on the sensitive information observed in the captured messages. Final severity requires further investigation.

## 2. Incident Details

| Item                 | Details                 |
| -------------------- | ----------------------- |
| Affected hostname    | `BEIJING-5CD1-PC`       |
| Internal IP address  | `10.4.10.132`           |
| Operating system     | Windows NT 6.1          |
| Suspicious domain    | `proforma-invoices.com` |
| External IP address  | `217.182.138.150`       |
| Requested executable | `tkraw_Protected99.exe` |
| Associated malware   | HawkEye Reborn v9       |

## 3. Detection and Initial Findings

Wireshark analysis revealed the following suspicious activities:

- **DNS activity:** `proforma-invoices.com` resolved to `217.182.138.150`.
- **HTTP download:** The target requested `tkraw_Protected99.exe`, and the server returned `200 OK`.
- **SMTP activity:** Two email messages contained password-log information.
- **Potential credential exposure:** The captured messages contained sensitive account information associated with HawkEye Reborn v9.

The evidence warrants further investigation, but the HTTP response alone does not confirm that the executable was executed.

## 4. Incident Timeline

| Time (UTC) | Observed activity                        |
| ---------- | ---------------------------------------- |
| 20:37:53   | DNS query for `proforma-invoices.com`    |
| 20:37:54   | Domain resolved to `217.182.138.150`     |
| 20:37:54   | HTTP request for `tkraw_Protected99.exe` |
| 20:38:15   | HTTP server returned `200 OK`            |
| 20:38:16   | First recorded password-log email event  |
| 20:48:20   | Second recorded password-log email event |

## 5. Technical Investigation

### 5.1 DNS and HTTP Analysis

The suspicious domain resolution and executable download indicate potential malware delivery.

**Blue Team actions:**

- Investigate the domain and destination IP using reliable threat intelligence.
- Review DNS, proxy, and firewall logs.
- Search endpoint telemetry for file creation and process execution.
- Verify the executable's hash against the original sample.

### 5.2 SMTP and Credential Exposure

Two SMTP messages containing password-log information were identified. The lab analysis associated the activity with HawkEye Reborn v9 and identified Exim 4.91 as the observed mail-server software.

**Blue Team actions:**

- Examine SMTP streams, message headers, senders, and recipients.
- Determine whether the information transfer was authorized.
- Review authentication logs for suspicious account activity.
- Reset confirmed exposed credentials and revoke affected sessions where appropriate.

The PCAP does not independently establish how each credential was collected or whether the credentials were subsequently misused.

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

## 7. Impact Assessment

- **Confidentiality:** Sensitive account information was present in the captured email messages.
- **Endpoint security:** The target requested a suspicious executable.
- **Account security:** Exposed credentials could enable unauthorized access if still valid.
- **Data protection:** The SMTP activity requires investigation to determine whether information was transferred without authorization.

The full extent of compromise and any subsequent account misuse remain unconfirmed.

## 8. Incident Response: Containment, Eradication, and Recovery

1. **Containment:** Isolate the affected endpoint if compromise is reasonably suspected and block verified malicious indicators where appropriate.
2. **Evidence preservation:** Secure the original PCAP, executable, endpoint logs, and email records.
3. **Credential protection:** Reset confirmed exposed passwords and revoke affected sessions or tokens.
4. **Investigation:** Examine endpoint processes, file activity, persistence, and authentication records.
5. **Eradication:** Remove confirmed malicious files and related artifacts using approved procedures.
6. **Recovery:** Verify system integrity, apply necessary security updates, and monitor for recurring suspicious activity.

## 9. Security Recommendations

- Strengthen email filtering and executable-download controls.
- Deploy EDR to detect suspicious processes and malware execution.
- Monitor unusual DNS queries and outbound HTTP/SMTP traffic.
- Enforce multifactor authentication to reduce credential-abuse risks.
- Centralize endpoint, DNS, firewall, email, and authentication logs in a SIEM.
- Create and test detection rules that correlate suspicious downloads with subsequent outbound communications.

## 10. Conclusion

The HawkEye Lab investigation identified suspicious HTTP activity and SMTP messages containing password-log information associated with HawkEye Reborn v9.

From a Blue Team perspective, the priority is to validate the evidence, investigate potential credential exposure, contain any confirmed compromise, and improve detection and prevention controls. Additional endpoint and mail-server evidence is required to establish the complete attack chain and determine the full impact.
