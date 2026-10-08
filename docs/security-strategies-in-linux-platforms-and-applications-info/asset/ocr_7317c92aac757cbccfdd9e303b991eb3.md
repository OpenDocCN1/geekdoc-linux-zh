# 214 PART 2 | Layered Security and Linux

| COMMAND | DESCRIPTION |
| --- | --- |
| aa-audit | Requires an existing security profile for a command or service. If profile exists, the aa-audit command changes the profile to audit mode. |
| aa-autodep | Creates a sample security profile for a command or service. |
| aa-complain | Requires an existing security profile for a command or service. If profile exists, the aa-complain command changes the profile to complain mode. |
| aa-enforce | Requires an existing security profile for a command or service. If profile exists, the aa-enforce command changes the profile to enforce mode. |
| aa-genproff | Reviews the /etc/apparmor.d/ directory for an existing profile for a command or service. If the profile does not exist, it's created using the aa-autodep. |
| aa-logprof | Reviews existing logs for suggested profile updates. |
| aa-notify | Lists denial log messages. |
| aa-status | Reviews current processes and processes. |
| aa-unconfined | Lists networked processes not controlled by AppArmor. |

FIGURE 7-8
An AppArmor configuration tool.

![](bbox=[0.235, 0.585, 0.915, 0.875])