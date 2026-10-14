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
