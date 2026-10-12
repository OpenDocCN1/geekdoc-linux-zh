```
# don't masquerade internal-internal traffic
$IPCHAINS -A forward -s $INTERNALNET -d $INTERNALNET -j ACCEPT
echo -n "."
# don't Masquerade external interface direct
$IPCHAINS -A forward -s $LOCALNET -d $REMOTEIN -j ACCEPT
echo -n "."
```

```
# masquerade all internal IPs going outside
$IPCHAINS -A forward -s $INTERNALNET -d $REMOTEIN -j MASQ
echo -n "."
# set Default rule on MASQ chain to Deny
$IPCHAINS -P forward DENY
echo -n "."
```

```
# Allow all connections from the network to the outside
$IPCHAINS -A input -s $INTERNALNET -d $REMOTEIN -j ACCEPT
$IPCHAINS -A output -s $INTERNALNET -d $REMOTEIN -j ACCEPT
echo -n ".." 
    echo "Done!"
# -----------Set telnet, www and FTP for minimum delay --
# This section manipulates the Type Of Service (TOS) bits of the
# packet. For this to work, you must have
# CONFIG_IP_ROUTE_TOS enabled in your kernel
echo -n "TOS flags.."
$IPCHAINS -A output -p tcp -d 0/0 www -t 0x01 0x10
$IPCHAINS -A output -p tcp -d 0/0 telnet -t 0x01 0x10
$IPCHAINS -A output -p tcp -d 0/0 ftp -t 0x01 0x10
echo -n ".."
```

```
# Set ftp-data for maximum throughput:
$IPCHAINS -A output -p tcp -d 0/0 ftp-data -t 0x01 0x08
echo -n ".." 
    echo "Done!"
```

```
# Trusted Networks -
# Add in any rules that specifically allow connections from
# hosts/nets that would otherwise be blocked.
# echo -n "Trusted Networks.."
```