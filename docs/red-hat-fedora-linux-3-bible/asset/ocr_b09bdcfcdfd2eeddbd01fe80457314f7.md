can use iptables. In fact, if you try to use the iptables script (`/etc/init.d/iptables`) to start iptables while the ipchains module is loaded, the iptables startup script silently fails and exits.

While iptables is generally considered to be more complex than ipchains to work with, it is also considered to be more powerful and flexible. Because development is not continuing for ipchains, the few broken ipchains features that exist will probably stay broken.

This section describes how to turn on iptables and set up firewall rules for several different types of situations. It also tells how to turn on features related to firewalls that allow your iptables firewall to do Network Address Translation (NAT), IP masquerading, port forwarding, and transparent proxies.

> **NOTE**: The Fedora startup scripts will "punch a hole" through your firewall if you use certain services, and will therefore work even if they are not explicitly enabled in your `iptables` configuration. For example, NTP (which sets your system time from a network time server) and DNS resolution (which lets you contact a DNS server to resolve addresses) both open the ports they need in your firewall.

# Turning on iptables

The following procedure describes how to get iptables going on your Fedora system.

> **TIP**: During the time that you turn off ipchains, turn on iptables, and configure the filtering rules for iptables, your computer may be unprotected from the network. You should test your firewall rules on non-critical computers, and then perform the switch on critical computers either quickly or by temporarily shutting down your network interfaces.

+   1. Stop the ipchains script from starting automatically at boot time:
+   # chkconfig ipchains off
+   
+   2. Set the iptables script to start automatically at boot time:
+   # chkconfig iptables on
+   
+   3. Now you can either reboot Fedora, or stop ipchains and unload the ipchains module, as follows:
+   # service ipchains stop
+   # modprobe -r ipchains
+   
+   4. Before you can start iptables you must have a working set of rules that have been placed in your `/etc/sysconfig/iptables` file. To create those rules, refer to the examples in the following sections. (Without the configuration file in place, iptables fails silently.)