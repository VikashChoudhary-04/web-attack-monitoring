# Web Attack Investigation Report

## Investigation Title

- Suspicious Web Activity and Web Attack Monitoring Investigation

---

## Objective

- Investigate web server telemetry to identify suspicious HTTP activity and detect common web attack patterns including SQL Injection, XSS, directory traversal, and reconnaissance behavior.

---

## Environment

| Component | Details |
|---|---|
| SIEM | Splunk Free |
| Log Source | Web Server Logs |
| Investigation Type | Web Attack Monitoring |
| Dataset | HTTP/Web Traffic Logs |

---

## Investigation Workflow

### 1. SQL Injection Detection

#### SPL Query

```spl
index=main ("UNION SELECT" OR "' OR 1=1" OR "SELECT * FROM" OR "DROP TABLE")
````

#### Purpose

- Detect potential SQL Injection attempts targeting web applications.

#### Findings

- HTTP requests were reviewed for suspicious SQL-related payloads and malicious query patterns.

- No confirmed SQL Injection exploitation activity was identified in the baseline dataset.

---

### 2. Cross-Site Scripting (XSS) Detection

#### SPL Query

```spl id="n0w8vm"
index=main ("<script>" OR "javascript:" OR "onerror=" OR "alert(")
```

#### Purpose

- Detect suspicious XSS payloads within HTTP requests.

#### Findings

- Web traffic was analyzed for script injection attempts and malicious client-side payload indicators.

- No confirmed XSS exploitation activity was identified.

---

### 3. Directory Traversal Monitoring

#### SPL Query

```spl id="u7j2qt"
index=main ("../" OR "..\\" OR "/etc/passwd")
```

#### Purpose

- Detect directory traversal attempts targeting sensitive files and directories.

#### Findings

- HTTP requests were reviewed for path traversal indicators and unauthorized file access attempts.

- No confirmed directory traversal activity was identified.

---

### 4. Suspicious User-Agent Hunting

#### SPL Query

```spl id="g2x5rk"
index=main ("sqlmap" OR "nikto" OR "nmap" OR "curl" OR "python-requests")
```

#### Purpose

- Identify suspicious User-Agent strings associated with scanners and offensive security tools.

#### Findings

- Web traffic was reviewed for evidence of automated scanning tools and reconnaissance activity.

- No confirmed malicious scanning activity was identified.

---

### 5. HTTP Error Spike Analysis

#### SPL Query

```spl id="d8m4sp"
index=main ("404" OR "403" OR "500")
| timechart count
```

#### Purpose

- Visualize abnormal spikes in HTTP errors.

#### Findings

- HTTP error activity was reviewed for:

  * Enumeration attempts
  * Reconnaissance activity
  * Broken application behavior
  * Attack anomalies

- No major error spikes or attack-related anomalies were identified.

---

### 6. Authentication Monitoring

#### SPL Query

```spl id="y1t6hn"
index=main ("login" OR "signin" OR "auth")
```

#### Purpose

- Monitor authentication-related web activity for potential brute force or credential abuse attempts.

#### Findings

- Authentication-related traffic was analyzed for repeated login attempts and suspicious behavior.

- No confirmed brute force activity was identified.

---

## MITRE ATT&CK Mapping

| Activity                       | ATT&CK Technique                          |
| ------------------------------ | ----------------------------------------- |
| SQL Injection Monitoring       | T1190 - Exploit Public-Facing Application |
| XSS Monitoring                 | T1059 - Command and Scripting Interpreter |
| Directory Traversal Monitoring | T1190 - Exploit Public-Facing Application |
| Scanner Detection              | T1595 - Active Scanning                   |
| Authentication Monitoring      | T1110 - Brute Force                       |

---

## SOC Analyst Assessment

- The reviewed web telemetry primarily reflected baseline or non-malicious HTTP activity.

- No confirmed exploitation attempts, web application compromise, malicious scanning, or successful attack activity were identified during the investigation.

---

## Key Lessons Learned

* Web logs provide valuable attack telemetry
* HTTP request analysis is critical for SOC operations
* Detection engineering requires contextual analysis
* Threat hunting improves visibility into suspicious behavior
* Reconnaissance activity can often precede exploitation
* False positives must always be evaluated carefully

---

## Future Improvements

- Potential future enhancements include:

  * GeoIP enrichment
  * IP reputation analysis
  * Threat intelligence integration
  * WAF telemetry monitoring
  * Automated alerting
  * User-Agent fingerprinting
  * Web attack dashboards

---

## Analyst Notes

- This investigation was conducted as part of a beginner SOC detection engineering learning project focused on web attack monitoring using Splunk, web server logs, Sigma rules, and MITRE ATT&CK mapping.
