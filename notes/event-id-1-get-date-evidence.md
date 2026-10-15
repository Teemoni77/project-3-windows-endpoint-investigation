# Sysmon Event ID 1 — PowerShell Get-Date

## Evidence Source

Saved Wazuh Discover export from the project investigation. The relevant Sysmon Event ID 1 fields are reproduced below for review. It documents the earlier process-creation test before the separate TCP port 8080 network test.

## Event Summary

- **Endpoint:** `MSEDGEWIN10`
- **Wazuh agent ID:** `004`
- **Endpoint IP:** `192.168.200.103`
- **Provider / channel:** `Microsoft-Windows-Sysmon` / `Microsoft-Windows-Sysmon/Operational`
- **Sysmon Event ID:** `1` — Process Create
- **Sysmon event record ID:** `20912`
- **Process ID:** `4760`
- **Command line:** `"C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe" -NoProfile -Command Get-Date`
- **Image:** `C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe`
- **User:** `MSEDGEWIN10\\IEUser`
- **Parent process ID:** `3988`
- **Sysmon UtcTime:** `2026-10-11 23:14:50.954`
- **Wazuh alert timestamp:** `Oct 12, 2026 @ 00:14:52.098`
- **Wazuh index:** `wazuh-alerts-4.x-2026.10.11`
- **Wazuh rule:** `92027` — “Powershell process spawned powershell instance” (level 4)

## Relevant Sysmon Record

```text
UtcTime: 2026-10-11 23:14:50.954
ProcessGuid: {43199d79-186a-6acc-bc04-000000001900}
ProcessId: 4760
Image: C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe
CommandLine: "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe" -NoProfile -Command Get-Date
CurrentDirectory: C:\\Windows\\system32\\
User: MSEDGEWIN10\\IEUser
ParentProcessGuid: {43199d79-203e-6aca-fd01-000000001900}
ParentProcessId: 3988
ParentImage: C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe
ParentUser: MSEDGEWIN10\\IEUser
```

## Interpretation

This record directly supports that Sysmon recorded the PowerShell `Get-Date` process creation and that Wazuh produced alert rule `92027` for the event. The command was used to inspect the Windows date/time as part of investigating timestamp handling.

The Sysmon `UtcTime` and Wazuh alert timestamp are both preserved as exported. They should not be silently treated as identical clocks or used to infer more than the evidence supports.

This is a separate process-creation event from the later Sysmon Event ID 3 TCP port 8080 test. It does not establish that the `Get-Date` process caused the network connection.

## Original Evidence

The relevant fields are transcribed from a saved Wazuh Discover export captured during the investigation. They document the original event details for review.
