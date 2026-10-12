
- **Packets from Internet (already connected)** — This line is split in two (I just used the backslash to join the lines because the page wasn't wide enough to show it as one line). It ACCEPTS packets that are both associated with connections that are already established (`--state ESTABLISHED,RELATED`) and are requested directly to the firewall's IP address (123.45.67.89).

- **TCP rules (new connections)** — Here is where you open up the ports for the TCP services you want to provide to anyone from the Internet. In these lines you open ports for FTP service (`--destination-port 21`), secure shell service (22), Web service (80), and IDENTD authentication (113), the last of which might be necessary for protocols such as IRC. Instead of accepting these requests immediately, you jump to the okay chain you defined to further check that the packets were formed properly.

> **CAUTION:** You want to ensure that the services on the ports to which you are allowing access are properly configured before you allow packets to be accepted to them.

- **UDP rules (new connections)** — These lines define the ports where connection packets are accepted from the Internet for UDP services. In this example I chose to accept requests for DNS service (`--destination-port 53`) because the computer is set up as a DNS server. The example also illustrates lines that accept requests for a couple of other optional ports. Port 2074 is needed by some multimedia applications the users on your LAN might want to use, and port 4000 is used by the ICQ protocol (for online chats).

- **ICMP rules** — ICMP messages are really more for reporting conditions of the server than for actually providing services. Packets from the Internet that are accepted for ICMP protocol requests are those for ICMP types 8 and 11. Type 8 service, which allows your computer to accept *echo reply messages*, makes it possible for people to ping your computer to see if it is available. Type 11 service relates to packets whose *time to live* (TTL) was exceeded in transit, and for which you are accepting a Time Exceeded message that is being returned to us. (You need to accept Type 11 messages to use the *traceroute* command to find broken routes to hosts you want to reach.)

### (4) **FORWARD chain rules** — Because this firewall is also acting as a router, FORWARD rules are needed to limit what the firewall will and will not pass between the two networks (Internet and local LAN). The first line forwards everything from the local LAN (`-A FORWARD -i eth1`). The second line forwards anything from the Internet that is associated with an established connection (`--state ESTABLISHED,RELATED`).

### (5) **OUTPUT chain rules** — These rules basically exist to prevent anyone from your local computer from *spoofing* IP addresses (that is, from saying packets are coming from somewhere that they are not). According to these three rules, each packet output from your firewall must have as its source address one of the addresses from the firewall computer's interfaces (127.0.0.1, 10.0.0.1, or 123.45.67.89).

### (6) **POSTROUTING chain rules** -- The POSTROUTING chain defines rules for packets that have been accepted, but need additional processing. This is where the actual network-address translation (NAT) work takes place. For the NAT table (-t `nat`), in the POSTROUTING chain, all packets that go out to the Internet have their addresses translated to that of the firewall's external interface (`--to-source 123.45.67.89`). In this case I used the Source Network Address Translation (SNAT) chain because I have a static IP address (123.45.67.89) associated with my Internet connection. If I were using a dynamic IP address (via DHCP), I would use MASQUERADE instead of SNAT. I would also have to change any references to `-d 123.45.67.89` to `-i eth0`. (Of course, you would be using a different IP address and possibly a different Ethernet interface.)

## Example 2: Firewall for shared Internet connection (no servers)

In this scenario, the firewall is protecting a Linux system (firewall) and several systems on the LAN that only want to connect to the Internet. No servers are behind this firewall, so you want to prevent people from the Internet from requesting services.

You could use the same script shown in Example 1, but not use lines that request TCP services. So you could drop the user-defined chain in section 2 and drop the TCP rules from section 3. You could also remove the ICMP rules, if you don't want your firewall to be invisible to `ping` requests (Type 8) and if you don't care about receiving messages when your packets exceed their time to live values (Type 11), such as when a packet runs into a broken router.

## Example 3: Firewall for single Linux system with Internet connection

In this example, there is one network interface, connecting your Red Hat Linux system to the Internet. You are not sharing that connection with other computers and you are not offering any services from your computer.

In this case, you could cut sections 2, 4, and 6. From section 3, you could cut all rules relating to incoming requests from the LAN and all TCP services. As I mentioned in Example 2, you could also remove the Type 8 ICMP rule to make your firewall invisible to `ping` requests from the Internet and the Type 11 ICMP rule to not accept messages about failed time-to-live packets.

## Understanding iptables

Now that you've seen something about what iptables rules look like and how you can get them going, step back a bit and see how iptables works.

The iptables feature works by having IP packets (that is, network data) that enter or leave the firewall computer, traverse a set of chains that define what is done with the packet. Each rule that you add essentially does the following:

- Checks if a particular criterion is met (such as that a packet requests a particular service or comes from a particular address) and
- Takes an action (such as dropping, accepting, or further processing a packet).

Different sets of rules are implemented for different types of tables. For example, tables exist for filtering (filter), network address translation (nat), and changing packet headers (mangle). Depending on the packet's source and destination, it traverses different chains. Most of the rules you create will relate to the filter table (which is implied if no other table is given).

The chains associated with the filter table are INPUT, OUTPUT, and FORWARD. You can add user-defined chains as well. You will probably be most interested in adding or removing particular TCP and UDP services using the basic rules shown in the previous example. Assign ACCEPT to packets you want to go through and DROP to those you want to discard. You can also assign REJECT to drop a packet but return a message to the sender, or LOG to neither drop nor accept the message, but to log information about the packet.

A lot of great features are built into iptables. The following descriptions tell you about some cool things you can do with iptables and give you some tips on using it.

## Allowing FTP and IRC services through an iptables firewall

With passive FTP, the FTP client sends its IP address and the port number on which it will listen for data to the server. If that client is on a computer that is behind your firewall, for which you are doing NAT, that information must be translated as well or the FTP server will not be able to communicate with the client.

iptables uses connection-tracking modules to track connections. Using this feature, it can look inside the FTP data themselves (that is, not in the IP packet header), to get the information it needs to do NAT (remember that computers from the Internet can't talk directly to your private IP addresses). To do FTP connection tracking (to allow passive FTP connections to the clients on your LAN), you need to have the following modules loaded:

- ip_conntrack
- ip_conntrack_ftp
- ip_nat_ftp

The same is true for chats (IRC) and DCC sends. Addresses and port numbers are stored within the IRC protocol packets, so those packets must be translated too. To allow clients on your LAN to use IRC services, you need to load the following modules:

- ip_conntrack_irc
- ip_nat_irc

The default port for IRC connections is 6667. If you don't want to use the default you can add different port numbers when you load the connection-tracking modules:

```
insmod ip_conntrack_irc.o ports=6668,6669
```
