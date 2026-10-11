# Objective 4
Find the YaST Module You Need

Being familiar with the RHEL system-config-\* tools, you possibly look for the corresponding tool in SUSE Linux Enterprise Server 10.

We compiled a table that lists the system-config-\* command on the left and the comparable YaST module on the right. You can access the module via the YaST Control Center or you can enter the command given in the right column in a console window.

The YaST modules do not match the respective system-config-\* tool exactly, but you will most likely find that they cover the functionality pretty well, and often offer more configuration options.

There are many more YaST modules than those listed here. To view the complete list, enter `yast -l` in a console window.

# Table 2-2

| RHEL | SLES 10 |
| :--- | :--- |
| system-config-authentication | yast2 nis<br>yast2 ldap<br>yast2 kerberos-client<br>yast2 samba-client |
| system-config-date | yast2 timezone |
| system-config-time (both are links to /usr/bin/consolehelper) | yast2 ntp-server |
| system-config-display | yast2 x11<br>sax2 |
| system-config-httpd | yast2 http-server |
| system-config-keyboard | yast2 keyboard |
| system-config-language | yast2 language |

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**