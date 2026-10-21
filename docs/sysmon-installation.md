# Sysmon Installation and Configuration

This document describes the process of installing and configuring Sysmon to collect detailed system activity logs for security monitoring and investigation. 

## 1. Sysmon Download

The official Sysmon package was downloaded from the
[Microsoft Sysinternals website](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon).

![Sysmon webpage](/screenshots/sysmon-config/01-sysmon-webpage.png)


## 2. Sysmon Configuration File Download
After downloading and extracting the the Sysmon package, a configuration file was obtained to define which events Sysmon should monitor and log. The configuration template was downloaded from [SwiftOnSecurity's GitHub repository](https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml).

![SwiftOnSecurity GitHub](/screenshots/sysmon-config/02-sysmonconfig-github.png)

## 3. Sysmon Installation via Windows Powershell

Following this, the configuration file was moved to the extracted Sysmon directory in preparation for applying the configuration through **Windows PowerShell**.

![Configuration file directory](/screenshots/sysmon-config/03-sysmonconfig-move.png)

Windows PowerShell was opened as an administrator, and the directory containing the Sysmon executable was accessed. The following command was executed to install Sysmon and apply the downloaded configuration file. The license agreement was also accepted during the installation process.

```
.\sysmon64а.exe-i sysmonconfig-export.xml
```
![Sysmon installation command](/screenshots/sysmon-config/04-sysmon-installation-command.png)
***Note:** `Sysmon64a.exe` was selected because the Windows 11 virtual machine runs on an ARM64 architecture, consistent with the Apple Silicon host (MacBook Pro M1). Using the version that matches the guest operating system's architecture helps ensure compatibility.*

## 4. Verify Installation

The Windows **Services** console was then opened, and the `Sysmon64a` service was located to verify that it was running, indicating that Sysmon had been installed successfully.

![Services window](/screenshots/sysmon-config/05-verify-sysmon.png)