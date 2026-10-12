# 2.1 z/VM system tools

Like Linux, the z/VM operating system has commands to display system information as well as system performance information. These commands are control program (CP) system commands. In this section we provide some CP commands that you can use to gather basic information about the status of the system.

# 2.1.1 Collecting technical setup information

Collect technical setup information as part of your information-gathering technique. To gather your release-level and service-level information use the command q cplevel, as shown in Figure 2-1.

```
q cplevel
z/VM Version 5 Release 3.0, service level 0703 (64-bit)
Generated at 03/13/08 07:41:44 EDT
IPL at 03/24/08 14:25:10 EDT
```

Figure 2-1 Sample output from the q cplevel command