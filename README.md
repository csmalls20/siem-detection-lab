# SIEM Detection Lab

This lab demonstrates centralized security log collection, analysis, and threat detection using Wazuh within an isolated virtual network environment designed to simulate a small-scale Security Operations Center (SOC). It illustrates how security events are collected from endpoints, analyzed by the SIEM, and investigated to identify potentially suspicious activity.


## Table of Contents

- [Lab Environment](#lab-environment)
- [Lab Diagram](#lab-diagram)
- [Wazuh Manager Installation](#wazuh-manager-installation)

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
| Ubuntu Server 26.04 | 4 GB | 2 | 60 GiB | Shared Network & Host Only |
| Windows 11 | 4 GB | 2 | 64 GiB | Shared Network & Host Only |
| Kali Linux | 4 GB | 2 | 40 GiB | Host Only |

Ubuntu Server and Windows 11 were configured with Shared Network (NAT) and Host Only adapters to provide internet access while maintaining an isolated network for communication between the virtual machines. Kali Linux was set up to use the Host Only network for controlled testing against the other machines.

## Lab Diagram

Picture of lab architecture

--
## Wazuh Manager Installation