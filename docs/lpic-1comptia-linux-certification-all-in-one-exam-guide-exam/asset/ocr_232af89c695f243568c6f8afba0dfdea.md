+   • -d ip_address/mask Specifies the destination address to be checked. If you want to check all IP addresses, use 0/0.
+   • -j target Specifies what to do if the packet matches the rule. You can specify ACCEPT, REJECT, DROP, or LOG actions.
+   • -i interface Specifies the interface where a packet is received. This only applies to INPUT and FORWARD chains.
+   • -o interface Specifies the interface where a packet is to be sent. This applies only to OUTPUT and FORWARD chains.

![](bbox=[0.05, 0.27, 0.18, 0.34])

> NOTE The options presented here represent only a sampling of what you can do with iptables. To see all the options available, see the iptables man page.

The best way to learn how to use iptables is to look at some examples. Table 17-4 has some sample iptables commands that you can start with.

You can use iptables to create a sophisticated array of rules that control how data flows through the firewall. Most administrators use the -P option with iptables to set up the firewall’s default filtering rules. Once the default is in place, then use iptables to configure exceptions to the default behavior needed by your particular network.

| iptables Command | Function |
| :--- | :--- |
| iptables -L | Lists existing rules. |
| iptables -D FORWARD ! | Deletes the first rule in the FORWARD chain. |
| iptables -t filter -F | Deletes all rules from the filter table. |
| iptables -P INPUT DROP | Sets a default policy for the INPUT chain that drops all incoming packets. |
| iptables -P FORWARD DROP | Configures your FORWARD chain to drop all packets. |
| iptables -A INPUT -s 0/0 -p icmp -j DROP | Configures the firewall to disregard all incoming PING packets addressed to the local Linux system. |
| iptables -A FORWARD -t cp -s 0/0 -sport 80 -j ACCEPT | Configures the firewall to allow HTTP traffic. |
| iptables -A INPUT -i eth0 -s 192.168.2.0/24 -j DROP | Configures the firewall to accept all incoming packets on eth0 coming from the 192.168.2.0 network. |

Table 17-4 iptables Commands