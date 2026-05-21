# MITRE ATT&CK Mapping

- This file documents the MITRE ATT&CK techniques related to detections and investigations performed in this web attack monitoring project.

---

## ATT&CK Overview

- MITRE ATT&CK is a framework that documents:
  - Adversary tactics
  - Attack techniques
  - Threat behaviors
  - Real-world attack patterns

- It helps SOC analysts:
  - Categorize detections
  - Improve visibility
  - Understand attacker methodology
  - Standardize investigations

---

## Detection Mapping

| Detection Activity | ATT&CK Technique | Technique ID | Tactic |
|---|---|---|---|
| SQL Injection Detection | Exploit Public-Facing Application | T1190 | Initial Access |
| XSS Monitoring | Command and Scripting Interpreter | T1059 | Execution |
| Directory Traversal Monitoring | Exploit Public-Facing Application | T1190 | Initial Access |
| Scanner/User-Agent Detection | Active Scanning | T1595 | Reconnaissance |
| Authentication Monitoring | Brute Force | T1110 | Credential Access |

---

## Technique Details

---

### T1190 — Exploit Public-Facing Application

#### Description

- Attackers exploit vulnerabilities in public-facing web applications to gain unauthorized access or execute malicious activity.

#### Common Web Attacks

- SQL Injection
- Directory Traversal
- Remote Code Execution
- File Inclusion Vulnerabilities

#### Detection Relevance

- Web request monitoring helps identify:
  - Exploit attempts
  - Malicious payloads
  - Suspicious URL activity
  - Unauthorized access attempts

#### Relevant Telemetry

- HTTP request logs
- Web server logs
- URL query strings
- HTTP error codes

---

### T1059 — Command and Scripting Interpreter

#### Description

- Attackers abuse scripting capabilities to execute malicious commands or payloads.

#### Detection Relevance

- XSS payloads and malicious scripts may indicate:
  - Client-side exploitation
  - Browser-based attacks
  - Malicious script execution

#### Relevant Indicators

- `<script>`
- `javascript:`
- `onerror=`
- Suspicious script payloads

---

### T1595 — Active Scanning

#### Description

- Attackers perform reconnaissance and scanning to identify:
  - Vulnerabilities
  - Exposed endpoints
  - Misconfigurations
  - Accessible services

#### Detection Relevance

- Monitoring suspicious User-Agents helps identify:
  - Automated scanners
  - Enumeration activity
  - Reconnaissance behavior

#### Common Indicators

- sqlmap
- nikto
- nmap
- curl
- python-requests

---

### T1110 — Brute Force

#### Description

- Attackers attempt repeated authentication attempts to gain unauthorized access.

#### Detection Relevance

- Authentication monitoring helps identify:
  - Login abuse
  - Credential attacks
  - Repeated authentication attempts
  - Password spraying behavior

#### Relevant Telemetry

- Login requests
- Authentication endpoints
- Failed authentication patterns
- HTTP authentication activity

---

## SOC Analyst Value

- MITRE ATT&CK mapping helps analysts:
  - Understand attacker behavior
  - Improve detection quality
  - Standardize investigations
  - Build stronger detections
  - Prioritize suspicious activity

---

## Key Lessons Learned

- Web telemetry provides critical attack visibility
- Threat hunting improves web attack detection
- ATT&CK mapping improves analytical context
- Detection engineering combines technical and contextual analysis
- Reconnaissance activity often precedes exploitation
- Authentication monitoring is essential for web security

---

## Project Context

- This ATT&CK mapping was created as part of a beginner SOC detection engineering project using:
  - Splunk
  - Web server logs
  - HTTP telemetry
  - Sigma rules
  - Threat hunting workflows
  - MITRE ATT&CK mapping
