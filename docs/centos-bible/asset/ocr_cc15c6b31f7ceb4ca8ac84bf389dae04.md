# **Part III Administration**

> **CAUTION** You want to ensure that the services on the ports to which you are allowing access are properly configured before you allow packets to be accepted to them.

+   UDP Rules (New Connections) — These lines define the ports where connection packets are accepted from the Internet for UDP services. In this example, I chose to accept requests for DNS service (`-destination port 53`) because the computer is set up as a DNS server. The example also illustrates lines that accept requests for the couple of other optional ports. Port 2074 is needed by some multimedia applications the users on your LAN might want to use, and port 4000 is used by the ICQ protocol (for online chat).

+   ICMP Rules — ICMP messages are really more for reporting conditions of the server than for actually providing services. Packets from the Internet that are accepted for ICMP protocol requests in our example are those for ICMP Types 3, 8, and 11. Type 3 service is needed when doing Path MTU Discovery (PMTUD). One of the answers of Type 3 is “Fragmentation needed but Don’t Fragment was set,” which is sent back to the Origin host so that this host can then reduce its packet size. Type 8 service, which allows your computer to accept echo request messages, makes it possible for people to ping your computer to see if it is available. Type 11 service relates to packets whose time to live (TTL) was exceeded in transit, and for which you are accepting a “Time Exceeded” message that is being returned to you. (You need to accept Type 11 messages to use the `traceroute` command to find broken routes to hosts you want to reach.)

**(4) FORWARD Chain Rules**

Because this firewall is also acting as a router, FORWARD rules are needed to limit what the firewall will and will not pass between the two networks (Internet and local LAN). The first line forwards everything from the local LAN (`-a FORWARD -i eth1`). The second line forwards anything from the Internet that is associated with an established connection (`--state ESTABLISHED, RELATED`).

**(5) OUTPUT Chain Rules**

These rules basically exist to prevent anyone from your local computer from *spoofing* IP addresses (i.e., from saying packets are coming from somewhere that they are not). According to these three rules, each packet output from your firewall must have as its source address one of the addresses from the firewall computer’s interfaces (`127.0.0.1`, `10.0.0.1`, or `123.45.67.89`).

**(6) POSTROUTING Chain Rules**

The POSTROUTING chain defines rules for packets that have been accepted, but need additional processing. This is where the actual Network Address Translation (NAT) work takes place. For the NAT table (`-t nat`), in the POSTROUTING chain, all packets that go out to the Internet have their addresses translated to that of the firewall’s external interface (`-o source 123.45.67.89`). In this case, I used the Source Network Address Translation (SNAT) chain because I have a static IP address (`123.45.67.89`) associated with my Internet connection. If I were using a dynamic IP address (via DHCP), I would use MASQUERADE instead of SNAT.