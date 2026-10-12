To launch Configure Firewalling from the Red Hat menu, click System Tools → More System Tools → Lokkit. Figure 14-1 shows the Configure Firewaling window.

With Configure Firewalling open, you are ready to start. Two warnings before you begin:

+   The Configure Firewaling window overwrites rules created previously. Just to be safe, you should back up your previous rules as follows:
+   
+   ```bash
+   # cp /etc/sysconfig/iptables /etc/sysconfig/iptables.old
+   ```

+   Run this procedure from the console (not over the network) because if you make a mistake setting up your firewall, you might block network access and not be able to reconnect to your computer to fix the problem.

![](bbox=[0.2, 0.32, 0.72, 0.58])

The following steps will help you answer questions about your firewall:

+   1.  **Basic Configuration** — Choose High Security if you mostly use the computer as a client for Web browsing, but not as a server (no shared printers, file systems, and so on). Low Security is best to begin with for a server computer. Only choose Disable Firewall if no connections to outside networks exist.

+   2.  **Local Hosts** — If you are connected to a local network that does not access the Internet, you can choose to trust your connection to that network (Yes). Say No, for example, if the interface provides a connection to a cable modem or DSL line.

+   3.  **DHCP** — Choose Yes if your network addresses are assigned via DHCP (say No if you are using static IP addresses you assign yourself).

+   4.  **Services** — Even as a mostly-client computer, you may want to share some network services. If so, select Yes and you will be able to activate the following services: