# Endpoint Detection Lab: Sysmon + Microsoft Sentinel

## 📌 Executive Summary

This project demonstrates detection of encoded PowerShell attacks using endpoint telemetry collected with Sysmon and analyzed within Microsoft Sentinel. The lab simulates real-world attacker behavior and builds detection logic to identify obfuscated command execution.

## 📄 Full Project Report
For a detailed breakdown of this lab, including full analysis and screenshots:

👉 ## 📄 Full Project Report
For a detailed breakdown of this lab, including full analysis and screenshots:

👉 [Download Full Report](Endpoint-Detection-Lab.pdf)

## 🎯 Objective

* Detect obfuscated PowerShell execution using Base64 encoding
* Ingest endpoint telemetry into a SIEM platform
* Create and validate detection rules for malicious activity

---

## 🏗️ Architecture

* Azure Virtual Machine (Windows)
* Sysmon installed for endpoint logging
* Logs forwarded to Log Analytics Workspace
* Integrated with Microsoft Sentinel for detection and alerting

---

## ⚔️ Attack Simulation

The following command was used to simulate attacker behavior:

```powershell
powershell.exe -enc <base64_payload>
```

### Why this matters:

* Attackers use `-enc` to hide malicious commands
* Enables fileless execution
* Common in real-world attacks and red team activity

---

## 🔍 Detection Logic

```kql
Event
| where Source == "Microsoft-Windows-Sysmon"
| where EventID == 1
| where CommandLine contains "-enc"
```

### Detection Breakdown:

* **EventID 1** → Process creation (Sysmon)
* **CommandLine contains "-enc"** → Indicator of obfuscated execution
* Focuses on identifying suspicious PowerShell usage

---

## 🚨 Alerting

* Converted detection query into a Scheduled Analytics Rule
* Frequency: 5 minutes
* Severity: High
* Triggered on matching PowerShell execution events

---

## 🧪 Validation

* Executed encoded PowerShell payload
* Verified Sysmon log generation
* Confirmed ingestion into Sentinel
* Alert successfully triggered

---

## 🛡️ Defensive Value

* Detects fileless malware techniques
* Identifies common attacker evasion methods
* Provides visibility into endpoint-level activity
* Scalable to enterprise SIEM environments

---

## 📚 Lessons Learned

* Endpoint visibility is critical for threat detection
* Obfuscation is commonly used to bypass defenses
* Detection engineering requires tuning and validation
* SIEM integration enables centralized monitoring

---

## ⚠️ Security Notice

All testing was performed in a controlled lab environment. No production systems or sensitive data were used. Any sensitive values (tokens, credentials) should be redacted in real-world scenarios.
