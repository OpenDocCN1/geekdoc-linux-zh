# The Firewall Configuration Tools

You can automate the process of configuring a firewall. For that purpose, RHEL includes both console and GUI versions of the Firewall Configuration tool. In this case, both tools are just filled with about the same number of features. While the look and feel of the two tools are different, the basic capabilities with respect to configuring access for trusted services are the same.

If you want to experiment with the Firewall Configuration tools, it's a good practice to first back up the associated configuration file, /etc/sysconfig/iptables. If mistakes are made, restore the original version of the file and run the following command:

```
# /etc/init.d/iptables restart
```

To learn about the changes that are made, compare the resulting /etc/sysconfig/iptables file with the backup. Any differences will be based on what you do in the Firewall Configuration tool.

> exam Watch If you use a Firewall Configuration tool, you may want to avoid editing the /etc/sysconfig/iptables file directly. Any changes will just be overwritten the next time you use that tool. Chapter 10 describes how you can set up customized rules with the Firewall Configuration tool.

# Trusted Services for Firewall Configuration Tools

Whichever tool is selected, both support easy configuration of a firewall to allow access to a variety of servers described in Table 4-6.

When comparing Table 4-6 to Table 4-5, you might note that while both TCP and UDP protocols are frequently reserved on a port for a specific service, frequently only one of these protocols is used by the actual service.

# The Console Firewall Configuration Tool

You can start the console firewall configuration tool with the system-config-firewall-tui command; the result is shown in Figure 4-5. As shown in the figure, firewalls are enabled by default; the option can be deselected.