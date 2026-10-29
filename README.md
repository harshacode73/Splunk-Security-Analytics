# Splunk Dashboard — SOC Security Monitoring

A Splunk-based SOC dashboard for security event monitoring, SSH brute-force detection, severity classification, and security event investigation.

## 1. Project Overview

The **SOC Security Monitoring Dashboard** is a cybersecurity project built using Splunk Enterprise to support security monitoring and investigation. It enables analysts to search collected security logs, identify suspicious authentication activity, classify events using configurable detection rules, and investigate potential threats.

The project focuses on Windows OpenSSH authentication logs and can be extended to include Kali Linux authentication logs and additional Windows security event sources.

## 2. Project Objectives

- Monitor security events collected in Splunk.
- Analyze failed and successful SSH authentication attempts.
- Identify repeated authentication failures that may indicate brute-force activity.
- Classify events according to configurable severity rules.
- Investigate PowerShell and Windows Remote Management activity when the relevant logs are available.
- Identify potential Windows audit-log-clearing activity.
- Map selected detection patterns to MITRE ATT&CK techniques.
- Present relevant security information through a centralized dashboard.

## 3. Tools and Technologies

| Technology | Purpose |
|---|---|
| Splunk Enterprise | Log indexing, searching, and visualization |
| Search Processing Language (SPL) | Security-event analysis and detection rules |
| Windows | Monitoring platform and Windows event sources |
| OpenSSH | SSH authentication event analysis |
| Kali Linux | Authorized lab testing and Linux log collection |
| Universal Forwarder | Forwarding supported logs to Splunk |
| XML | Dashboard configuration |
| MITRE ATT&CK | Mapping potential adversary techniques |

## 4. Key Features

### Security Event Monitoring
Search and review security events collected in the configured Splunk index.

### SSH Authentication Analysis
Examine failed logins, invalid usernames, and successful authentication events.

### Potential Brute-Force Detection
Identify repeated authentication failures using configurable thresholds and time windows. These detections indicate suspicious patterns and require further investigation.

### Severity Classification
Group matching events into Critical, High, Medium, Low, or Unclassified categories using project-defined rules.

### PowerShell Investigation
Search for configured PowerShell-related indicators when the required Windows event sources are being collected.

### Windows Remote Management (WinRM)
Investigate matching WinRM-related events when the relevant Windows logs are available.

### Audit-Log Clearing Detection
Search for Windows events associated with possible security-log clearing, including Security Event ID 1102 when the corresponding audit logs are collected.

### MITRE ATT&CK Mapping
Associate selected event patterns with relevant ATT&CK techniques to support investigation and documentation.

### Recent Events and Host Overview
Review recent security events and compare indexed event volumes across hosts.

## 5. Severity Classification

Severity is assigned using configurable detection rules rather than being treated as an inherent property of every raw log event.

| Severity | Example condition |
|---|---|
| Critical | An event or correlated sequence meeting a configured critical-risk rule |
| High | Repeated authentication failures or another validated high-risk pattern |
| Medium | Multiple failed logins or suspicious activity requiring investigation |
| Low | Lower-risk activity, such as a successful login without additional suspicious indicators |
| Unclassified | Events that do not match the configured classification rules |

**Note:** These are example classification criteria. Actual severity depends on the implemented SPL, event context, thresholds, and investigation findings. A successful login is not automatically safe, and a keyword match alone does not prove an attack.

## 6. MITRE ATT&CK Mapping

The project uses selected MITRE ATT&CK techniques to document activity that may be consistent with known adversary behavior.

| Activity | Technique | ID |
|---|---|---|
| Brute-force attempts | Brute Force | [T1110](https://attack.mitre.org/techniques/T1110/) |
| Windows Remote Management | Remote Services: Windows Remote Management | [T1021.006](https://attack.mitre.org/techniques/T1021/006/) |
| PowerShell execution | Command and Scripting Interpreter: PowerShell | [T1059.001](https://attack.mitre.org/techniques/T1059/001/) |
| Windows event-log clearing | Indicator Removal: Clear Windows Event Logs | [T1070.001](https://attack.mitre.org/techniques/T1070/001/) |

These mappings provide investigative context. They do not independently confirm that an adversary used a technique or that a security incident occurred.

## 7. Lab Environment

The project uses Splunk Enterprise on a Windows monitoring machine. Security events are stored in the `harsha` index.

The environment is designed to support:

- Windows OpenSSH operational logs.
- Kali Linux authentication logs through the Universal Forwarder.
- Additional Windows security and operational logs, where configured.

Log availability depends on the installed components, enabled inputs, permissions, forwarding configuration, and event-source settings.

## 8. Setup and Configuration

1. Install Splunk Enterprise on the monitoring machine.
2. Create or select the index used for lab security events.
3. Configure supported Windows and Linux log sources.
4. Configure receiving and forwarding settings if using a Universal Forwarder.
5. Verify connectivity and confirm that events are indexed.
6. Open Splunk Search and Reporting.
7. Run and validate the SPL searches in the `queries/` directory.
8. Import or recreate the dashboard using the configuration in `dashboards/`.
9. Configure saved alerts separately using the instructions in `docs/alert-configuration.md`.
10. Test the searches, alerts, and dashboard panels using authorized lab events.

See ['docs/setup.md'](docs/setup.md) and [docs/log-collection.md](docs/log-collection.md) for the detailed setup instructions.

## 9. Testing and Validation

Use authorized lab-generated events to validate the implemented detections.

Suggested test cases:

- Failed SSH authentication.
- Successful SSH authentication.
- Invalid SSH usernames.
- Repeated failures from the same source IP.
- PowerShell-related activity, if collected.
- WinRM-related activity, if collected.
- Windows audit-log-clearing events in a dedicated lab, where safely simulated.

For each test, verify that:

1. The relevant event is generated.
2. Splunk receives and indexes the event.
3. The expected SPL search returns the event.
4. The severity classification matches the configured rule.
5. Any associated saved alert triggers under the intended conditions.
6. The corresponding dashboard panel displays the expected result.

Record the actual test results and document any missing data sources or known detection limitations.

## 10. Project Structure

```text
Splunk-dashboard/
├── README.md
├── dashboards/
│   └── soc_security_dashboard.xml
├── queries/
│   ├── ssh_brute_force.spl
│   ├── ssh_successful_login.spl
│   ├── ssh_invalid_user.spl
│   ├── ssh_failures_by_source_ip.spl
│   ├── severity_counts.spl
│   ├── high_severity.spl
│   ├── medium_severity.spl
│   ├── critical_severity.spl
│   ├── powershell_detection.spl
│   ├── winrm_detection.spl
│   ├── audit_log_cleared.spl
│   ├── recent_security_events.spl
│   ├── events_by_host.spl
│   └── mitre_mapping.spl
├── alerts/
│   ├── ssh_brute_force_alert.md
│   ├── windows_security_alert.md
│   └── linux_authentication_alert.md
├── configs/
│   └── inputs.conf.example
├── docs/
│   ├── setup.md
│   ├── log-collection.md
│   ├── log-analysis.md
│   └── alert-configuration.md
└── screenshots/
```

*This is the intended repository structure. Include only files that actually exist in your repository, and update the tree if your filenames differ.*

## 11. Limitations

- Detection quality depends on the logs available to Splunk.
- Windows and Linux events may use different field names and formats.
- Keyword- and regex-based searches can generate false positives and false negatives.
- Brute-force thresholds must be evaluated using the correct time range, source IP, and host.
- A dashboard refresh does not automatically perform incident-response actions.
- Saved alerts require separate configuration and testing.
- MITRE ATT&CK mappings indicate potential relevance, not confirmed attacker behavior.
- Missing event sources can prevent a detection from finding relevant activity.

## 12. Future Improvements

- Configure and validate scheduled alerts and notification actions.
- Improve field extraction, normalization, and event correlation.
- Add username-, host-, and source-IP-based investigation panels.
- Tune thresholds to reduce false positives.
- Expand Windows and Linux security-event coverage.
- Add incident investigation notes and response procedures.
- Automate repeatable tests for detection rules.
- Add sanitized screenshots showing verified search results and dashboard panels.

## 13. Disclaimer

This project is intended for cybersecurity education, defensive monitoring, and authorized lab testing. Perform security testing only on systems and networks for which you have explicit permission.

---

**Project:** Splunk-Security-Analystics
**Focus:** Security monitoring, authentication analysis, detection engineering, and investigation
