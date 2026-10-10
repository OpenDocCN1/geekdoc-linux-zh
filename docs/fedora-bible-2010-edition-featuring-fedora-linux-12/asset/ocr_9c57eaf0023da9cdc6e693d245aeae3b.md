4. Restart your network interfaces to have IP packet forwarding take effect.

```
# /etc/init.d/network restart
```

> TIP: You can also use `sysctl -p` to have the kernel pick up forwarding changes. We recommend restarting networking, though.

5. Once the rules file is in place, start up iptables:

```
# /etc/init.d/iptables start
```

6. At this point, iptables is installed as your firewall. You can check to see that the modules used by iptables are loaded by using the `lsmod` command. Here are some examples:

```
# lsmod | less
```

Module Size Used by
Ip6t_REJECT 4716 2
nf_conntrack_ipv6 18784 2
iptable_filter 3360 1
ip6_tables 11684 1 ip6table_filter

7. If you want to allow passive FTP or IRC connections from computers on your LAN, you may need to load those modules by adding them to the `/etc/modprobe.conf` file. The basic connection tracking module, `ip_conntrack`, should be loaded by default already. (See the description of passive FTP and IRC after the firewall-examples sections.)

If there is an error in your `/etc/sysconfig/iptables` file, you can make a copy of that file, and then try to make a workable configuration by running `system-config-firewall` and setting up a basic firewall. You can then make changes to your firewall to add the features that you need.

> TIP: As you add iptables rules, more modules will have to be loaded. Appropriate modules should be loaded automatically when a new rule is entered. Run `lsmod | less` again after you have added a few rules to see which modules were added. Note that these modules will not be unloaded if you decide to stop iptables. They will stay loaded until the next reboot or until you remove them (`modprobe -r`).

The following sections contain examples of iptables firewall rules.

# Creating iptables firewall rules

One way to configure iptables is to start by adding and deleting rules to your kernel from the command line. Then when you get a set of rules that you like, you save the rules that are currently running on your system. The tools you use to create your firewall rules and then make them permanent are as follows:

+   - `iptables` — Use this command to append (-A), delete (-D), replace (-R), or insert (-I) a rule. Use the -L option to list all current rules.