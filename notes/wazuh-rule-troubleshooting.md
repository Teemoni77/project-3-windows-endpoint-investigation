# Wazuh Custom Rule Troubleshooting

## Objective

Investigate why the custom Wazuh rule intended to detect a controlled inbound Sysmon network connection to TCP port 8080 did not reliably generate the expected alert.

## Confirmed Results

- The Windows endpoint was connected to Wazuh.
- Sysmon Event ID 3 was found in Wazuh archived event data.
- The archived event recorded a connection from Kali Linux (`192.168.200.10`) to Windows (`192.168.200.103`) on TCP port `8080`.
- The event included process and connection-direction fields relevant to investigation.
- The Wazuh rule configuration passed the available syntax validation check.

## Outstanding Issue

Successful event ingestion and rule syntax validation did not establish that the custom rule matched the live event and generated an alert. Reliable live alert generation remains unverified.

## Next Steps

Further investigation should establish why the rule does not match the live EventChannel event and then validate the complete detection path using a new controlled test.

No successful custom alert is claimed in this project unless supported by evidence.

## Findings and Limitations

### Confirmed Findings

- The Windows endpoint (`MSEDGEWIN10`, agent ID `004`) is connected to the Wazuh manager.
- Sysmon is generating endpoint telemetry, including process creation (Event ID 1), network connections (Event ID 3), and DNS queries (Event ID 22).
- A controlled connectivity test from Kali Linux (`192.168.200.10`) to the Windows endpoint (`192.168.200.103`) on TCP port `8080` succeeded.
- The corresponding Sysmon Event ID 3 record was received and indexed in Wazuh archives.
- The archived record identifies PowerShell as the associated process and records the source and destination network details.

### Outstanding Issue

The intended custom Wazuh rule (`100100`) did not generate the expected alert, despite the network event being present in the archives. The cause remains unresolved.

### Conclusion

This investigation demonstrates endpoint telemetry collection, controlled network testing, and verification of archived Sysmon events in Wazuh. Successful generation of the intended custom alert has **not** been demonstrated and remains a limitation of the project.
