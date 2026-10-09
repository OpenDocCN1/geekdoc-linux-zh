![](bbox=[0.31, 0.09, 0.86, 0.41])

*Figure 11-16: The SELinux feature of Red Hat Enterprise Linux 5.*

> This feature comes as part of Red Hat Enterprise Linux (RHEL) 4 and the later versions.

# ## SELinux Modes

SELinux has three different modes.

| **Mode** | **Description** |
| :--- | :--- |
| Disabled | In this mode, SELinux is turned off. So, MAC will not be implemented and the default DAC method will be prevalent. |
| Enforcing | In this mode, all security policies are enforced. Therefore, processes cannot violate the security policies. |
| Permissive | In this mode, SELinux is enabled, but the security policies are not enforced. So, processes can bypass the security policies. However, when a security violation occurs, it is logged and a warning message is sent to the user. |