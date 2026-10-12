# ## 17.11 Lab – using SNMP

In this module we use some easily accessible command-line tools to explore SNMP:

+   * Linux: the UC Davis SNMP tools, which are distributed freely
+   * Windows-NT: the SNMP utilities included in the NT Server 4.0 Resource Kit.

These simple tools emphasize that using SNMP need not be a huge and expensive project.  
   We’re going to look at some standard variables in the *system* subtree. These all have the prefix: iso. og. dod. internet. mgmt. mib-2. *system* (1.3.6.1.2.1.1):

| Name | ID | Name | ID |
| :--- | :--- | :--- | :--- |
| **sysDescr** | 1 | **sysName** | 5 |
| **sysObjectID** | 2 | **sysLocation** | 6 |
| **sysUpTime** | 3 | **sysServices** | 7 |
| **sysContact** | 4 | | |

The details of these variables or objects are explained in full in RFC-2578, but briefly, they describe the name of the machine, who looks after it, where it is, etc. One other point we must mention is that SNMP has security mechanisms to prevent unauthorized people examining or changing settings. In version 1 of SNMP, authorization consists of sending a password, called the *community string*. This is sent “in clear” (not encrypted) in the request, so it can easily be *seen* with a sniffer and is therefore a security hole, which SNMP version 2 overcomes by adding authentication. In these examples below on a basic network where security hasn’t been configured, we will use the default community string **public** to gain access.

![](bbox=[0.06, 0.62, 0.88, 0.94])

**Figure 17.20** *snmpget* on Linux