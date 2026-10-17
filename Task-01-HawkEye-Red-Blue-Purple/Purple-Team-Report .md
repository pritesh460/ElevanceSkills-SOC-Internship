# Purple Team Report

## 1. Executive Summary

This report combines Red Team attack analysis and Blue Team defensive investigation of the HawkEye Lab using Wireshark.

The investigation identified a suspicious executable download and SMTP messages containing password-log information associated with HawkEye Reborn v9. These findings indicate potential credential exposure and email-based data exfiltration.

## 2. Objectives

- Combine Red Team and Blue Team findings.
- Identify potential attack techniques and defensive gaps.
- Improve threat detection and incident response.
- Validate security controls through controlled testing.
- Provide a clear handover and recommendations.

## 3. Lab Environment

| Item             | Details                  |
| ---------------- | ------------------------ |
| Lab              | HawkEye — CyberDefenders |
| Target hostname  | `BEIJING-5CD1-PC`        |
| Internal IP      | `10.4.10.132`            |
| Operating system | Windows NT 6.1           |
| Analysis tools   | Wireshark&#x20;          |
| Evidence source  | `stealer.pcap`           |

## 4. Combined Red Team and Blue Team Findings

### 4.1 Suspicious Executable Download

**Red Team finding:** The target requested `tkraw_Protected99.exe` over HTTP from a server associated with `proforma-invoices.com`.

**Blue Team finding:** Wireshark showed DNS resolution, an HTTP request, and a `200 OK` response. Executable execution was not confirmed by the network evidence alone.

**Purple Team actions:**

- Verify the executable's hash and malware classification.
- Correlate the download with endpoint file and process logs.
- Test detection rules for suspicious executable downloads.

### 4.2 Potential Credential Theft

**Red Team finding:** SMTP messages contained password-log information associated with HawkEye Reborn v9.

**Blue Team finding:** The messages indicate potential credential exposure, but the collection method and subsequent account misuse remain unconfirmed.

**Purple Team actions:**

- Investigate potentially affected accounts and authentication logs.
- Reset confirmed exposed credentials and revoke affected sessions where appropriate.
- Correlate endpoint activity with the captured SMTP messages.

### 4.3 Potential Data Exfiltration

**Red Team finding:** Two SMTP messages containing password-log information suggest possible email-based data exfiltration.

**Blue Team finding:** The messages require further investigation to establish their recipients, authorization status, and relationship to the executable download.

**Purple Team actions:**

- Examine SMTP streams, message headers, and mail-server logs.
- Test alerts for unusual outbound SMTP activity.
- Confirm that legitimate email traffic is distinguished from suspicious transfers.

### 4.4 Network Indicators

The capture contains DNS and HTTP activity involving `proforma-invoices.com` and `217.182.138.150`.

**Purple Team actions:**

- Validate the indicators against the original PCAP and reliable threat intelligence.
- Search firewall, DNS, proxy, and endpoint logs for related activity.
- Apply blocking rules after confirming malicious activity and assessing operational impact.

## 5. Incident Timeline

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

## 7. MITRE ATT&CK Mapping

| Technique                              | ID        | Assessment                                                                             |
| -------------------------------------- | --------- | -------------------------------------------------------------------------------------- |
| Phishing                               | T1566     | Delivery method requires verification.                                                 |
| User Execution: Malicious File         | T1204.002 | Execution is not confirmed.                                                            |
| Web Protocols                          | T1071.001 | HTTP was observed; command-and-control use is unconfirmed.                             |
| Credentials from Password Stores       | T1555     | Password logs were found; the collection method is unknown.                            |
| Exfiltration Over Alternative Protocol | T1048     | SMTP was observed; the precise technique and unauthorized transfer require validation. |

## 8. Defensive Improvements

- **Endpoint security:** Improve visibility into suspicious downloads, file creation, and process execution.
- **Network security:** Monitor unusual DNS queries and outbound HTTP/SMTP communications.
- **Credential protection:** Reset confirmed exposed credentials and enforce multifactor authentication where appropriate.
- **SIEM monitoring:** Correlate network, endpoint, email, and authentication events.
- **Email security:** Restrict outbound SMTP traffic to approved mail infrastructure where appropriate.
- **Incident response:** Maintain procedures for evidence preservation, containment, investigation, and recovery.

## 9. Purple Team Validation Plan

1. **Validate evidence:** Confirm the IoCs, timestamps, and observed activity against the original capture.
2. **Develop detections:** Create or improve SIEM and endpoint rules for suspicious downloads and outbound communications.
3. **Simulate safely:** Reproduce representative behaviours in an isolated, authorized lab without executing the suspected malware on production systems.
4. **Test detection:** Verify whether endpoint, network, and SIEM controls generate the expected alerts.
5. **Measure performance:** Record missed detections, false positives, detection time, and response time.
6. **Improve controls:** Tune detection rules and update response procedures.
7. **Retest:** Repeat the simulation to confirm improvements.
8. **Document results:** Record remaining gaps, remediation owners, and follow-up actions.

## 10. Final Handover

**Red Team to Blue Team**

- Provide the suspicious domain, IP, filename, hash, and relevant packet evidence.
- Document the suspected attack path and unconfirmed stages.

**Blue Team to Purple Team**

- Provide relevant network, endpoint, SMTP, and authentication evidence.
- Document alerts generated, detection gaps, and response actions.

**Purple Team follow-up**

- Validate detection rules in an isolated lab.
- Document test results and unresolved security gaps.
- Assign remediation actions and retest the controls after improvements.

## 11. Conclusion

The HawkEye Lab investigation identified a suspicious executable download and SMTP messages containing password-log information associated with HawkEye Reborn v9.

The Red Team findings describe potential attack opportunities, while the Blue Team findings support investigation and defensive response. The Purple Team connects both perspectives by validating evidence, testing detections, and improving security controls.

Further endpoint and mail-server investigation is required to confirm executable execution, establish the relationship between the observed events, and determine the full extent of potential compromise.
