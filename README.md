# Azure-SOC-Homelab-Honeypot-Sentinel
Built a cloud-based SOC homelab in Microsoft Azure using a Windows honeypot, Log Analytics Workspace, Microsoft Sentinel, KQL, and attack map visualization for security monitoring and threat detection.
# Azure SOC Homelab using Honeypot and Microsoft Sentinel

## Overview

This project demonstrates the deployment of a cloud-based Security Operations Center (SOC) homelab using Microsoft Azure and Microsoft Sentinel.

The objective was to build a Windows honeypot, collect and analyze security logs, monitor failed login attempts, enrich logs with geographic information, and visualize attacker activity using Microsoft Sentinel.

This lab provides hands-on experience with SIEM operations, log analysis, cloud security monitoring, and threat detection.

---

## Project Objectives

* Deploy a Windows virtual machine in Microsoft Azure.
* Configure the VM as a honeypot.
* Collect Windows Security Event Logs.
* Forward logs to Azure Log Analytics Workspace.
* Connect Microsoft Sentinel to the environment.
* Analyze security events using Kusto Query Language (KQL).
* Enrich attacker IP addresses with GeoIP data.
* Visualize attacks on a geographic attack map.

---

## Technologies Used

### Cloud Platform

* Microsoft Azure

### Security Tools

* Microsoft Sentinel
* Azure Log Analytics Workspace

### Operating System

* Windows Server

### Logging & Monitoring

* Windows Event Viewer
* Azure Monitor Agent (AMA)

### Query Language

* Kusto Query Language (KQL)

### Networking

* Azure Virtual Network (VNet)
* Network Security Groups (NSG)

---

## Architecture

```text
Internet
    │
    ▼
Windows Honeypot VM
    │
    ▼
Azure Monitor Agent
    │
    ▼
Log Analytics Workspace
    │
    ▼
Microsoft Sentinel
    │
    ▼
KQL Analysis & Attack Map
```

---

## Project Workflow

### 1. Azure Environment Setup

* Created Azure subscription.
* Created Resource Group.
* Configured Virtual Network (VNet).
* Deployed Windows Server Virtual Machine.

---

### 2. Honeypot Configuration

* Configured a public IP address.
* Allowed inbound RDP traffic.
* Modified Network Security Group rules.
* Disabled Windows Firewall for testing purposes.

The VM was intentionally exposed to attract malicious login attempts and generate security events.

---

### 3. Log Collection

Windows Security Events were collected from the virtual machine and forwarded to Azure Log Analytics Workspace using Azure Monitor Agent.

Key Event IDs monitored:

| Event ID | Description      |
| -------- | ---------------- |
| 4624     | Successful Logon |
| 4625     | Failed Logon     |
| 4634     | Logoff           |
| 4688     | Process Creation |

---

### 4. Microsoft Sentinel Integration

* Created Log Analytics Workspace.
* Connected Microsoft Sentinel.
* Configured Windows Security Events via AMA connector.
* Verified log ingestion.

---

### 5. KQL Log Analysis

Example query used to investigate failed login attempts:

```kql
SecurityEvent
| where EventID == 4625
| order by TimeGenerated desc
```

Example query to count failed logins:

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedAttempts = count() by Account
| order by FailedAttempts desc
```

---

### 6. GeoIP Enrichment

A GeoIP watchlist was imported into Microsoft Sentinel to enrich attacker IP addresses with location data.

This allowed identification of:

* Source Country
* Source City
* Latitude
* Longitude

for incoming attacks.

---

### 7. Attack Map Visualization

A Microsoft Sentinel Workbook was created to display attack activity geographically.

The attack map visualized:

* Source countries
* Source IP addresses
* Failed login attempts
* Global attack distribution

---

## Skills Demonstrated

### Cloud Security

* Azure Administration
* Virtual Networking
* Resource Management

### Security Operations

* SIEM Administration
* Threat Monitoring
* Event Analysis
* Security Alert Investigation

### Log Analysis

* Windows Event Logs
* Kusto Query Language (KQL)

### Incident Detection

* Failed Login Analysis
* Brute Force Detection
* Geographic Threat Analysis

---

## Screenshots

Project Screenshots

1. SOC Architecture
2. Azure Virtual Machine Deployment
3. Azure Resource Group and Resources
4. Windows Event Viewer - Failed Login Events (Event ID 4625)
5. Log Analytics Workspace Security Logs
6. GeoIP Watchlist Import
7. GeoIP Enriched Security Events
8. Microsoft Sentinel Attack Map

---

## Key Learnings

* Understanding Azure cloud infrastructure.
* Deploying and managing virtual machines.
* Collecting and forwarding security logs.
* Using Microsoft Sentinel for security monitoring.
* Writing KQL queries for threat investigation.
* Enriching security data with threat intelligence.
* Visualizing attacker behavior using Sentinel Workbooks.

---

## Future Improvements

* Create custom Sentinel analytics rules.
* Configure automated incident response.
* Integrate threat intelligence feeds.
* Simulate real-world attack scenarios.
* Perform threat hunting using advanced KQL queries.

---

## Author

Vishal Kumar R

