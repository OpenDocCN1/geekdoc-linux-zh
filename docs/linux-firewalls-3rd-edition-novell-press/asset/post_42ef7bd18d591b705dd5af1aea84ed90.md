
## Using Connection State to Bypass Rule Checking

Specifying the state match for previously initiated and accepted exchanges enables you to bypass the firewall tests for the ongoing exchange. The initial client request remains controlled by the service’s specific filters, however. The following code checks for established connections:

```bash
$IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
$IPT -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

$IPT -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
# Using the state module alone, INVALID will break protocols that use
# bidirectional connections or multiple connections or exchanges,
# unless an ALG is provided for the protocol. At this time, FTP is the
# only protocol with ALG support.

$IPT -A INPUT -m state --state INVALID -j LOG \
  --log-prefix 'INVALID input: '
$IPT -A INPUT -m state --state INVALID -j DROP

$IPT -A OUTPUT -m state --state INVALID -j LOG \
  --log-prefix 'INVALID output: '
$IPT -A OUTPUT -m state --state INVALID -j DROP

$IPT -A FORWARD -m state --state INVALID -j LOG \
  --log-prefix 'INVALID forward: '
$IPT -A FORWARD -m state --state INVALID -j DROP
```

## Source-Address Spoofing and Other Bad Addresses

This section establishes some filters based on source and destination addresses. These addresses will never be seen in a legitimate packet.

At the packet-filtering level, one of the few cases of source-address spoofing that you can identify as a forgery with certainty is your own IP address. These rules deny incoming packets claiming to be from you:

```bash
# Refuse spoofed packets pretending to be from you
$IPT -A INPUT -s $DMZ_IPADDR -j DROP
$IPT -A INPUT -s $LAN_IPADDR -j DROP

$IPT -A FORWARD -s $DMZ_IPADDR -j DROP
$IPT -A FORWARD -s $LAN_IPADDR -j DROP

$IPT -A INPUT -i $DMZ_INTERFACE \
 -s $LAN_ADDRESSES -j DROP
```

The preceding rules are redundant if you have activated the rp_filter kernel facility. It's good practice to define the rules explicitly.

Likewise, the firewall rules drop packets that don’t contain a local source address. Regardless, it’s good practice to explicitly define a rule to implement RFC 2827, “Network Ingress Filtering: Defeating Denial of Service Attacks Which Employ IP Source Address Spoofing”:

```bash
$IPT -A FORWARD -o $DMZ_INTERFACE \
    -s ! $LAN_ADDRESSES -j DROP
```

```bash
$IPT -A FORWARD -i $LAN_INTERFACE \
    -s ! $LAN_ADDRESSES -j DROP
```

```bash
$IPT -A OUTPUT -o $DMZ_INTERFACE -s ! $DMZ_IPADDR -j DROP
$IPT -A OUTPUT -o $LAN_INTERFACE -s ! $LAN_IPADDR -j DROP
```

We’ll skip the rules from Chapter 4 that checked for private network source addresses. The gateway firewall is performing that function.

The next sets of rules are primarily for completeness. Both of the firewall’s default policies are to drop everything. As such, broadcast addresses are dropped by default and must be explicitly enabled when they are wanted:

```bash
# Refuse malformed broadcast packets
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $BROADCAST_SRC -j DROP
```

```bash
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $BROADCAST_SRC -j DROP
```

```bash
# Don’t forward directed broadcasts
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $DMZ_NETWORK -j DROP
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE \
    -d $DMZ_BROADCAST -j DROP
```

```bash
# Don’t forward limited broadcasts in either direction
$IPT -A FORWARD -d $BROADCAST_DEST -j DROP
```

Multicast is always sent over UDP. Whether or not you add rules to accept incoming multicast, the following rules block illegal multicast packets:

```bash
$IPT -A INPUT -p ! udp -d $CLASS_D_MULTICAST -j DROP
$IPT -A FORWARD -p ! udp -d $CLASS_D_MULTICAST -j DROP
```

## Filtering ICMP Control and Status Messages

When the connection state tracking is used, ICMP error messages are forwarded for existing connections, and incoming and outgoing messages are accepted. The error messages are RELATED messages. Otherwise, ICMP traffic would require explicit acceptance rules.

ping's `echo-request` message type must be allowed explicitly, in any case. `echo-request` and `echo-reply` are diagnostic messages rather than error messages related to an ongoing exchange. Also of note regarding `echo-request` is that DHCP sometimes relies on `echo-request` to discover whether an address that is about to be assigned is already in use by a host on the local network.

Rather than duplicating the ICMP rules from Chapter 4, I'll assume that you are using the state module. `echo-request` and `time-exceeded` do need special consideration, however.

### ECHO REQUEST (TYPE 8) AND ECHO REPLY (TYPE 0) MESSAGES

`ping` uses two ICMP message types. The request message, `echo-request`, is message Type 8. The reply message, `echo-reply`, is message Type 0. `echo-request` messages are not forwarded into the LAN from anywhere. External `echo-request` to the choke are allowed from only the gateway firewall:

```bash
$IPT -A INPUT         -i $OM2_INTERFACE -p icmp --icmp-type echo-request \
             -s $GATEWAY_IPADDR -j ACCEPT
```

Some sites might choose to block outgoing `echo-reply` messages even if incoming `echo-request` messages are dropped. Some trojans, such as `loki`, use unsolicited `echo-reply` messages to carry covert login sessions in the packets' data area from your local hosts to remote servers:

```bash
$IPT -A OUTPUT        -o $OM2_INTERFACE -p icmp --icmp-type echo-reply \
             -d $GATEWAY_IPADDR -j ACCEPT
$IPT -A FORWARD       -o $OM2_INTERFACE -p icmp --icmp-type echo-reply -j DROP
```

### TIME EXCEEDED STATUS (TYPE 11) MESSAGES

ICMP message Type 11, `time-exceeded`, indicates a timeout condition—or, more accurately, that a packet's maximum hop count has been exceeded. On networks today, `time-exceeded` is mostly seen as the ICMP response to a `traceroute` request.

Many people use `traceroute` to pinpoint a problem in the network. Additionally, `traceroute` is useful in network mapping and locating critical gateways. Whether or not you choose to use `traceroute`, it's a good idea to block outgoing `time-exceeded` messages. There are few legitimate reasons for someone to map your internal network, and plenty of hostile reasons to do so. It should be noted that some versions of traceroute, notably those on `*nix` platforms, use UDP as the transport mechanism rather than ICMP.

If you need to allow any kind of incoming UDP traffic on the unprivileged ports, it's easier and more effective to block your outgoing response than it is to try to block the incoming requests. **traceroute** starts at UDP port 33434, by default, but the base port is settable by command-line option and optionally can use ICMP **echo-request** rather than UDP as well.

```bash
$IPT -A OUTPUT -o $DN_Z_INTERFACE -p icmp --icmp-type time-exceeded -j DROP
$IPT -A FORWARD -o $DN_Z_INTERFACE -p icmp --icmp-type time-exceeded -j DROP
```

If new incoming UDP packets are dropped by default, your system won't return the ICMP Type 3 **port-unreachable** message that endpoint hosts return.

## Enabling DNS (UDP/TCP Port 53)

DNS relies on both UDP and TCP. Connection modes include regular client-to-server connections, server-to-server lookup traffic, and DNS zone transfers.

It's unlikely that a residential site will host public DNS service or pay the fee to have a top-level public pointer to its name server, though Dynamic DNS services are changing this paradigm. Smaller businesses may or may not do so. It's common to hire a DNS service or to have the service provided by the ISP or ASP. Larger organizations usually do host publicly accessible name servers, as well as run local, private name servers internally.

### CLASSIC DNS SETUP FOR A LAN

Some sites need the additional sense of security that comes with a classic DNS setup that hides local hosts—security through obscurity, if you will. The attraction of this setup is that sensitive, local, personal, and account information can be centrally stored in the internal DNS database.

The idea is that a publicly visible host runs its own DNS server for the public. The server is configured as the authoritative source for the site, but the information is incomplete. The public name server knows nothing about internal machines. DNS clients on the public name server machine, if any, possibly don't use the local name server. Instead, `/etc/resolv.conf` on the public server points to an internal, private machine as the name server for the local clients. Incoming queries from the Internet are handled by the public DNS server. Local queries are handled by the internal DNS server.

The internal server is also configured as the authoritative source for the site. In this case, the information is correct. Local queries, possibly queries from the public server's local clients, and queries from the private LAN are all handled by this internal, private DNS server. As shown in Figure 6.6, when the local server doesn't have the requested lookup information, it queries the public server, which, in turn, forwards the query to an external name server.
