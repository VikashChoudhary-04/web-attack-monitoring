# Web Attack Detection Queries (Splunk SPL)

- This file contains Splunk SPL queries used for web attack monitoring, suspicious HTTP activity detection, and threat hunting.

---

## 1. SQL Injection Detection

```spl
index=main ("UNION SELECT" OR "' OR 1=1" OR "SELECT * FROM" OR "DROP TABLE")
````

### Purpose

- Detect potential SQL Injection attempts in web requests.

### Detection Goal

- Identify:

  * SQL Injection payloads
  * Database manipulation attempts
  * Suspicious query strings

---

## 2. Cross-Site Scripting (XSS) Detection

```spl id="0f2w8p"
index=main ("<script>" OR "javascript:" OR "onerror=" OR "alert(")
```

### Purpose

- Detect potential XSS payloads in HTTP requests.

### Detection Goal

- Identify:

  * Script injection attempts
  * Malicious client-side payloads
  * Browser exploitation attempts

---

## 3. Directory Traversal Detection

```spl id="7u1m4q"
index=main ("../" OR "..\\" OR "/etc/passwd")
```

### Purpose

- Detect directory traversal attempts.

### Detection Goal

- Identify:

  * Unauthorized file access attempts
  * Sensitive file enumeration
  * Path traversal activity

---

## 4. Suspicious User-Agent Hunting

```spl id="m4z7yq"
index=main ("sqlmap" OR "nikto" OR "nmap" OR "curl" OR "python-requests")
```

### Purpose

- Identify suspicious User-Agent strings associated with scanners and offensive tools.

### Detection Goal

- Detect:

  * Automated scanning tools
  * Reconnaissance activity
  * Security testing behavior

---

## 5. HTTP Error Spike Detection

```spl id="v2n5rx"
index=main ("404" OR "403" OR "500")
| timechart count
```

### Purpose

- Visualize spikes in HTTP errors.

### Detection Goal

- Identify:

  * Scanning behavior
  * Enumeration attempts
  * Broken application activity
  * Web attack anomalies

---

## 6. Excessive Request Monitoring

```spl id="f8s1km"
index=main
| stats count by host
| sort - count
```

### Purpose

- Monitor systems generating excessive web activity.

### Detection Goal

- Identify:

  * High request volumes
  * Potential brute force activity
  * Automated attack behavior

---

## 7. Suspicious Authentication Monitoring

```spl id="j5v4pt"
index=main ("login" OR "signin" OR "auth")
```

### Purpose

- Monitor suspicious authentication-related HTTP activity.

### Detection Goal

- Identify:

  * Login abuse
  * Authentication targeting
  * Brute force against web applications

---

## MITRE ATT&CK Mapping

| Detection                 | ATT&CK Technique                          |
| ------------------------- | ----------------------------------------- |
| SQL Injection Detection   | T1190 - Exploit Public-Facing Application |
| XSS Detection             | T1059 - Command and Scripting Interpreter |
| Directory Traversal       | T1190 - Exploit Public-Facing Application |
| User-Agent Hunting        | T1595 - Active Scanning                   |
| Authentication Monitoring | T1110 - Brute Force                       |

---

## Detection Engineering Concepts

- This project demonstrates:

  * Web attack monitoring
  * HTTP telemetry analysis
  * Threat hunting workflows
  * Attack pattern detection
  * Reconnaissance monitoring
  * Detection engineering fundamentals

---

## Notes

- These queries were developed as part of a beginner SOC detection engineering learning project using:

  * Splunk
  * Web server logs
  * HTTP telemetry
  * Sigma rules
  * MITRE ATT&CK mapping
