
Subnetting is a local extension to the network address part of the local IP addresses. A local network mask is defined as one that treats some of the most significant host address bits as if they were part of the network address. These additional network address bits serve to define multiple networks locally. Remote sites are not aware of local subnets. They see the address range as normal Class A, B, or C addresses.

For example, let's take the Class C private address block, 192.168.1.0. The base address, known as the network address, is 192.168.1.0 for this example. The network mask for this example is 255.255.255.0, exactly matching the first 24 bits, the network address, of the 192.168.1.0/24 network.

This network can be divided into two local networks by defining the first 25 bits, rather than the first 24 bits, as the network portion of the address. In current parlance, we say that the local network has a prefix length of 25 rather than 24. The most significant bit of the host address field is now treated as part of the network address field. The host field now contains 7 bits rather than 8. The network mask becomes 255.255.255.128, or /25 in CIDR notation. Two subnetworks are defined: 192.168.1.0, addressing hosts from 1 to 126, and 192.168.1.128, addressing hosts from 129 to 254. Each subnet loses two host addresses because each subnet uses the lowest host address, 0 or 128, as the network address, and uses the highest host address, 127 or 255, as the broadcast address. Table 6.2 shows this in tabular form.

**TABLE 6.2**
Class C Network 192.168.1.0 Subnetted into Two Subnets

| SUBNET NUMBER | NONE | 0 | 1 |
|---|---|---|---|
| Network Address | 192.168.1.0 | 192.168.1.0 | 192.168.1.128 |
| Network Mask | 255.255.255.0 | 255.255.255.128 | 255.255.255.128 |
| First Host Address | 192.168.1.1 | 192.168.1.1 | 192.168.1.129 |
| Last Host Address | 192.168.1.254 | 192.168.1.126 | 192.168.1.254 |
| Broadcast Address | 192.168.1.255 | 192.168.1.127 | 192.168.1.255 |
| Total Hosts | 254 | 126 | 126 |

Subnetworks 192.168.1.0 and 192.168.1.128 can be assigned to two separate internal network interface cards. Each subnet consists of two independent networks, each containing up to 126 hosts.

Subnetting allows for the creation of multiple internal networks, each containing different classes of client or server machines and each with its own independent routing. Different firewall policies can then be applied to the networks.

Of course, this example showed the network being divided into two portions. The network can in fact be divided into many parts in order to create a number of smaller networks. It’s quite common to see a network with a subnet mask of 255.255.255.252 or /30 used between routers at two locations. Table 6.3 takes the process one step further and shows the same network divided into four subnets.

**TABLE 6.3**
Class C Network 192.168.1.0 Subnetted into Four Subnets

| | 0 | 1 | 2 | 3 |
| :--- | :--- | :--- | :--- | :--- |
| **Network Address** | 192.168.1.0 | 192.168.1.64 | 192.168.1.128 | 192.168.1.192 |
| **Network Mask** | 255.255.255.192 | 255.255.255.192 | 255.255.255.192 | 255.255.255.192 |
| **First Host Address** | 192.168.1.1 | 192.168.1.65 | 192.168.1.129 | 192.168.1.193 |
| **Last Host Address** | 192.168.1.62 | 192.168.1.126 | 192.168.1.190 | 192.168.1.254 |
| **Broadcast Address** | 192.168.1.63 | 192.168.1.127 | 192.168.1.191 | 192.168.1.255 |
| **Total Hosts** | 62 | 62 | 62 | 62 |

### Selective Internal Access by Host, Address Range, or Port

Traffic through a firewall machine’s internal interface can be selectively limited, just as traffic through the external interface is. For example, on a firewall for a small, residential site, rather than letting everything through on the internal interface, traffic could be limited to DNS, SMTP, POP, and HTTP. In this case, let’s say that a firewall machine provides these services for the LAN. Local machines are not allowed any other access to outside services. In this case, forwarding isn’t done.

#### POINT OF INTEREST

> In this example, local hosts are limited to the specific services: DNS, SMTP, POP, and HTTP. Because POP is a local mail-retrieval service in this case, and because DNS, SMTP, and HTTP are proxied services, no direct Internet access is being made by LAN clients. In each case, the local clients are connecting to local servers. POP is a local LAN service. The three other servers establish remote connections on the client’s behalf.

This example would be used only by a small, likely residential, site. Placing the mail gateway and POP services on the firewall host can require the host to have user accounts. It is not necessary that these accounts be login accounts, however.

## CONFIGURATION OPTIONS FOR AN INTERNAL LAN

The following example considers a firewall machine with an internal interface connected to a LAN. Constants for the internal interface are as shown here:

```
LAN_INTERFACE="eth1"     # internal interface to the LAN
LAN_GATEWAY="192.168.1.1"    # firewall machine's internal
                              # interface address
LAN_ADDRESSES="192.168.1.0/24"    # range of addresses used on the LAN
```

LAN machines point to the firewall machine's internal interface as their name server:

```
# Generic gateway response rule
$IPT -A OUTPUT -o $LAN_INTERFACE \
    -s $LAN_GATEWAY \
    -d $LAN_ADDRESSES --dport $UNPRIVPORTS \
    -m state --state ESTABLISHED,RELATED -j ACCEPT
```

```
# Service-specific LAN request rules
```

```
$IPT -A INPUT -i $LAN_INTERFACE -p udp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $LAN_GATEWAY --dport 53 \
    -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $LAN_GATEWAY --dport 53 \
    -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

LAN machines also point to the firewall as their SMTP and POP server:

```
# Sending mail - SMTP
$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $GATEWAY --dport 25 \
    -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```
# Receiving Mail - POP
$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $GATEWAY --dport 110 \
    -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

The sendmail server will initiate an AUTH lookup request to the mail client. You won't likely be running the AUTH daemon, but you can send a REJECT for AUTH requests which can, on certain mail configurations, prevent a delay:

```
$IPT -A OUTPUT -o $LAN_INTERFACE -p tcp \
    -s $GATEWAY --sport $UNPRIVPORTS \
    -d $LAN_ADDRESSES --dport 113 -j REJECT
```

```
$IPT -A INPUT -i $LAN_INTERFACE ! --syn -p tcp \
    -s $LAN_ADDRESSES --sport 113 \
    -d $GATEWAY --dport $UNPRIVPORTS -j REJECT
```

Finally, a local web caching proxy server is running on the firewall machine on port 8080. Internal machines point to the web server on the firewall as their proxy, and the web server forwards any outgoing requests on their behalf, along with caching any pages retrieved from the Internet. All connections to the proxy are via port 8080. Secure web and FTP access to remote sites is initiated by the proxy server:

```
$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $GATEWAY --dport 8080 \
    -m state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

Remember that the web server will use the FTP passive mode protocol to retrieve data from remote FTP sites. The firewall's external interface will need input and output rules to access remote FTP, HTTP, and HTTPS service ports. The gateway host must also have rules for the external interface to account for email and local DNS queries to remote hosts.

## CONFIGURATION OPTIONS FOR MULTIPLE LANS

Adding a second internal LAN allows this example to be developed further. The next example can be better secured than the preceding example. As shown in Figure 6.5, the DNS, SMTP, POP, and HTTP services are offered from server machines in a second LAN rather than from the firewall machine. The second LAN may or may not serve as a public DMZ. It's equally possible that the second LAN represents an internal service LAN, and its services are not offered to the Internet (although, in that case, the firewall could be required to at least be a mail gateway, depending on the local firewall configuration). In either case, firewall hosts do not typically host services. In this example, traffic is routed between the two LANS by the internal interfaces on the firewall machine.
