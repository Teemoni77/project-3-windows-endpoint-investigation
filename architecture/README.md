# Lab Architecture

This folder contains the architecture diagram for the Windows Endpoint Detection and Investigation project.

## Lab Components

- **pfSense:** Virtual network gateway and firewall.
- **Kali Linux:** Controlled network testing.
- **Windows 10:** Endpoint monitored by Sysmon and the Wazuh agent.
- **Wazuh SIEM:** Centralised security monitoring and archived event investigation.

## Network

The lab uses an isolated virtual network on `192.168.200.0/24`.

| System | IP address |
|---|---|
| pfSense LAN | `192.168.200.1` |
| Kali Linux | `192.168.200.10` |
| Wazuh SIEM | `192.168.200.40` |
| Windows 10 endpoint | `192.168.200.103` |

## Architecture Diagram

[View the lab architecture diagram](01-lab-environment.png)

The diagram shows the virtual lab environment and the relationships between its network and security-monitoring components.
