
## Firewall computer

The firewall computer is set up as follows:

- **Local host** — `127.0.0.1` (IP address) and `lo` (interface). You shouldn't need to change these.
- **Connection to the Internet** — `123.45.67.89` (IP address) and `eth0` (interface). Replace them with the static IP address and interface name associated with your connection to the Internet, respectively.
- **Connection to the LAN** — `10.0.0.1` (IP address) and `eth1` (interface). Replace `10.0.0.1` and `eth1` with the static IP address and interface name associated with your connection to your LAN, respectively.
- **Computers on the LAN** — Each computer on the LAN in the example has an IP address from `10.0.0.2` to `10.0.0.254`. Change `10.0.0.255` to a number that matches your LAN's range of addresses.

Here is an example of a script to load firewall rules that could be used for the configuration shown in Figure 14-2:

```bash
# (1) Policies (default)
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

# (2) User-defined chain for ACCEPTED TCP packets
iptables -N okay
iptables -A okay -p TCP --syn -j ACCEPT
iptables -A okay -p TCP -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A okay -p TCP -j DROP

# (3) INPUT chain rules
# Rules for incoming packets from LAN
iptables -A INPUT -p ALL -i eth1 -s 10.0.0.0/24 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 10.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -i lo -s 123.45.67.89 -j ACCEPT
iptables -A INPUT -p ALL -i eth1 -d 10.0.0.255 -j ACCEPT

# Rules for incoming packets from the Internet
# Packets for established connections
iptables -A INPUT -p ALL -d 123.45.67.89 -m state --state \
ESTABLISHED,RELATED -j ACCEPT

# TCP rules
iptables -A INPUT -p TCP -i eth0 --destination-port 21 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 22 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 80 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 113 -j okay

# UDP rules
iptables -A INPUT -p UDP -i eth0 --destination-port 53 -j ACCEPT
iptables -A INPUT -p UDP -i eth0 --destination-port 2074 -j ACCEPT
iptables -A INPUT -p UDP -i eth0 --destination-port 4000 -j ACCEPT

# ICMP rules
iptables -A INPUT -p ICMP -i eth0 --icmp-type 8 -j ACCEPT
iptables -A INPUT -p ICMP -i eth0 --icmp-type 11 -j ACCEPT

# (4) FORWARD chain rules
# Accept the packets we want to forward
iptables -A FORWARD -i eth1 -j ACCEPT
iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT

# (5) OUTPUT chain rules
# Only output packets with local addresses (no spoofing)
iptables -A OUTPUT -p ALL -s 127.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 10.0.0.1 -j ACCEPT
iptables -A OUTPUT -p ALL -s 123.45.67.89 -j ACCEPT

# (6) POSTROUTING chain rules
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 123.45.67.89
```

I divided the commands in the preceding script into six sections. The following text describes each of those sections.

- **(1) Policies** — The `iptables -P` commands set the default policies for `INPUT`, `OUTPUT`, and `FORWARD` chains. By assigning each of those policies to `DROP`, any packet that isn’t matched is discarded. In other words, for a packet to get through, it has to be specifically matched and ACCEPTED by one of the other rules in the script.

- **(2) User-defined chain** — A user-defined chain I call `okay` is created to do a few more checks on packets requesting certain TCP services that I’m going to allow through (Web, FTP, and DNS services). The `N` `okay` option creates the `okay` chain. The next line says that a `SYN` packet (`--syn`), which requests a new connection, is fine to let through. The next line allows through packets associated with an `ESTABLISHED` connection (one that has already had traffic pass through the interface) or a `RELATED` connection (one that is starting a new connection related to an already established connection). The final line in this set tells `iptables` to `DROP` packets that don’t meet one of those checks.

- **(3) INPUT chain rules** — The bulk of the packet filtering is done in the `INPUT` chain. The first set of input rules indicates to `iptables` when to always accept packets from the Internet and from the LAN. The next three sets determine which requests for specific protocols (`TCP`, `UDP`, and `ICMP`) are accepted:

    - **Packets from LAN** — Because you want the users on your LAN and the firewall computer itself to be able to use the Internet, this set of rules lets through packets that are initiated from those computers. The first line tells iptables to accept packets for ALL protocols for which the source is an acceptable address on your LAN (`-s 10.0.0.0/24`, which represents IP numbers `10.0.0.1` through `10.0.0.254`). The next three lines allow packets that come from all valid IP addresses on the firewall computer itself (`-s 127.0.0.1`, `10.0.0.1` and `123.45.67.89`). The last line accepts broadcast packets (`-d 10.0.0.255`) on the LAN.

    - **Packets from Internet (already connected)** — This line is split in two (I just used the backslash to join the lines because the page wasn’t wide enough to show it as one line). It `ACCEPTS` packets that are both associated with connections that are already established (`-state ESTABLISHED,RELATED`) and are requested directly to the firewall’s IP address (`123.45.67.89`).

    - **TCP rules (new connections)** — Here is where you open up the ports for the TCP services you want to provide to anyone from the Internet. In these lines you open ports for FTP service (`-destination-port 21`), secure shell service (`22`), Web service (`80`), and `IDENT` authentication (`113`, the last of which might be necessary for protocols such as IRC. Instead of accepting these requests immediately, you jump to the `okay` chain you defined to further check that the packets were formed properly.

    > **CAUTION:** You want to ensure that the services on the ports to which you are allowing access are properly configured before you allow packets to be accepted to them.

    - **UDP rules (new connections)** — These lines define the ports where connection packets are accepted from the Internet for UDP services. In this example I chose to accept requests for DNS service (`-destination-port 53`) because the computer is set up as a DNS server. The example also illustrates lines that accept requests for a couple of other optional ports. Port 2074 is needed by some multimedia applications; the users on your LAN might want to use, and port 4000 is used by the ICQ protocol (for online chats).

    - **ICMP rules** — `ICMP` messages are really more for reporting conditions of the server than for actually providing services. Packets from the Internet that are accepted for `ICMP` protocol requests in our example are those for `ICMP` types `8` and `11`. Type `8` service, which allows your computer to accept *echo request messages*, makes it possible for people to ping your computer to see if it is available. Type `11` service relates to packets whose *time to live (TTL)* is exceeded in transit, and for which you are accepting a *Time Exceeded* message that is being returned to you. (You need to accept type `11` messages to use the `traceroute` command to find broken routes to hosts you want to reach.)

- **(4) FORWARD chain rules** — Because this firewall is also acting as a router, `FORWARD` rules are needed to limit what the firewall will and will not pass between the two networks (Internet and local `LAN`). The first line forwards everything from the local `LAN` (`-A FORWARD -i eth1`). The second line forwards anything from the Internet that is associated with an established connection (`-state ESTABLISHED,RELATED`).

- **(5) OUTPUT chain rules** — These rules basically exist to prevent anyone from your local computer from spoofing IP addresses (that is, from saying packets are coming from somewhere that they are not). According to these three rules, each packet output from your firewall must have as its source address one of the addresses from the firewall computer's interfaces (127.0.0.1, 10.0.0.1, or 123.45.67.89).

- **(6) POSTROUTING chain rules** — The POSTROUTING chain defines rules for packets that have been accepted, but need additional processing. This is where the actual network-address translation (NAT) work takes place. For the NAT table (-t nat), in the POSTROUTING chain, all packets that go out to the Internet have their addresses translated to that of the firewall's external interface (-to-source 123.45.67.89). In this case I used the Source Network Address Translation (SNAT) chain because I have a static IP address (123.45.67.89) associated with my Internet connection. If I were using a dynamic IP address (via DHCP), I would use MASQUERADE instead of SNAT. I would also have to change any references to -d 123.45.67.89 to -i eth0. (Of course, you would be using a different IP address and possibly a different Ethernet interface.)

## Example 2: Firewall for shared Internet connection (no servers)

In this scenario, the firewall is protecting a Linux system (firewall) and several systems on the LAN that only are used to connect to the Internet. No servers are behind this firewall, so you want to prevent people from the Internet from requesting services.

You could use the same script shown in Example 1, but not use lines that request TCP services. So you could drop the user-defined chain in section 2 and drop the TCP rules from section 3. You could also remove the ICMP rules, if you don't want your firewall to be visible to ping requests (Type 8) and if you don't care about receiving messages when your packets exceed their time-to-live values (Type 11), such as when a packet runs into a broken router.

## Example 3: Firewall for single Linux system with Internet connection

In this example, there is one network interface, connecting your Fedora system to the Internet. You are not sharing that connection with other computers and you are not offering any services from your computer.

In this case, you could cut sections 2, 4, and 6. From section 3, you could cut all rules relating to incoming requests from the LAN and all TCP services. As I mentioned in Example 2, you could also remove the Type 8 ICMP rule to make your firewall invisible to ping requests from the Internet and the Type 11 ICMP rule to not accept messages about failed time-to-live packets.
