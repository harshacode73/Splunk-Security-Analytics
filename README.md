# Splunk Dashboard — SOC Security Monitoring

A Splunk-based SOC dashboard for security event monitoring, suspicious activity analysis, SSH brute-force detection, severity classification, and security event investigation.

## 1. Project Overview

The **SOC Security Monitoring Dashboard** is a cybersecurity project built using Splunk Enterprise to support security monitoring and investigation.

It enables security analysts to search collected security logs, identify suspicious authentication activity, analyze abnormal login patterns, classify events using configurable detection rules, and investigate potential security threats.

The project focuses on Windows OpenSSH authentication logs and is designed to support Kali Linux authentication logs and additional Windows security event sources.

## 2. Project Objectives

- Monitor security events collected in Splunk.
- Analyze failed and successful SSH authentication attempts.
- Identify repeated authentication failures that may indicate brute-force activity.
- Detect potentially suspicious activities across monitored systems.
- Classify security events according to configurable severity rules.
- Investigate PowerShell and Windows Remote Management activity when relevant logs are available.
- Identify potential Windows audit-log-clearing activity.
- Map selected detection patterns to MITRE ATT&CK techniques.
- Present security information through a centralized dashboard.
- Improve security monitoring and investigation capabilities using SPL queries.

## 3. Tools and Technologies

| Technology | Purpose |
|---|---|
| Splunk Enterprise | Log indexing, searching, monitoring, and visualization |
| Search Processing Language (SPL) | Security event analysis and detection rules |
| Windows | Monitoring platform and Windows event sources |
| OpenSSH | SSH authentication event analysis |
| Kali Linux | Authorized lab testing and Linux log collection |
| Splunk Universal Forwarder | Forwarding supported logs to Splunk |
| XML | Dashboard configuration |
| MITRE ATT&CK | Mapping potential adversary techniques |

## 4. Key Features

### 4.1 Security Event Monitoring

Search and review security events collected from configured Windows and Linux sources in Splunk.

### 4.2 SSH Authentication Analysis

Examine failed logins, invalid usernames, and successful SSH authentication events to identify unusual login patterns.

### 4.3 Potential Brute-Force Detection

Identify repeated authentication failures using configurable thresholds and time windows. These patterns may indicate brute-force attempts and require further investigation.

### 4.4 Severity Classification

Group matching security events into Critical, High, Medium, Low, or Unclassified categories using project-defined detection rules.

### 4.5 PowerShell Investigation

Search for configured PowerShell-related indicators to investigate potentially suspicious command execution when the required Windows event sources are collected.

### 4.6 Windows Remote Management (WinRM)

Investigate WinRM-related events to identify potentially unusual remote access activity.

### 4.7 Audit-Log Clearing Detection

Search for Windows events associated with possible security-log clearing, including Security Event ID 1102 when the corresponding audit logs are collected.

### 4.8 MITRE ATT&CK Mapping

Associate selected event patterns with relevant MITRE ATT&CK techniques to provide additional context during security investigations.

### 4.9 Recent Events and Host Overview

Review recent security events and compare indexed event volumes across monitored hosts.

## 5. Lab Environment

The project uses Splunk Enterprise on a Windows monitoring machine. Security events are stored in the `harsha` index.

The environment is designed to support:

- Windows OpenSSH operational logs.
- Windows Sysmon operational events.
- Kali Linux authentication logs through the Universal Forwarder.
- Additional Windows security and operational logs, where configured.

Log availability depends on installed components, enabled inputs, permissions, forwarding configuration, and event-source settings.

## 6. Suspicious Activity Analysis and Threat Detection

The **Suspicious Activity Analysis** module focuses on identifying, monitoring, and investigating potentially malicious activities across Windows and Kali Linux environments using Splunk Enterprise.

It uses Search Processing Language (SPL) queries and configurable detection rules to analyze authentication logs, identify abnormal login patterns, detect suspicious system activities, and support security investigations.

### 6.1 Detection Use Cases

| Detection Use Case | Analysis Objective |
|---|---|
| SSH Brute-Force Detection | Identify repeated failed SSH authentication attempts that may indicate brute-force activity. |
| Invalid User Detection | Detect authentication attempts involving non-existent usernames. |
| Successful Login Monitoring | Monitor successful authentication events and identify potentially unusual access patterns. |
| Source IP Analysis | Identify source IP addresses associated with repeated authentication failures. |
| PowerShell Activity Monitoring | Investigate potentially suspicious PowerShell command execution. |
| WinRM Activity Monitoring | Monitor Windows Remote Management activity for unusual remote access patterns. |
| Security Log Clearing Detection | Identify Windows Security Event ID 1102, which indicates that the audit log was cleared. |

### 6.2 Severity Classification

Security events are classified according to configurable detection rules, event context, and investigation findings.

| Severity | Description |
|---|---|
| Critical | Events or correlated sequences matching configured critical-risk detection rules. |
| High | Repeated authentication failures or other validated high-risk activity. |
| Medium | Suspicious activity requiring further investigation. |
| Low | Lower-risk events without additional suspicious indicators. |
| Unclassified | Events that do not match the configured classification rules. |

**Note:** Severity levels are assigned through project-defined detection logic. A keyword match or individual event does not independently confirm a security incident.

### 6.3 Dashboard Visualizations

The Suspicious Activity Analysis module is designed to include the following dashboard panels:

1. Suspicious Activity Overview
2. SSH Authentication Failure Trends
3. Top Source IP Addresses
4. Invalid Username Attempts
5. Successful Authentication Events
6. PowerShell Execution Analysis
7. WinRM Remote Access Monitoring
8. Windows Security Log Clearing Events
9. Severity-Based Event Distribution
10. Recent Security Events

### 6.4 Detection and Investigation Workflow

The module follows a structured security monitoring and investigation workflow:

1. **Log Collection:** Collect security events from Windows and Kali Linux systems.
2. **Log Indexing:** Forward and store collected events in the Splunk `harsha` index.
3. **Log Analysis:** Analyze authentication and system activity using SPL queries.
4. **Suspicious Activity Detection:** Identify abnormal patterns using configured detection rules.
5. **Severity Classification:** Categorize matching events as Critical, High, Medium, Low, or Unclassified.
6. **Security Investigation:** Examine event details, timestamps, usernames, source IP addresses, and affected hosts.
7. **Dashboard Reporting:** Present relevant security findings through interactive dashboard panels.

### 6.5 MITRE ATT&CK Mapping

Selected detection use cases are associated with MITRE ATT&CK techniques to provide additional context during security investigations.

| Observed Activity | MITRE ATT&CK Technique | Technique ID |
|---|---|---|
| Brute-Force Attempts | Brute Force | T1110 |
| Windows Remote Management | Remote Services: Windows Remote Management | T1021.006 |
| PowerShell Execution | Command and Scripting Interpreter: PowerShell | T1059.001 |
| Windows Event Log Clearing | Indicator Removal: Clear Windows Event Logs | T1070.001 |

These mappings indicate potential relationships between observed activity and known adversary techniques. They do not independently establish malicious intent.

## 7. Setup and Configuration

1. Install Splunk Enterprise on the Windows monitoring machine.
2. Create or select the index used for lab security events.
3. Configure supported Windows and Linux log sources.
4. Configure receiving and forwarding settings if using a Universal Forwarder.
5. Verify connectivity between the monitored systems and Splunk.
6. Confirm that security events are successfully indexed.
7. Open Splunk Search and Reporting.
8. Run and validate the SPL searches.
9. Import or recreate the dashboard using the dashboard XML configuration.
10. Configure saved alerts separately.
11. Test the searches, alerts, and dashboard panels using authorized lab events.

Detailed setup instructions can be maintained in:

- `docs/setup.md`
- `docs/log-collection.md`
- `docs/log-analysis.md`
- `docs/alert-configuration.md`

## 8. Testing and Validation

Use authorized lab-generated events to validate the implemented detection rules.

### Suggested Test Cases

- Failed SSH authentication.
- Successful SSH authentication.
- Invalid SSH usernames.
- Repeated authentication failures from the same source IP.
- PowerShell-related activity, if collected.
- WinRM-related activity, if collected.
- Windows audit-log-clearing events in a dedicated lab, where safely simulated.

### Validation Process

For each test, verify that:

1. The relevant event is generated.
2. Splunk receives and indexes the event.
3. The expected SPL search returns the event.
4. The extracted fields contain the expected values.
5. The severity classification matches the configured rule.
6. Any associated saved alert triggers under the intended conditions.
7. The corresponding dashboard panel displays the expected result.

Record actual test results and document missing data sources or known detection limitations.

## 9. Detection and Investigation Workflow

The overall project follows this workflow:

```text
Windows / Kali Linux Systems
           |
           v
       Log Collection
           |
           v
      Splunk Indexing
       (harsha index)
           |
           v
       Log Analysis
        (SPL Queries)
           |
           v
 Suspicious Activity Detection
           |
           v
   Severity Classification
           |
           v
 Security Investigation
           |
           v
   SOC Dashboard Reporting
```

## 10. Project Structure

The following is the intended repository structure. Keep only the files that actually exist in the GitHub repository and update filenames when necessary.

```text
Splunk-dashboard/
│
├── README.md
│
├── dashboards/
│   └── soc_security_dashboard.xml
│
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
│
├── alerts/
│   ├── ssh_brute_force_alert.md
│   ├── windows_security_alert.md
│   └── linux_authentication_alert.md
│
├── configs/
│   └── inputs.conf.example
│
├── docs/
│   ├── setup.md
│   ├── log-collection.md
│   ├── log-analysis.md
│   └── alert-configuration.md
│
└── screenshots/
```

## 11. Limitations

- Detection quality depends on the logs available to Splunk.
- Windows and Linux events may use different field names and formats.
- Keyword- and regex-based searches can generate false positives and false negatives.
- Brute-force thresholds must be evaluated using the correct time range, source IP, and host.
- A dashboard refresh does not automatically perform incident-response actions.
- Saved alerts require separate configuration and testing.
- MITRE ATT&CK mappings indicate potential relevance, not confirmed attacker behavior.
- Missing event sources can prevent a detection from finding relevant activity.
- Detection rules must be validated against actual indexed events before being considered operational.

## 12. Future Improvements

- Configure and validate scheduled security alerts and notification actions.
- Improve field extraction, normalization, and event correlation.
- Add username-, host-, and source-IP-based investigation panels.
- Tune detection thresholds to reduce false positives.
- Expand Windows and Linux security-event coverage.
- Add incident investigation notes and response procedures.
- Automate repeatable tests for detection rules.
- Improve dashboard visualizations and investigation capabilities.
- Add sanitized screenshots showing verified search results and dashboard panels.

## 13. Disclaimer

This project is intended for cybersecurity education, defensive monitoring, and authorized lab testing.

Perform security testing only on systems and networks for which you have explicit permission.

---

**Project:** Splunk Dashboard — SOC Security Monitoring

**Focus Areas:** Security Monitoring | Suspicious Activity Analysis | SSH Authentication Analysis | Detection Engineering | MITRE ATT&CK | Security Investigation
