You can allow incoming packets meant for specific Internet services such as SSH, TELNET, and FTP. If you select a network interface such as eth0 (the first Ethernet card) as trusted, then all network traffic over that interface will be allowed without any filtering.

# Using the iptables command

It's somewhat complex to use the iptables command. iptables uses the concept of a chain, which is a sequence of rules. Each rule says what to do with a packet if the header contains certain information (such as the source or destination IP address). If a rule does not apply, iptables consults the next rule in the chain. By default, there are three chains:

+   - **INPUT chain:** The first set of rules against which packets are tested. The packets continue to the next chain only if the input chain does not specify DROP or REJECT.
+   - **FORWARD chain:** Contains the rules that apply to packets attempting to pass through this system to another system (for example, when you use a Red Hat Linux system as a router between your LAN and the Internet).
+   - **OUTPUT chain:** Includes the rules applied to packets before they are sent out (either to another network or to an application).

You can add rules to these chains or create new chains of rules by using the iptables command. You can also view the current chains and save them to a file. For example, if you have done nothing else, the iptables -L command should show the following:

```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

In this case, all three chains — INPUT, FORWARD, and OUTPUT — show the same ACCEPT policy, which means everything is wide open.

If you're setting up a packet filter, the first thing you do is specify the packets that you want to accept. For example, to accept packets from the 192.168.0.0 network, add the following rule to the input chain:

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```