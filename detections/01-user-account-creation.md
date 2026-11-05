# User Account Creation

## Objective

To verify that the creation of a local user account on the monitored Windows 11 endpoint is recorded and can be investigated through Wazuh.

---

## Test Procedure

Using the default Windows user account with administrative privileges, a new local user account was created by executing the following command in **Command Prompt**.

```
net user jane password /add
```

---

## Event Investigation

The Windows Security log was examined in Event Viewer to verify that the account creation was recorded. The activity was logged as **Event ID 4720**, which indicates that a user account was created in Windows.

![Event Viewer user creation log](../screenshots/user-account-creation/01-windows-event-viewer.png)

Using this Event ID, the Wazuh Dashboard was then examined to determine whether the event was collected.

![Wazuh Dashboard user creation log](../screenshots/user-account-creation/02-wazuh-dashboard.png)

---

## Detection Results

Wazuh successfully collected the account creation event and generated a corresponding alert. This confirmed that the activity was visible in the SIEM and identified by the configured detection rules.

---

## MITRE ATT&CK Mapping

- **Tactic:** Persistence
- **Technique:** Create Account: Local Account
- **Technique ID:** T1136.001