# Chapter 4. The sysconfig Directory

+   - SETCOLOR_SUCCESS=<value>, where <value> sets the color to a color indicating success via the echo --command. The default color is set to green.
- SETCOLOR_FAILURE=<value>, where <value> sets the color to a color indicating failure via the echo --command. The default color is set to red.
- SETCOLOR_WARNING=<value>, where <value> sets the warning color via the echo --command. The default color is set to yellow.
- SETCOLOR_NORMAL=<value>, where <value> resets the color to "normal" via the echo -en.
- LOGLEVEL=<value>, where <value> sets the initial console level for the kernel. The default is 3; 8 everything (including debugging); 1 means nothing except kernel panics. The syslog daemon overrides this setting once set.
- PROMPT=<value>, where <value> is one of the following boolean values:
  - yes - Enables the key for interactive mode.
  - no - Disables the key for interactive mode.

# 4.1.15. /etc/sysconfig/ipchains

The /etc/sysconfig/ipchains file contains information used the ipchains initialization script when using the ipchains service.
This file is modified by typing the command /sbin/service ipchains save when valid ipchains rules are in place. Do not manually edit this file. Instead, use the /sbin/ipchains command to configure the necessary packet filtering rules and then save the rules to this file using /sbin/service ipchains save.

Use of ipchains to set up firewall rules is not recommended as it is deprecated and may disappear from future releases of Red Hat Linux. If a firewall is, use iptables instead.

# 4.1.16. /etc/sysconfig/iptables

Like /etc/sysconfig/ipchains, /etc/sysconfig/iptables file stores information used by the kernel to set up packet filtering rules at boot time or when the service is started.
Do not modify this file by hand unfamiliar with how construct iptables rules. The easiest way to add rules is to use the Security Level Configuration Tool (redhat-config-securitylevel), or the GNOME Lokit command, the /usr/sbin/lokkit command to create a firewall. These applications edit this file at the end.

Rules can be created manually by using /sbin/iptables: then type /sbin/service iptables save to add the rules to the /etc/sysconfig/iptables file.
Once this file exists, any firewall rules saved it persists through a system reboot or service restart.
For more information on iptables see Chapter 16.

# 4.1.17. /etc/sysconfig/irda

The /etc/sysconfig/irda file controls infrared devices on the system are configured at startup.
The following values may be used:

+   - IRDA=<value>, where <value> is one of the following boolean values: