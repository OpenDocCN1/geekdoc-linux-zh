Listing 20.2 shows a shell script that sets up a basic one-way packet-filtering and masquerading firewall using ipchains.

# **LISTING 20.2   A Basic Firewall Using ipchains**

```
#!/bin/sh -x
# To enable logging if necessary
#LOG=-l

# Constants
ANYWHERE=0.0.0.0/0
EXT_IF=eth0
INT_IF=eth1

# Networks
INTERNAL_NET=10.0.1.0/24
EXTERNAL_ADDR=205.142.24.1/32

# Disable packet forwarding while we set up the firewall
echo 0 > /proc/sys/net/ipv4/ip_forward

# Flush all rules
/sbin/ipchains -F input
/sbin/ipchains -F output
/sbin/ipchains -F forward

# Deny all packets by default - this is a mostly-closed firewall
/sbin/ipchains -P input DENY
/sbin/ipchains -P output DENY
/sbin/ipchains -P forward DENY

# Accept anything to/from localhost
/sbin/ipchains -A input -j ACCEPT -p all -s localhost -d localhost -i lo \\
SLOG
/sbin/ipchains -A output -j ACCEPT -p all -s localhost -d localhost -i lo \\
SLOG

# Spoofing protection - deny anything coming from the outside with an \\
internal
# address
/sbin/ipchains -A input -j RETURN -p all -s $INTERNAL_NET -d $ANYWHERE -I \\
$EXT_IF $LOG

# Accept TCP packets belonging to already-established connections
/sbin/ipchains -A input -j ACCEPT -p tcp -s $ANYWHERE -d
$ME -i $EXT_IF |.y $LOG

# Accept and masquerade all packets from the inside going anywhere
/sbin/ipchains -A input -j ACCEPT -p all -s $INTERNAL_NET -d $ANYWHERE -I \\
$INT_IF $LOG
```