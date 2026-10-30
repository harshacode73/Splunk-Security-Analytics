# SOC Security Monitoring Dashboard

## Project Overview
This project uses Splunk to monitor security events and help identify suspicious activity. It includes a dashboard for visualizing security events, detecting SSH login failures, classifying alerts by severity, and mapping detections to MITRE ATT&CK techniques.

## Objectives
- Monitor security events using Splunk.
- Detect repeated SSH login failures.
- Identify suspicious login activity.
- Classify events by severity.
- Map detections to MITRE ATT&CK techniques.
- Display security information in a SOC dashboard.

## Tools and Technologies
- Splunk Enterprise
- Windows
- Windows OpenSSH logs
- Search Processing Language (SPL)
- MITRE ATT&CK

## Dashboard Features
- Security event monitoring
- SSH failed-login monitoring
- Brute-force detection
- Severity classification
- Recent event monitoring
- MITRE ATT&CK mapping

## Project Structure
- dashboards/ — Splunk dashboard XML
- queries/ — SPL detection queries
- docs/ — Setup and testing documentation
- screenshots/ — Dashboard screenshots

## Setup
1. Install Splunk Enterprise.
2. Configure the required event-log input.
3. Send the logs to the `harsha` index.
4. Open Splunk Search & Reporting.
5. Run the SPL queries in the `queries/` directory.
6. Import or configure the dashboard XML in Splunk.

## Limitations
Detection accuracy depends on the available logs and the SPL rules. Severity labels displayed on the dashboard are based on the configured detection logic; they do not automatically perform incident response actions.

## Disclaimer
This project is intended for cybersecurity learning, defensive monitoring, and authorized lab testing.