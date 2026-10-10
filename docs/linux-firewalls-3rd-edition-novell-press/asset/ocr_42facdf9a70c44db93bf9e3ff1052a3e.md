define a **DNS_SERVER** constant, and the DMZ servers use the standard DNS client/server protocols:

```
# DNS name server (53) - requests to remote servers
# ----------------------------------------------------

$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p udp \\
    -s $DNS_SERVER --sport $UNPRIVPORTS --dport 53 \\
    -m state --state NEW -j ACCEPT

$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \\
    -s $DNS_SERVER --sport $UNPRIVPORTS --dport 53 \\
    -m state --state NEW -j ACCEPT
```

```
# DNS name server (53) - requests from remote clients
# -------------------------------------------------------

$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p udp \\
    --sport $UNPRIVPORTS -d $DNS_SERVER --dport 53 \\
    -m state --state NEW -j ACCEPT

$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \\
    --sport $UNPRIVPORTS -d $DNS_SERVER --dport 53 \\
    -m state --state NEW -j ACCEPT
```

Naturally, the single pair of generic rules is required to forward **ESTABLISHED** and **RELATED** traffic.

# CHOKE DMZ CONFIGURATION AS A PRIVATE NAME SERVER

The choke hosts the private name server in this example. (The server, or servers, could just as easily run in the LAN itself or in a separate local server network.) LAN clients use the private name server. If the choke server can't service a query from its DNS cache, it forwards the request to the public server running in the DMZ.

The private DNS server receives client queries from the client programs running on machines in the LAN. In this example, requests from DMZ clients go to the private server so that they have access to DNS information about LAN clients:

```
# DNS LAN clients to private server (53)
# --------------------------------------

$IPT -A INPUT -i $LAN_INTERFACE -p udp \\
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \\
    -d $LAN_IPADDR --dport 53 \\
    -m state --state NEW -j ACCEPT
```