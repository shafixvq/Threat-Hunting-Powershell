# Threat Hunting: Suspicious PowerShell Activity

## Overview
This project demonstrates a basic threat hunting exercise focused on identifying suspicious PowerShell execution that may indicate malicious activity.

## Objective
- Proactively search for abnormal PowerShell usage
- Identify potential attacker techniques
- Improve detection and visibility

## Hypothesis
Adversaries may use PowerShell to execute malicious commands, download payloads, or perform lateral movement without triggering immediate alerts.

## Tools Used
- SIEM (Wazuh)
- Windows Event Logs
- MITRE ATT&CK Framework

## Hunting Process
1. Queried logs for PowerShell process execution
2. Reviewed command-line arguments
3. Checked execution frequency and context
4. Compared activity against baseline behavior

## Findings
- PowerShell execution was observed on the endpoint
- Commands executed were standard administrative commands
- No evidence of obfuscation or malicious behavior was identified

## MITRE ATT&CK Mapping
- T1059.001: Command and Scripting Interpreter – PowerShell

## Conclusion
The observed activity was classified as **Benign**, but the exercise highlights how attackers could leverage PowerShell for malicious purposes.

## Recommendations
- Monitor PowerShell execution frequency
- Alert on encoded or obfuscated commands
- Correlate with network activity

