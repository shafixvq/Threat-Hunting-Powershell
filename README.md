# Threat Hunting: Suspicious PowerShell Activity (Wazuh)

## 1. Overview
This project demonstrates a structured threat hunting exercise focused on identifying suspicious PowerShell activity on a Windows endpoint using Wazuh SIEM.

The lab emphasizes **visibility validation, telemetry collection, and hunting methodology**, rather than relying solely on pre-built alerts.

---

## 2. Objective
- Proactively hunt for abnormal PowerShell usage
- Validate endpoint logging and SIEM ingestion
- Identify attacker techniques abusing PowerShell
- Improve detection readiness and SOC visibility

---

## 3. Hypothesis
Adversaries may abuse PowerShell to:
- Execute malicious commands in memory
- Download payloads from remote servers
- Bypass traditional signature-based defenses

If PowerShell logging is correctly enabled, these activities should be observable through Windows event logs and collected by Wazuh.

---

## 4. Tools & Environment
- **SIEM**: Wazuh Dashboard
- **Endpoint**: Windows 10 (Wazuh Agent installed)
- **Log Source**: Windows Event Logs
- **Framework**: MITRE ATT&CK
- **Log Channel**: Microsoft-Windows-PowerShell/Operational

---

## 5. Prerequisite: PowerShell Logging Validation

Before hunting, PowerShell logging was validated to ensure sufficient telemetry.

### Group Policy Configuration
Path:   

Computer Configuration

└── Administrative Templates

└── Windows Components

└── Windows PowerShell

Enabled policies:
- ✅ Turn on PowerShell Script Block Logging
- ✅ Turn on Module Logging
- ✅ Enable Windows Security Event Logging

These settings ensure PowerShell activity generates Event IDs required for threat hunting.

---

## 6. Endpoint Telemetry Verification

PowerShell events were verified locally on the endpoint using **Event Viewer**:

Log Path:

Applications and Services Logs

└── Microsoft

└── Windows

└── PowerShell

└── Operational


Validated Event IDs:
- **4104** – Script Block Logging
- **4103** – Module Logging

This confirmed PowerShell activity was being logged **before SIEM analysis**.

---

## 7. Wazuh Agent Collection Verification

The Wazuh agent configuration (`ossec.conf`) was verified to ensure collection of the PowerShell event channel.

Agent logs confirmed:
- Successful connection to Wazuh Manager
- Event channel analysis enabled
- No ingestion errors observed

This validated that PowerShell logs were successfully forwarded to the SIEM.

---

## 8. Threat Hunting Process

### Step 1: Initial Hunting Query
PowerShell activity was searched using event-based hunting rather than keyword-only filters.

Example queries: data.win.system.eventID:4104


---

### Step 2: Execution Context Review
For each PowerShell event, the following attributes were reviewed:
- Executed command
- Parent process
- User context
- Execution frequency

---

### Step 3: Behavior Analysis
Observed activity was compared against:
- Normal administrative behavior
- Known malicious PowerShell patterns
- MITRE ATT&CK techniques

---

## 9. Simulated PowerShell Activity

Benign PowerShell commands were executed to generate test telemetry:

- whoami
- ipconfig
- Get-Process

These commands successfully generated PowerShell Operational logs for analysis.

## 10. Findings

- PowerShell execution was observed on the endpoint
- Commands executed were standard administrative commands
- No encoded, obfuscated or suspicious scripts were identified
- No lateral movement or payload download behavior detected
- The activity was classified as Benign.

## 11. MITRE ATT&CK Mapping

T1059.001 – Command and Scripting Interpreter: PowerShell

## 12. Challenges Encountered

- PowerShell events were not easily discoverable using default UI filters
- Field normalization required event ID–based hunting
- Visibility depended heavily on proper Group Policy configuration

13. Conclusion

- This threat hunting exercise demonstrated the importance of:
- Proper endpoint logging configuration
- Telemetry validation before hunting
- Structured, hypothesis-driven investigation




