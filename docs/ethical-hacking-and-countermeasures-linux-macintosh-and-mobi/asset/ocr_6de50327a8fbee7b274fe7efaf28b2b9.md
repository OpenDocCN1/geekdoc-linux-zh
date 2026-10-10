To run IPTables, the following options have to be configured in the kernel. The CONFIG_PACKET option allows applications and utilities to work directly with various network devices. It simplifies the behavior of packets negotiating the built-in chains (INPUT, OUTPUT, and FORWARD). The iptables command is used to configure both IP filtering and Network Address Translation (NAT). There is a separation of packet filtering and NAT functionality. To facilitate this, there are two tables of rules called filter and nat. The filter table is used if a user does not specify the -t option to override it.

Five built-in chains are also provided. The INPUT and FORWARD chains are available for the filter table, the PREROUTING and POSTROUTING chains are available for the nat table, and the OUTPUT chain is available for both tables. All connection tracking is handled in the PREROUTING chain, except locally generated packets, which are handled in the OUTPUT chain. IPTables does all recalculation of states within the PREROUTING chain. If an initial packet is sent in a stream, the state gets set to NEW within the OUTPUT chain, and when the system receives a return packet, the gate gets changed in the PREROUTING chain to ESTABLISHED. If the local machine does not originate the first packet, the NEW state is set within the PREROUTING chain. So, all state changes and calculations are done within the PREROUTING and OUTPUT chains of the nat table.

# ## How IPTables Works

It can also control the rate-limited connection and logging capability, apart from the ability to filter on TCP flag and TCP options, and also MAC addresses. The following steps show how IPTables works:

+   1. One packet enters the network interface.
+   2. The interface unpacks the data-link layer information.
+   3. The interface forwards the packet to the kernel.
+   4. The kernel investigates the packet and chooses to reject, drop, or accept it.

Figure 1-9 shows an IPTables decision tree. Figure 1-10 shows how a packet interacts with IPTables.

# ## Tool: Netfilter

To simplify aspects of datagram processing in the kernel firewalling code and to produce a filtering framework that was both cleaner and more flexible, Paul Russell made a new framework called Netfilter. The IPTables utility is used to configure Netfilter filtering rules. Its syntax borrows heavily from the IPChains command, but differs in that its functionality can be extended without recompiling it. It manages this by using shared libraries.

There are three basic functionalities that Netfilter offers:

+   1. Accepts the packet or allows the packet to pass through
+   2. Rejects the packet and informs the source of the filter rule
+   3. Discards the packet

# ## IPTables Command

IPTables looks at each incoming packet and decides what to do with it. Multiple tables can be used, depending upon the type of packet being monitored and what is to be done with the packet. The IPTables command has the following syntax:

```
iptables [-t <table-name>]<command> <chain-name> <parameter-1><option1> <parameter-n> <option-n>
```

The following command configures IPTables to allow the firewall to accept TCP packets coming on the interface, echoing from any IP address destined for the firewall's IP address of 192.168.1.1:

```
iptables -A INPUT -s 0/0 -i eth0 -d 192.168.1.1 -p TCP -j ACCEPT
```

The following pair of commands configures IPTables to allow the firewall to send ICMP echo requests (pings) and, in turn, accept the expected ICMP echo replies:

```
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
```