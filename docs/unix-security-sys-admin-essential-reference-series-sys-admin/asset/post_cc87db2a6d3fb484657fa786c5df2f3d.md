
The rules for the forward group specify which packets may flow from one interface to another. These rules really make the firewall a firewall, either allowing or blocking traffic. You can also specify in the forwarding group whether or not a packet should be masqueraded. The forwarding rules are the only place where masquerading can be configured. The other two groups only concern the traffic on the physical interface.

These rules are constructed using various options of the ipfwadm command (Listing 12.2). It is very important to become familiar with these options. Incorrect rules may create subtle and not so subtle backdoors through your firewall.

Here are the most important options. The first option states the group for which the rule is intended. The -I is for the input group, the -O for the output group, and the -F for the forwarding group. You can then specify whether a rule should be added (-a), deleted (-d), or inserted (-i). The parameter of this option is the policy for the rule. This policy can be accept (accept the packet), reject (reject the packet), or deny (ignore the packet).

Neither reject nor deny allows matching packets in, but there is a subtle, yet important difference. A packet that is rejected will result in an ICMP message transmission to the sender of the original packet. The user originating the rejected message will get some sort of error message stating "connection refused." This error message gives potential intruders some information. It tells them that some host (the one sending the ICMP messages) "owns" the refused address; thus, the intruder now knows that perhaps some other attempt will succeed at that host.

A denied packet is silently ignored; thus, the intruder cannot tell whether there is no host responding or the packets are just tossed away. My advice is to always use a deny policy instead of a reject policy for your Internet connection. Connections on the local net may be rejected, so the local user will know they've been refused.

Using the -D and -S options of the ipfwadm command, you can specify the source and destination address. You can even mask bits from the address to specify a group of hosts belonging to the same subnet. This will save you a lot of typing and speed up the matching process in the firewall. Note that 0.0.0.0 matches all IP addresses (i.e., the world).

The next two important options are -k and -y. These two specify whether the ACK and SYNC flags in the TCP header should be set. (For more information on headers, see the sidebar "TCP/IP Headers.") You can use these options to block anyone from initiating a connection to your firewall. Although blocking SYNC packets originating in the Internet is generally a good idea, it does cause problems with SMTP and FTP protocols, as detailed later.

The last important option is the -p option. It specifies the default policy. The default policy is activated when no rule matches. This rule is a safety net of sorts: it closes all the unspecified possibilities in your packet filtering. For my firewall, I have set the default policy for all groups to deny, so all unknown packets are silently ignored. A few examples of these rules are shown in Listing 12.3.

## Figure 12.3 A simplified description of the TCP protocol.

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_143_0.png)

## TCP/IP Headers

Each packet transmitted across the network has a number of headers. The first is the header determined by the physical transport medium. In this case, that is Ethernet. These headers are not relevant to the firewall.

The second set of headers are the IP headers. The IP header contains the source and destination IP address. The firewall code will check these addresses against the specified rules. Besides these addresses, the header also has a TOS (Type Of Service) field, which describes the kind of traffic in the packet. In ftp data traffic, for example, this field will contain the hexadecimal number 8. The TOS field is not used in all packets.

A UDP header does not contain that much information; however, it does specify a source and destination port number. These port numbers can be useful when you want to write rules that allow only certain UDP services.

Last but not least, the TCP header has many fields, only a few of which are of interest. Just like the UDP header, the TCP header contains a source and destination port number. It also contains a number of bitfields that are used by the TCP protocol to make a TCP connection reliable. These bitfields are used to indicate the state of a packet. Figure 12.3 is a simplified description of the TCP protocol. The SYN and ACK denote when the SYN and ACK fields in the TCP header are set.

You can specify in your firewall rules whether the SYN and ACK fields should be set or cleared. Thus, you can keep anyone on the Internet from initiating a connection to your firewall by stating that the SYN bit may not be set on any packet that reaches your firewall via the Internet interface. Refusing all SYN packets, however, can cause problems with SMTP and ftp services. (See the section "Special Input Rules" in the main text for more information on problems with refusing SYN packets.)
