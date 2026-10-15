# Windows Endpoint Detection & Investigation — Wazuh and Sysmon

## Project Overview

This project documents a hands-on Windows endpoint security monitoring and investigation lab built using Wazuh, Sysmon, and VMware. It demonstrates endpoint telemetry collection, security event analysis, controlled network testing, and investigation using a centralised security monitoring platform.

The project focuses on understanding what endpoint events reveal, how to investigate network activity, and how to distinguish confirmed observations from detection gaps and unresolved issues.

## Objectives

- Deploy and monitor a Windows endpoint using the Wazuh agent.
- Collect and examine Windows Sysmon telemetry.
- Investigate process creation and network connection events.
- Perform controlled network testing within an isolated virtual lab.
- Use Wazuh's indexed event data to investigate endpoint activity.
- Document findings, limitations, and opportunities for improving detection rules.

## Lab Environment

The lab uses VMware virtual machines and an isolated host-only network.

| Component | Role |
|---|---|
| pfSense | Virtual network gateway and firewall |
| Kali Linux | Controlled security testing |
| Windows 10 | Endpoint under investigation |
| Wazuh | Centralised security monitoring and event analysis |
| Sysmon | Detailed Windows system telemetry |

### Network Layout

The lab uses the `192.168.200.0/24` network.

| System | IP address |
|---|---|
| pfSense LAN | `192.168.200.1` |
| Kali Linux | `192.168.200.10` |
| Wazuh SIEM | `192.168.200.40` |
| Windows 10 endpoint | `192.168.200.103` |

## Endpoint Monitoring

The Windows endpoint is registered with Wazuh as agent `004`, named `MSEDGEWIN10`. The agent was observed in the Active state, and both the Wazuh agent and Sysmon services were running.

Sysmon telemetry examined during the project included:

- **Event ID 1:** Process creation.
- **Event ID 3:** Network connection.
- **Event ID 11:** File creation.
- **Event ID 13:** Registry value set.
- **Event ID 22:** DNS query.

These event types provide useful context for investigating endpoint execution and network behaviour. Their presence alone does not establish malicious activity.

## Controlled Network Investigation

A controlled connectivity test was performed between Kali Linux and the Windows endpoint.

A PowerShell TCP listener was configured on the Windows endpoint at TCP port `8080`. Kali Linux then successfully connected to that port.

The corresponding Sysmon Event ID 3 was found in Wazuh's archived event data. The event recorded network activity involving:

- Source IP: `192.168.200.10`
- Destination IP: `192.168.200.103`
- Destination port: `8080`
- Process: Windows PowerShell
- Initiated: `false`

This demonstrates that endpoint network telemetry was collected and could be examined through Wazuh's indexed archive data.
### Evidence: Sysmon Network Connection (Event ID 3)

The archived Sysmon record confirms that Wazuh received and indexed a Windows network-connection event associated with a controlled connectivity test from Kali Linux to the Windows endpoint on TCP port 8080.

- **Source:** `192.168.200.10` (Kali Linux)
- **Destination:** `192.168.200.103:8080` (Windows endpoint)
- **Process:** PowerShell
- **Sysmon Event ID:** `3`
- **Evidence:** [View the archived network-event record](screenshots/04-sysmon-network-event-record.png)

**Detection limitation:** The event was archived and indexed, but the intended custom Wazuh alert was not successfully demonstrated. This remains an unresolved item in the investigation.

The test was controlled lab activity, not evidence of an external compromise.

## Event Analysis and Investigation

The investigation involved examining archived Windows events, identifying relevant Sysmon fields, and correlating the observed network connection with the test performed in the lab.

The project distinguishes between:

1. **Telemetry collection:** Events were received and stored in Wazuh's archive indices.
2. **Event investigation:** Relevant event fields were examined to understand the recorded activity.
3. **Rule-based alerting:** A custom rule was developed and tested, but reliable alert generation for the intended network event remains unresolved.

Archived events are not necessarily security alerts. A successful investigation therefore requires distinguishing event ingestion from rule matching and alert generation.

## Findings

- The Windows endpoint was connected to Wazuh.
- Sysmon produced detailed endpoint telemetry.
- A controlled Kali-to-Windows TCP connection succeeded.
- The corresponding Sysmon network connection event was located in Wazuh's archived data.
- The archived event contained useful source, destination, port, process, and connection-direction information.
- Custom rule troubleshooting identified an outstanding detection-engineering issue that requires further investigation.

## Limitations

This project does not claim that the custom TCP port 8080 detection rule was successfully validated through live alert generation.

The investigation also does not establish that the observed activity was malicious. The connection was generated deliberately for testing.

Further work would include resolving the custom rule's live matching behaviour, validating successful alert generation, and extending the investigation with additional correlated endpoint events where supported by evidence.

## Tools and Technologies

- VMware
- pfSense
- Kali Linux
- Windows 10
- Sysmon
- Wazuh agent, manager, indexer, and dashboard
- OpenSearch Dashboards / Discover for event investigation
- PowerShell
- Netcat (`nc`)

## Security and Scope

All testing was conducted in a controlled virtual lab using systems configured for this project. The work focuses on defensive monitoring, telemetry analysis, and investigation.

## Key Takeaway

Effective endpoint investigation requires more than collecting logs. Analysts must interpret event fields, correlate observations with known activity, validate alerting separately from ingestion, and clearly document limitations.


