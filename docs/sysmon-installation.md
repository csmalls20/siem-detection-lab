# Sysmon Installation

This document describes the process of installing and configuring Sysmon to collect detailed system activity logs for security monitoring and investigation. 

The official Sysmon package was downloaded from the
[Microsoft Sysinternals website](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon).

![Sysmon webpage](/screenshots/sysmon-config/01-sysmon-webpage.png)

After downloading and extracting the the Sysmon package, a configuration file was obtained to define which events Sysmon should monitor and log. The configuration template was downloaded from [SwiftOnSecurity's GitHub repository](https://github.com/SwiftOnSecurity/sysmon-config/blob/master/sysmonconfig-export.xml).


![SwiftOnSecurity GitHub](/screenshots/sysmon-config/02-sysmonconfig-github.png)

Following this, the file was moved to the extracted directory of the Sysmon download.