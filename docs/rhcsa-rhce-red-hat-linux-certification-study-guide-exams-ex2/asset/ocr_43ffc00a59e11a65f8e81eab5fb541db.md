In contrast, NAT hides the IP address of the computers of a LAN that connect to outside networks. NAT replaces the internal source address with the IP address of the gateway or router system with the firewall. That internal source address is cached on the gateway, so it knows which computer made the request.

When the firewall receives data such as a web page, the process is reversed. As the packets pass through the firewall, the originating computer is identified in the cache. The header of each packet is modified accordingly before the packets are sent on their way.

This approach is useful for several reasons. Hiding that internal IP addresses makes it harder for a cracker to know what IP address to use to break into an internal network. NAT supports connections between systems with private IP addresses and external networks such as the Internet. It's the reason why IPv4 addressing has survived for so long. In the Linux world, this process is known as IP masquerading.

# The Structure of the iptables Command

The way iptables commands are assembled into a firewall is based on “chains.” A chain of firewall rules may be applied to each network packet, in order. Each rule in a chain does two things: it specifies the conditions a packet must meet to match the rule, and it specifies the action if the packet matches.

The iptables command uses the following basic format:

```
iptables -t tabletype <action direction> <packet pattern> -j <what to do>
```

Now analyze this command, item by item. The first item is the -t tabletype switch. There are three basic tabletype options of interest for iptables:

+   - **filter** Sets a rule for filtering packets.
+   - **nat** Configures Network Address Translation, also known as masquerading, discussed later in this chapter.
+   - **mangle** Changes packet headers.

The default is filter; if you don't specify a -t tabletype, the iptables command assumes that you're trying to create a filtering rule.

The next item is the <action direction>. There are four basic actions associated with iptables rules:

+   - **-A (--append)** Appends a rule to the end of a chain.