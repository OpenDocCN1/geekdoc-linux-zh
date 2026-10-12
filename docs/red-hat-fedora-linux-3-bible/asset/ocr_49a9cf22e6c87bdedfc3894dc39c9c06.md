> **TIP:** If you are new to iptables, you can start with a workable set of default values by configuring your firewall during Fedora installation. I recommend selecting a Medium security firewall and configuring a few services to be allowed. The resulting `/etc/sysconfig/iptables` file will let you study how Fedora creates its firewall rules.

+   5. If you are doing NAT or IP Masquerading, turn on IP packet forwarding. One way to allow this is to change the value of `net.ipv4.ip_forward` to 1 in the `/etc/sysctl.conf` file. Open that file as root user with any text editor and change the line to appear as follows:
+   `net.ipv4.ip_forward = 1`

+   6. Restart your network interfaces to have IP packet forwarding take effect.
+   `# /etc/init.d/network restart`

+   7. Once the rules file is in place, start up iptables:
+   `# /etc/init.d/iptables start`

+   8. At this point, iptables is installed as your firewall. You can check to see that the modules used by iptables are loaded by using the `lsmod` command, as follows:
+   `# lsmod | grep ip`
+   ```
+   ipt_REJECT		4736	1
+   ipt_state		1536	7
+   ip_conntrack	24368	1	ipt_state
+   iptables_filter	2176	1
+   iptables			13568	3	ipt_REJECT, ipt_state, iptable_filter
+   ```

+   9. If you want to allow passive FTP or IRC connections from computers on your LAN, you may need to load those modules by adding them to the `/etc/modules.conf` file. The basic connection tracking module, `ip_conntrack`, should be loaded by default already.
+   (See the description of passive FTP and IRC after the firewall-example sections.)

If your iptables service didn’t start, make sure that:

+   - An ipchains module is not loaded. (Unload it with `modprobe -r` as shown previously.)
+   - The `/etc/sysconfig/iptables` file exists. (You need to create one if one was not already created for you when you installed Fedora.)

> **TIP:** As you add iptables rules, more modules will have to be loaded. Appropriate modules should be loaded automatically when a new rule is entered. Run `lsmod | grep ip` again after you have added a few rules to see which modules were added. Note that these modules will not be unloaded if you decide to stop iptables. They will stay loaded until the next reboot or until you remove them (modprobe -r).

The following sections contain examples of iptables firewall rules.