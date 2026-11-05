# SIEM Detection Lab

## Project Overview

This lab demonstrates centralized security log collection, analysis, and threat detection using Wazuh within an isolated virtual network environment designed to simulate a small-scale Security Operations Center (SOC). It illustrates how security events are collected from endpoints, analyzed by the SIEM, and investigated to identify potentially suspicious activity.


## Table of Contents

- [Lab Environment](#lab-environment)
- [Lab Architecture](#lab-architecture)
- [Wazuh Manager Installation](#wazuh-manager-installation)
- [Wazuh Agent Installation](#wazuh-agent-installation)
- [Sysmon Installation (Optional)](#sysmon-installation)
- [Detection Testing](#detection-testing)
- [Key Findings](#key-findings)
- [Future Improvements](#future-improvements)

---

## Lab Environment

| Component | Role
|------|---------|
| UTM | Virtualization Platform |
| Ubuntu Server 26.04 | Wazuh Manager |
| Windows 11 | Wazuh Agent |
| Kali Linux | Attacker Machine |
| Wazuh | SIEM Platform |

### VM Configuration

Each virtual machine was configured according to its role within the lab.

| Virtual Machine | Memory | Processors | Storage | Network Mode |
|---------|---------|---------|---------|---------|
| Ubuntu Server 26.04 | 8 GB | 2 | 60 GiB | Shared Network & Host Only |
| Windows 11 | 4 GB | 2 | 64 GiB | Shared Network & Host Only |
| Kali Linux | 4 GB | 2 | 40 GiB | Host Only |

Ubuntu Server and Windows 11 were configured with Shared Network (NAT) and Host Only adapters to provide internet access while maintaining an isolated network for communication between the virtual machines. Kali Linux was set up to use the Host Only network for controlled testing against the Windows 11 endpoint.

---

## Lab Architecture
```
┌─────────────────────────┐
│       Kali Linux        │
│     Attacker Machine    │
│     192.168.24.30       │
└────────────┬────────────┘
             │
             │ Attack Simulation
             │ Nmap, SMB Enumeration
             │
             ▼
┌─────────────────────────┐
│       Windows 11        │
│       Wazuh Agent       │
│     192.168.24.20       │
└────────────┬────────────┘
             │
             │ Security Event Collection
             │ Log Forwarding (TCP 1514)
             │
             ▼
┌─────────────────────────┐
│      Ubuntu Server      │
│      Wazuh Manager      │
│      Wazuh Dashboard    │
│      Wazuh Indexer      │
│      192.168.24.10      │
└─────────────────────────┘
```
---

## Wazuh Manager Installation
**Note:** Upon installing Ubuntu Server 26.04, the default interface was command-line based. Although not a requirement, the following commands were executed to install a graphical desktop environment and update the system packages:

```
sudo apt update && sudo apt upgrade -y
sudo apt install ubuntu-desktop -y
sudo reboot
```

After installing the Ubuntu desktop environment, the Wazuh Manager, Dashboard, and Indexer were installed using the Wazuh installation script downloaded with `curl`.

```
curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```

Upon successful installation, the Wazuh installation script provided the credentials required to access the Wazuh Dashboard. The Dashboard was accessed by entering the server's IP address into the web browser and providing the username and password.

```
https://192.168.24.10
```

![Wazuh Dashboard login](screenshots/wazuh-config/01-dashboard-login.png)

---

## Wazuh Agent Installation

After accessing the Wazuh Dashboard, **Deploy new agent** was selected to configure the Windows 11 agent with the following settings:
- **Operating system:** `Windows`
- **Server address:** `192.168.24.10`
- **Agent name:** `wazuh-agent`

![Wazuh Dashboard](screenshots/wazuh-config/02-wazuh-dashboard.png)
![Agent information](screenshots/wazuh-config/03-agent-information.png)

Following the configuration, the Wazuh Dashboard generated an installation command for the agent. The command was copied and executed in Windows PowerShell on the Windows 11 virtual machine to install the Wazuh agent.

```
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.9-1.msi -OutFile $env:tmp\wazuh-agent; msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='192.168.24.10' WAZUH_AGENT_NAME='wazuh-agent' 
```

After installing the Wazuh agent, the service was started using the following command in **Windows PowerShell**. The agent's status was then verified in the Wazuh Dashboard.

```
NET START Wazuh
```

![Start agent command](screenshots/wazuh-config/04-start-agent.png)
![Agent verification](screenshots/wazuh-config/05-agent-verification.png)

---

## Sysmon Installation (Optional)

As an optional enhancement, **Sysmon (System Monitor)** was installed on the Windows 11 endpoint to capture additional system activity and enhance security monitoring.

For detailed installation and configuration instructions, see
[Sysmon Installation and Configuration](docs/sysmon-installation.md).

---

## Detection Testing

The lab was tested by simulating security-related activities on the Windows 11 endpoint and verifying whether the resulting events were collected and analyzed by Wazuh. The following scenarios were selected to evaluate the SIEM's event monitoring and threat detection capabilities.


| Test Scenario | Objective
|------|---------|
| User Account Creation | Verify monitoring of newly created Windows user accounts |
| Failed Login Attempts | Identify unsuccessful authentication attempts |
| File Integrity Monitoring | Detect changes to monitored files and directories |
| Suspicious PowerShell Execution | Identify potentially suspicious command execution on the Windows endpoint |
| Network Reconnaissance | Investigate network scanning activity originating from the Kali Linux VM |
| SMB Enumeration | Detect attempts to discover available network shares and access shared resources on the Windows endpoint |

For detailed testing procedures, configuration, screenshots, and results, see [Detection Testing](detections/README.md).

---

## Key Findings

The lab successfully demonstrated centralized security event collection and investigation using Wazuh. The detection scenarios validated the platform's ability to identify and generate alerts for various security events, including:

- **Account Monitoring:** Detection of newly created accounts
- **Authentication Monitoring:** Identification of repeated failed login attempts
- **File Integrity Monitoring:** Detection of modifications to monitored files and directories
- **Process Monitoring:** Identification of potentially suspicious PowerShell command executions
- **Network Monitoring:** Investigation of network scanning and SMB share enumeration originating from Kali Linux

---

## Future Improvements

- Expand monitoring to additional endpoints
- Implement additional custom detection rules
- Implement automated responses to simulated attacks
- Improve alert correlation and investigation capability