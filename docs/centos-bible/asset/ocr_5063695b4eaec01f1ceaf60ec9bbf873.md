# # Part III Administration

# ## Turning on iptables

The iptables firewall feature, also referred to as *netfilter*, is the default firewall software when you install CentOS.

This section describes how to turn on iptables and set up firewall rules for several different types of situations. It also tells how to turn on features related to firewalls that allow your firewall to do Network Address Translation (NAT), IP masquerading, port forwarding, and transparent proxies.

> **NOTE**
> The CentOS startup scripts will punch a hole through your firewall if you use certain services, and will therefore power even if they are not explicitly enabled in your iptables configuration. For example, NTP (which sets your system time from a network time server) and DNS resolution (which lets you contact a DNS server to resolve addresses) both open the ports they need in your firewall.

The following procedure describes how to get iptables going on your CentOS system.

+   1. Set the iptables script to start automatically at boot time:
+      ```
+      # chkconfig iptables on
+      ```
+   2. Before you can start iptables, you must have a working set of rules that has been placed in your /etc/sysconfig/iptables file. To create those rules, refer to the examples in the following sections. (Without the configuration file, iptables fails silently.)

> **TIP**
> If you are new to iptables, you can start with a workable set of default values by configuring, using your firewall during the CentOS installation. I recommend selecting to enable the firewall and enabling only those services you are ready to offer. The resulting /etc/sysconfig/iptables file will let you study how CentOS creates its firewall rules.

+   3. If you are doing NAT or IP Masquerading, turn on IP packet forwarding. One way to allow this is to change the value of net.ipv4.ip_forward to 1 in the /etc/sysctl.conf file. Open that file as root user with any text editor and change the line to appear as follows:
+      ```
+      net.ipv4.ip_forward = 1
+      ```
+   4. Restart your network interfaces to have IP packet forwarding take effect.
+      ```
+      # /etc/init.d/network restart
+      ```
+   5. Once the rules file is in place, start up iptables:
+      ```
+      # /etc/init.d/iptables start
+      ```
+   6. At this point, iptables is installed as your firewall. You can check to see that the modules used by iptables are loaded by using the `lsmod` command. Here are some examples:
+      ```
+      # lsmod | less
+      Module             Size Used by
+      nf_conntrack_ftp   10656  0
+      ```