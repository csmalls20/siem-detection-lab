# Detection Testing

## Overview

This document outlines the security testing performed in the SIEM detection lab. Each test simulates a security-related activity to evaluate whether the resulting events are collected, analyzed, and, potentially flagged by Wazuh. 

Testing is primarily conducted on the Windows 11 endpoint, with selected activities originating from the Kali Linux machine. The Wazuh Dashboard is used to evaluate detection results by verifying event collection and reviewing generated alerts.

## Detection List

1. [User Account Creation](01-user-account-creation.md) - Monitors Windows user account creation events.
2. [Failed Logins](02-failed-logins.md) - Tests detection of repeated unsuccessful Windows authentication attempts.
3. [File Integrity Monitoring](03-file-integrity-monitoring.md) - Tests whether changes to monitored files generate alerts.
4. [Suspicious PowerShell Execution](04-suspicious-powershell-execution) - Detects potentially suspicious command execution using PowerShell.
5. [Network Reconnaissance](05-network-reconnaissance.md) - Identifies network scanning activity against the Windows 11 endpoint. 