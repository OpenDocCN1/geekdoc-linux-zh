![](bbox=[0.04, 0.11, 0.09, 0.145])

The netstat Command

# The netstat Command

The netstat command displays statistics about a network, including socket status, interfaces that have been auto-configured, memory statistics, and routing tables. With no arguments, the default netstat command displays open sockets. Some of the frequently used netstat command options are described in the following table.

| **Option** | **Displays** |
|---|---|
| -r or --route | The kernel routing tables. |
| -g or --groups | The multicast group membership. |
| -i r or --interface or --interface=iface | A table of all network interfaces or the specified interface. |
| -M or --masquerade | A list of masqueraded connections. |
| -s or --statistics | A summary of statistics for each protocol. |
| -e or --extend | Additional details. |

![](bbox=[0.31, 0.415, 0.87, 0.71])

Figure 12-17: The netstat command displaying a summary of statistics for each protocol.