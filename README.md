# soc-security-monitoring-dashboard
A Splunk-based SOC dashboard for security event monitoring, SSH brute-force detection, and severity classification.
 # SOC Security Monitoring Dashboard Using Splunk

## 1. Project Overview

The SOC Security Monitoring Dashboard is a cybersecurity monitoring project developed using Splunk Enterprise. It helps security analysts review security events, identify suspicious authentication activity, classify potential threats by severity, and investigate events using MITRE ATT&CK technique mappings.

The dashboard brings multiple security-event categories into one place, making it easier to monitor events and investigate potentially malicious activity.

## 2. Objectives

- Monitor security events collected in Splunk.
- Identify suspicious SSH authentication activity.
- Detect patterns associated with brute-force attempts.
- Classify events according to severity.
- Investigate PowerShell-related activity.
- Identify Windows Remote Management activity.
- Detect possible Windows audit-log clearing.
- Map detected activity to relevant MITRE ATT&CK techniques.
- Present security information through a dashboard.

## 3. Tools and Technologies

- Splunk Enterprise
- Search Processing Language (SPL)
- Windows
- OpenSSH
- Kali Linux for authorized lab testing
- XML for dashboard configuration
- MITRE ATT&CK framework

## 4. Dashboard Features

### Critical Alerts
Displays events classified as critical by the configured detection rules.

### High Alerts
Displays events that meet the configured high-severity conditions.

### Medium Alerts
Displays suspicious activity that meets the configured medium-severity conditions.

### Low Alerts
Displays events classified as low severity by the configured rules.

### Brute-Force Investigation
Displays authentication events associated with potential brute-force activity.

### MITRE ATT&CK Mapping
Associates selected event patterns with relevant ATT&CK techniques.

### PowerShell Investigation
Displays events matching configured PowerShell-related indicators.

### WinRM Investigation
Displays events associated with Windows Remote Management.

### Audit-Log Clearing
Displays events matching configured indicators of Windows audit-log clearing.

### Recent Security Events
Provides a consolidated view of recent events.

### Events by Host
Visualizes the number of indexed events associated with each host.

## 5. Severity Classification

The dashboard uses configurable rules to classify events.

| Severity | Example detection condition |
|---|---|
| Critical | Audit-log clearing or a suspicious authentication sequence meeting the configured critical rule |
| High | Repeated failed authentication attempts or configured high-risk command indicators |
| Medium | Multiple failed authentication attempts or configured suspicious PowerShell indicators |
| Low | Successful authentication without a matching higher-severity condition |
| Unclassified | Events that do not match the configured detection rules |

These classifications are rule-based and should be validated against the actual event data. A matching keyword alone does not prove that an attack occurred.

## 6. MITRE ATT&CK Mapping

The project includes mappings for selected activity categories.

| Activity | Technique | Technique ID |
|---|---|---|
| Brute-force activity | Brute Force | T1110 |
| Windows Remote Management | Remote Services: Windows Remote Management | T1021.006 |
| PowerShell activity | Command and Scripting Interpreter: PowerShell | T1059.001 |
| Clearing Windows event logs | Indicator Removal: Clear Windows Event Logs | T1070.001 |

The mappings indicate potential techniques associated with matching event patterns. They do not establish that a technique was successfully executed.

## 7. Environment

The lab uses Splunk Enterprise to search security events indexed under the `harsha` index.

The environment can be extended to collect authorized Windows security logs, OpenSSH operational logs, and other supported event sources.

Actual event collection depends on the configured Splunk inputs and available data sources.

## 8. Installation and Setup

1. Install Splunk Enterprise on the monitoring machine.
2. Configure an index for the lab security events.
3. Configure supported event sources to send logs to Splunk.
4. Verify that events appear in the intended index.
5. Open Splunk Search and Reporting.
6. Test the SPL queries in the `queries` directory.
7. Import or recreate the dashboard using the XML in `dashboards`.
8. Verify that the dashboard panels return expected results.
9. Test the detection rules using authorized lab events.

Refer to `docs/setup.md` for detailed configuration instructions.

## 9. Testing

Test the project using authorized lab-generated events, including:

- Failed SSH authentication attempts.
- Successful SSH authentication.
- Repeated failed authentication attempts from the same source.
- PowerShell-related events.
- Windows Remote Management events.
- Audit-log-clearing events, when safely simulated in a dedicated lab.

Confirm that each event is indexed and that the corresponding search returns the expected result.

Do not test against systems without permission.

## 10. Limitations

- Detection depends on the logs collected and indexed by Splunk.
- Event formats differ between Windows and Linux.
- Regex-based detection can produce false positives and false negatives.
- Severity thresholds must be validated against event timestamps and source identities.
- Dashboard refresh does not automatically execute response actions.
- Saved alerts must be configured separately for notifications or other alert actions.
- MITRE ATT&CK mappings describe potential techniques and require investigation.

## 11. Future Improvements

- Add validated scheduled alerts and notification actions.
- Improve event normalization and field extraction.
- Add source-IP and username-based correlation.
- Reduce duplicate alert notifications.
- Add dashboards for additional Windows security events.
- Integrate endpoint detection and response data.
- Add investigation notes and incident-response documentation.
- Create repeatable tests for each detection rule.

## 12. Disclaimer

This project is intended for cybersecurity education, defensive monitoring, and authorized lab testing. All testing should be performed only on systems and networks for which permission has been granted.
