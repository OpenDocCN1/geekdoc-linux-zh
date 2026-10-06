# Part III: Administering Fedora and RHEL

| iptables_filter | 6528 1 |
| ip_tables | 13840 1 iptable_filter |
| x_tables | 15380 7 xt_tcpudp,ip_REJECT,xt_state,ip_tables |

If want to allow passive FTP or ICMP connections from computers on your LAN, you may need to load these modules by adding them to the /etc/modprobe.conf file. The basic connection tracking module, ip_conntrack, should be loaded by default already. (See the description of passive FTP and IRC after the firewall-example sections.)

If there is an error in your /etc/sysconfig/iptables file, you can make a copy of that, and try to make a working configuration by using system-firewall and setting up a firewall. You can then make changes to your firewall to add the features that you need.

> TIP: As you add iptables rules, more modules will be loaded. Appropriate modules should be loaded automatically when a new rule is entered. Run again when you have added a few rules to see which modules were added. Note that these modules will not be unloaded if you decide to stop iptables. They will stay loaded until the next reboot or you remove them (modprobe -r).

The following sections contain examples of iptables rules.

# Creating iptables rules

One way to configure iptables is to start by adding and deleting rules to your kernel from the command line. When you get a set of rules that you like, you save the rules that are currently running on your system. The tools you use to create your firewall rules and then make them permanent as follows:

+   * iptables — Use this command to append (-A), delete (-D), replace (-R) or insert (-I) a rule. Use the -l option to list all current rules.
* service iptables save — Use this command to save the rules from the kernel and install them in the configuration file.
* /etc/sysconfig/iptables — This is the configuration file that contains the rules that were saved from the service iptables save command.
* /etc/sysconfig/iptables-config — You can add settings for managing your iptables rules to the iptables-config file. For example, iptables modules, such as ip_conntrack and others described later in this chapter, can be added to the IPTABLES_MODULES line to be loaded automatically. You can also set whether the iptables table in your running kernel is saved to a file when iptables stops.