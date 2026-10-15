# Investigation Timeline

## Purpose

This timeline records the confirmed stages of the controlled Windows endpoint network investigation. It distinguishes the time of the archived Wazuh record from the embedded Sysmon event time because those timestamps differ in the available evidence.

## Timeline

| Stage | Evidence | What it supports | What it does not establish |
|---|---|---|---|
| Endpoint telemetry | Sysmon baseline output includes Event ID 1 (process creation) and Event ID 22 (DNS query). | Sysmon was generating endpoint telemetry during the observed baseline period. | The events alone do not indicate malicious activity. |
| Controlled connectivity test | Kali (`192.168.200.10`) successfully connected to the Windows endpoint (`192.168.200.103`) on TCP port `8080`. | The controlled TCP connectivity test succeeded. | It does not demonstrate an attack or compromise. |
| Archived network event | Sysmon Event ID 3 was found in Wazuh archives. The record identifies PowerShell, source `192.168.200.10:57468`, destination `192.168.200.103:8080`, PID `7276`, and `Initiated: false`. | The network event was received and indexed, and its recorded fields can be examined. | It does not prove that the custom Wazuh rule generated an alert. |
| Timestamp interpretation | For the cited archived record, the Wazuh archive timestamp is `2026-10-12 10:48:38.355`; the embedded Sysmon `UtcTime` is `2026-10-10 07:53:37.870`. The record's `eventRecordID` is `21310`. | Both timestamps are preserved for transparent analysis. | Their difference is not explained by the available evidence; do not treat them as a single reconciled event time. |
| Custom detection | Rule `100100` passed the available syntax validation, but the expected live alert was not observed. | Configuration syntax was validated and a detection gap was identified. | Syntax validation does not establish successful matching or alert generation. |

## Assessment

The available evidence supports endpoint telemetry generation, a successful controlled TCP connection, and the presence of the corresponding Sysmon network event in Wazuh archives. It does not demonstrate successful live alert generation by custom rule `100100`. The cause of the detection gap remains unresolved.

## Evidence References

- [Main project README and evidence gallery](../README.md)
- [Wazuh custom-rule troubleshooting notes](wazuh-rule-troubleshooting.md)
- [Archived Sysmon network-event evidence image](../screenshots/04-sysmon-network-event-record.png)

## Scope Note

This timeline is based on the evidence currently documented in the repository. It does not infer a definitive chronological sequence from the differing Wazuh archive timestamp and embedded Sysmon `UtcTime`.