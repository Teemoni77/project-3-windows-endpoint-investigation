# Project Evidence Screenshots

This folder contains evidence supporting the Windows Endpoint Detection and Investigation project.

## Evidence Index

- `02-wazuh-endpoint-connected.png` — Wazuh agent registration and endpoint status.
- `03-sysmon-baseline-recent.png` — Recent Sysmon process-creation and DNS-query telemetry; this is the baseline image embedded in the main README.
- `03-Sysmon-Baseline-Process-Creation.png` — Earlier baseline screenshot retained as historical supporting evidence.
- `04-sysmon-network-event-record.png` — Formatted evidence derived from an archived Sysmon Event ID 3 record.

## Evidence Interpretation

The evidence demonstrates endpoint connectivity, Sysmon telemetry generation, and the presence of a controlled network-connection event in Wazuh archives.

The archived network event confirms telemetry ingestion and indexing; it does not prove that the intended custom Wazuh alert was generated.

Evidence is presented to support verified findings and distinguish confirmed results from unresolved detection issues.
