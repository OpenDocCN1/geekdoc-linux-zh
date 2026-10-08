
## Enabling Common UDP Services

causes the target system to return a Destination Unreachable message, indicating the end-point of the route to the host. By the default deny policy, the firewall being developed in this chapter blocks incoming UDP traceroute packets because traceroute default ports are not explicitly enabled. As a result, outgoing ICMP messages to incoming traceroute requests won't be sent. Table 7.13 lists the client/server connection protocol for the traceroute service.

### Table 7.13 traceroute Protocol

| Description | Protocol | Remote Address | Remote Port / ICMP Type | In/Out | Local Address | Local Port / ICMP Type |
| --- | --- | --- | --- | --- | --- | --- |
| Outgoing traceroute probe | UDP | ANYWHERE | 33434:33523 | Out | IPADDR | 32769:65535 |
| Time exceeded (intermediate hop) | ICMP | ANYWHERE | 11 | In | IPADDR | — |
| Port not found (termination) | UDP | ANYWHERE | 3 | In | IPADDR | — |
| Incoming traceroute probe | UDP | ISP | 32769:65535 | In | IPADDR | 33434:33523 |
| Time exceeded (intermediate hop) | ICMP | ISP | — | Out | IPADDR | 11 |
| Port not found (termination) | ICMP | ISP | — | Out | IPADDR | 3 |

traceroute can be configured to use any port or port range. As such, it's difficult to block all incoming traceroute packets by listing specific ports. However, it often uses source ports in the range from 32, 769 to 65, 535 and destination ports in the range from 33, 434 to 33, 523. Because traceroute can be configured to use any source and destination port, the most effective way to block traceroute is to block the outgoing ICMP messages generated in response. Symbolic constants are defined for traceroute's default source and destination ports:

```
TRACEROUT_SRC_PORTS="32769:65535"
TRACEROUT_DEST_PORTS="33434:33523"
```

### ENABLING OUTGOING traceroute REQUESTS

If you intend to use traceroute yourself, you must enable the UDP client ports. Note that you must allow incoming ICMP Time Exceeded and Destination Unreachable messages from anywhere for outgoing traceroute to work:

```
$IPT -A OUTPUT -o $INTERNET -p udp \
-s $IPADDR --sport $TRACEROUT_SRC_PORTS \
-dport $TRACEROUT_DEST_PORTS -j ACCEPT
```

Because traceroute is a less secure UDP service and can be used to identify your edge router, map your LAN, or attack other UDP services, allowing incoming traceroute isn't recommended.

## 7.6.2 Accessing Your ISP's DHCP Server
(UDP Ports 67, 68)

DHCP exchanges, if any, between your site and your ISP's server will necessarily be local client-to-remote server exchanges. Most often, DHCP clients receive temporary, or permanent, dynamically allocated IP addresses from a central server that manages the ISP's customer address space. The server also typically provides your local host with other configuration information, such as the network subnet mask; the network MTU; the default, first-hop router addresses; the domain name; and the default TTL.

If you have a dynamically allocated IP address from your ISP, you need to run a DHCP daemon on your machine. It's uncommon for bogus server messages to fly around your ISP's local subnet if someone runs the server by accident. For this reason, it's especially important to filter DHCP messages to limit traffic between your client and your specific ISP DHCP server as much as possible.

Table 7.14 lists the DHCP message type descriptions, as quoted from RFC 2131, "Dynamic Host Configuration Protocol."

### Table 7.14 DHCP Message Types

| DHCP Message | Description |
|---|---|
| DHCPDISCOVER | Client broadcast to locate available servers |
| DHCPOFFER | Server to client in response to DHCPDISCOVER with offer of configuration parameters |
| DHCPREQUEST | Client message to servers either (a) requesting offered parameters from one server and (b) declining offers from all others; (c) confirming receipt of previously allocated address after, for example, system reboot; or (d) extending the lease on a particular network address |
| DHCPACK | Server to client with configuration parameters, including committed network address |
| DHCPNAK | Server to client indicating that a network address is incorrect (for example, client has moved to new subnet) or client's lease has expired |
| DHCPDECLINE | Client to server indicating that network address is already in use |
| DHCPRELEASE | Client to server relinquishing network address and canceling remaining lease |
| DHCPINFORM | Client to server, asking only for local configuration parameters; client already has externally configured address |

In essence, when the DHCP client initializes, it broadcasts a DHCPDISCOVER query to discover any DHCP servers are available. Any servers receiving the query respond with a DHCPOFFER message indicating their willingness to function as server to this client; they include the configuration parameters that they have to offer. The client broadcasts a DHCPREQUEST message to accept one of the servers and to inform any remaining servers that it has chosen to decline their offers. The chosen server responds with a broadcast DHCPACK, indicating confirmation of the parameters that it originally offered. Address assignment is complete at this point. Periodically, the client sends a DHCPREQUEST message requesting a renewal on the IP address. If the lease is renewed, the server responds with a unicast DHCPACK message. Otherwise, the client falls back to the initialization process. Table 7.15 lists the complete client/server exchange protocol for the DHCP service.

### Table 7.15 DHCP Protocol

| Description | Protocol | Remote Address | Remote Port | In/Out | Local Address | Local Port |
|---|---|---|---|---|---|---|
| DHCPDISCOVER | UDP | 255.255.255.255 | 67 | Out | 0.0.0.0 | 68 |
| DHCPOFFER | UDP | DHCP SERVER | 67 | In | 255.255.255 | 68 |
| DHCPREQUEST | UDP | DHCP SERVER | 67 | Out | 0.0.0.0 | 68 |
| DHCPDECLINE | UDP | DHCP SERVER | 67 | In | ISP/NETMASK | 68 |
| DHCPACK | UDP | DHCP SERVER | 67 | In | IPADDR | 68 |
| DHCPREQUEST | UDP | DHCP SERVER | 67 | Out | IPADDR | 68 |
| DHCPRELEASE | UDP | | | | | | 68 |

The DHCP protocol is far more complicated than this brief summary, but the summary describes the essentials of the typical client and server exchange.

The following firewall rules allow communication between your DHCP client and a remote server:

```
DHCP_SERVER="my.dhcp.server" # if you use one

# Initialization or rebinding: No lease or Lease time expired.
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s BROADCAST_SRC --port 68 \
  -d BROADCAST_DEST --dport 67 -j ACCEPT

# Incoming DHCP OFFER from available DHCP servers
$IPT -A INPUT -i $INTERNET -p udp \
  -s BROADCAST_SRC --port 67 \
  -d BROADCAST_DEST --dport 68 -j ACCEPT

# Fall back to initialization
# The client knows its server, but has lost its lease,
# or else it needs to reconfirm the IP address after rebooting.
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s BROADCAST_SRC --port 68 \
  -d DHCP_SERVER --dport 67 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p udp \
  -s $DHCP_SERVER --port 67 \
  -d BROADCAST_DEST --dport 68 -j ACCEPT

# As a result of the above, we're supposed to change your IP
# address with this message, which is addressed to our new
# address before the DHCP client has received the update.
# Depending on the server implementation, the destination address
# can be the new IP address, the subnet address, or the limited
# broadcast address.

# If the network subnet address is used as the destination,
# the next rule must allow incoming packets destined to the
# subnet address, and the rule must precede any general rules
# that block including broadcasting packets.

# Lease renewal
$IPT -A OUTPUT -o $INTERNET -p udp \
  -s $IPADDR --port 68 \
  -d $DHCP_SERVER --dport 67 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p udp \
  -s $DHCP_SERVER --port 67 \
  -d $IPADDR --dport 68 -j ACCEPT
```

Notice that DHCP traffic cannot be completely limited to your DHCP server. During initialization sequences, when your client doesn't yet have an assigned IP address or even
