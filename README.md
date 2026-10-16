# Splunk SIEM Home Lab

A hands-on Security Information and Event Management (SIEM) project focused on centralized firewall log collection, network security monitoring, and security event investigation.

## Overview

This project explores how a SIEM solution can be deployed in a virtualized environment to collect and analyze firewall logs.

The lab uses Splunk Enterprise on Windows 10, OPNsense as the firewall, and Kali Linux as a testing machine. VMware virtual networking provides the environment for connectivity and controlled security testing.

The main goal is to understand the log collection pipeline and develop practical skills relevant to Blue Team operations and Security Operations Center (SOC) workflows.

## Objectives

- Deploy Splunk Enterprise on Windows 10.
- Configure OPNsense firewall logging and log forwarding.
- Investigate collected logs using Splunk Search Processing Language (SPL).
- Generate controlled network traffic from Kali Linux.
- Correlate test activities with available firewall logs.
- Document the lab architecture, configuration, and investigation findings.

## Architecture

The lab consists of three primary virtual machines:

- **Windows 10:** Runs Splunk Enterprise for log ingestion and investigation.
- **OPNsense:** Enforces network policies and generates firewall logs.
- **Kali Linux:** Generates controlled traffic for monitoring and testing.

The intended workflow is to forward relevant OPNsense logs to Splunk, search the collected events, and investigate activity generated during lab testing.

The exact network interfaces, IP addressing, routing, and log transport settings will be documented alongside the implementation evidence.


<img width="773" height="533" alt="{2C41A9AA-5ECA-42EA-875E-09C4FB5BBC04}" src="https://github.com/user-attachments/assets/0020dc63-395d-4a97-b98d-fc2eb3330e65" />

## Implementation Plan

### 1. Virtual Network Configuration
- Configure the virtual network adapters.
- Verify connectivity between the required lab components.
- Document the VMnet2 and NAT network configuration.

### 2. OPNsense Configuration
- Review firewall interfaces and network rules.
- Configure the relevant logging settings.
- Set up log forwarding to the Splunk receiver, where applicable.

### 3. Splunk Deployment
- Install Splunk Enterprise on Windows 10.
- Configure the appropriate receiving input.
- Verify connectivity and incoming log data.

### 4. Log Collection and Investigation
- Search for incoming OPNsense events.
- Inspect available fields and event timestamps.
- Develop SPL searches to filter and summarize relevant events.

### 5. Controlled Security Testing
- Generate authorized test traffic from Kali Linux.
- Review corresponding firewall events.
- Record observations and investigate the resulting logs.

## Log Analysis

This section will contain verified SPL queries and investigation examples.

Each investigation will document:

- **Objective:** The behavior or event being investigated.
- **Method:** The test procedure and SPL query.
- **Evidence:** The relevant events observed in Splunk.
- **Analysis:** What the available logs indicate.
- **Limitations:** What cannot be concluded from the collected data.

## Skills Developed

- SIEM deployment and basic administration
- Firewall configuration and logging
- Centralized log collection
- SPL-based event searching
- Virtual network troubleshooting
- Security event investigation
- Technical documentation and evidence collection

## Future Improvements

- Integrate Windows security logs and Sysmon telemetry.
- Build dashboards for firewall activity.
- Develop alerting rules for selected security events.
- Expand log analysis and detection use cases.
- Document investigation workflows relevant to SOC operations.

## Disclaimer

This project is intended for educational purposes and authorized testing within a controlled lab environment. Security testing is performed only against systems and networks for which authorization has been granted.
