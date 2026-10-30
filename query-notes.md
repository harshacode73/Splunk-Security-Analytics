# SPL Query Notes

These searches assume events are stored in `index=harsha`. Change the index name if yours differs.

- Choose an appropriate time range in Splunk before running a query.
- SSH searches expect OpenSSH text events such as `Failed password for ... from <IP>`.
- PowerShell, WinRM, and Event ID 1102 searches only return results if those data sources are collected and indexed.
- Severity thresholds are example learning rules, not universal SOC standards.
- The rolling SSH counts use events in the selected time range. Include enough history for the 180-second window.
- Keyword-based classifications can produce false positives; inspect raw events.
- These searches display detections; they do not create notable events, send notifications, or automatically remediate incidents.
