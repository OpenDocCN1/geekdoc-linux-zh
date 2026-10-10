This example would be used only by a small, likely residential, site. Placing the mail gateway and POP services on the firewall host can require the host to have user accounts. It is not necessary that these accounts be login accounts, however.

# CONFIGURATION OPTIONS FOR AN INTERNAL LAN

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
    -state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

LAN machines also point to the firewall as their SMTP and POP server:

```
# Sending mail - SMTP
$IPT -A INPUT -i $LAN_INTERFACE -p tcp \
    -s $LAN_ADDRESSES --sport $UNPRIVPORTS \
    -d $GATEWAY --dport 25 \
    -state --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

```
# Receiving Mail - POP
```