
The single MASQUERADE rule on the `nat` table’s `POSTROUTING` chain remains unchanged. All forwarded traffic is masqueraded. (Locally generated traffic going out the `ppp0` interface is not masqueraded because the traffic is identified with the interface’s IP address, by definition.) The FORWARD rules in the `filter` table are limiting what traffic is forwarded and, therefore, what traffic is seen at the `POSTROUTING` chain.

## Applying Standard NAT to LAN Traffic to the Internet

Assuming that that site had a dynamically assigned but semi-permanent IP address or that it has a permanently assigned IP address, the more general SNAT version of source NAT would be used. Just as in the masquerading example, small residential sites often forward and NAT all outgoing LAN traffic:

```bash
iptables -t nat -A POSTROUTING -o <external interface> -j SNAT \
  --to-source <external address>
```

As with masquerading, a single SNAT rule can be sufficient. The NAT and connection state tracking take care of the incoming packets. The FORWARD rule pair is necessary, however, as in the following example:

```bash
iptables -A FORWARD -o <external interface> \
  -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -o <LAN interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT
```

In the case of small sites with 24×7 connections, it’s especially important to be selective about what traffic gets forwarded. The single FORWARD rule allowing outgoing new connections isn’t sufficient. Trojans and viruses are common. The newer networked devices can tend to be somewhat promiscuous about what they do over the network. There’s a good chance that Microsoft Windows machines and devices such as networked printers are generating far more traffic than you realize. Also, much of that local traffic is broadcast. It’s a good idea to avoid the risk of forwarding broadcast traffic. Routers are no longer supposed to forward directed broadcast traffic by default, but many still do. (Limited broadcasts don’t cross network boundaries without a relay agent to duplicate the packet and pass it on. Most devices use limited broadcasts.) A final reason is the case of attaching work laptops to the home network. Many employers don't want office laptops to have Internet access without VPN or the protection of their corporate firewalls and antivirus software.

## Examples of DNAT, LANs, and Proxies

For the residential and small-business site, destination NAT is probably the most welcome addition to Linux NAT.

### Host Forwarding

DNAT provides the host-forwarding capability that, until now, was available only through third-party solutions. For small sites with a single public IP address, DNAT allows incoming connections to local services to be transparently forwarded to a server running in a DMZ. Public services aren't required to run on the firewall machine.

With a single IP address, remote sites send client requests to the firewall machine. The firewall is the only local host address visible to the Internet. The service (for example, a web or mail server) itself is hosted internally in a private network. For packets arriving on that service's port, the firewall changes the destination address to that of the local server's network interface and forwards the packet to the private machine. The reverse is done for server responses. For packets from the server, the firewall changes the source address to that of its own external interface and forwards the packet on to the remote client.

The most common example is forwarding incoming HTTP connections to a local web server:

```bash
iptables -t nat -A PREROUTING -i <public interface> -p tcp \
  --sport 1024:65535 -d <public address> --dport 80 \
  -j DNAT --to-destination <local web server>
```

The tricky part is the question of what address is seen on each chain. Destination NAT was applied before the packet reached the FORWARD chain. So the rule on the FORWARD chain must refer to the internal server's private IP address rather than to the firewall's public address:

```bash
iptables -A FORWARD -i <public interface> -o <DMZ interface> -p tcp \
  --sport 1024:65535 -d <local web server> --dport 80 \
  -m state --state NEW -j ACCEPT
```

Connection tracking and NAT automatically reverse the translation for packets returning from the server. Because the initial connection request was accepted, a generic FORWARD rule suffices to forward the return traffic from the local server to the Internet:

```bash
iptables -A FORWARD -i <DMZ interface> -o <public interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT
```

Of course, don't forget that ongoing traffic from the client must be forwarded as well because the convention used in this book has been to separate individual service rules specifying the **NEW** state from a single rule for all ESTABLISHED or RELATED traffic:

```bash
iptables -A FORWARD -i <public interface> -o <DMZ interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT
```

### Host Forwarding and Port Redirection

DNAT can modify the destination port as well as the destination address. By way of example, I'll set up a rather contrived situation and build on the previous example. Let's say that this site has a second semi-private web server. The server is bound to port **81** on the same internal host. The internal host is running two separate web servers, hosting two different websites. Clients direct their requests to port **80** on the firewall. Port **81** is closed on the firewall. Incoming connections to the semi-private server are accepted from only specific remote addresses.

In other words, all incoming web connection requests are targeted to the firewall host's TCP port **80**. Requests from general client addresses are NATed and forwarded to port **80** on the server in the DMZ. Requests from specific remote clients are NATed and forwarded to a second web server on port **81** on the same server in the DMZ.

The NAT rule translates both the destination address and the destination port. The order of the two NAT rules is important here. The client traffic is originally targeted to port **80** in both cases. Firewall rules are ordered from most specific to most general. The selected clients must be selected out and redirected to port **81** before their packets match the more general rule that matches all clients and redirects packets to port **80** on the internal host:

```bash
iptables -t nat -A PREROUTING -i <public interface> -p tcp \
  -s <Allowed remote host> --sport 1024:65535 \
  -d <public address> --dport 80 \
  -j DNAT --to-destination <local web server>:81

iptables -t nat -A PREROUTING -i <public interface> -p tcp \
  --sport 1024:65535 -d <public address> --dport 80 \
  -j DNAT --to-destination <local web server>
```

The rule on the **FORWARD** chain must refer to the internal server's private IP address and port **81** rather than to the firewall's public address and port **80**. Rule order is not important here. The NAT modification was done previously on the **PREROUTING** chain. The forwarding rules see the modified packets:

```bash
iptables -A FORWARD -i <public interface> -o <DMZ interface> -p tcp \
  --sport 1024:65535 -d <local web server> --dport 81 \
  -m state --state NEW -j ACCEPT
```

```bash
iptables -A FORWARD -i <public interface> -o <DMZ interface> -p tcp \
  --sport 1024:65535 -d <local web server> --dport 80 \
  -m state --state NEW -j ACCEPT
```

As in the previous example, the single generic FORWARD rule pair for ongoing connections is repeated here:

```bash
iptables -A FORWARD -i <DMZ interface> -o <public interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -i <public interface> -o <DMZ interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT
```

### Host Forwarding to a Server Farm

DNAT can accept a range of destination addresses to translate to, and it selects one of the addresses when the exchange is initiated. As an example of multiple destination addresses, let’s say that this site has a handful of public web servers. A web server is advertised as running on one of these addresses. Five duplicate web servers are running in the DMZ, each assigned a different private IP address ranging from 192.168.1.1 to 192.168.1.5. Remote clients address the web server at the single public address.

The NAT rule translates the original destination address to one of the addresses in the NAT list:

```bash
iptables -t nat -A PREROUTING -i <public interface> -p tcp \
  --sport 1024:65535 -d <public web address> --dport 80 \
  -j DNAT --to-destination 192.168.1.1-192.168.1.5
```

The private server address range was chosen to allow the FORWARD rule to use an address mask to match any of the servers’ addresses:

```bash
iptables -A FORWARD -i <public interface> -o <DMZ interface> -p tcp \
  --sport 1024:65535 -d 192.168.1.0/29 --dport 80 \
  -m state --state NEW -j ACCEPT
```

As in the previous examples, the single generic FORWARD rule pair for ongoing connections is repeated here:

```bash
iptables -A FORWARD -i <DMZ interface> -o <public interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -A FORWARD -i <public interface> -o <DMZ interface> \
  -m state --state ESTABLISHED,RELATED -j ACCEPT
```
