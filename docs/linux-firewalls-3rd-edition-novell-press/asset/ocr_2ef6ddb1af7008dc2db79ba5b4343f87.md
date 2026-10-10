```
for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
    echo 1 > $f
done

# Log packets with impossible addresses.
for f in /proc/sys/net/ipv4/conf/*/log_martians; do
    echo 1 > $f
done

#---------------------------------------------------------------

# Remove any existing rules from all chains
$IPT --flush
$IPT -t nat --flush
$IPT -t mangle --flush
$IPT -X
$IPT -t nat -X
$IPT -t mangle -X
$IPT --policy INPUT  ACCEPT
$IPT --policy OUTPUT  ACCEPT
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PREROUTING  ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
if [ "$1" = "stop" ]
then
    echo 'Firewall completely stopped!  WARNING: THIS HOST HAS NO FIREWALL RUNNING.'
    exit 0
fi

# Unlimited traffic on the looopback interface
$IPT -A INPUT  -i SLOOPBACK_INTERFACE -j ACCEPT
$IPT -A OUTPUT -o SLOOPBACK_INTERFACE -j ACCEPT

# Set the default policy to drop
$IPT --policy INPUT REJECT
$IPT --policy OUTPUT REJECT
$IPT --policy FORWARD REJECT

#---------------------------------------------------------------

# Stealth Scans and TCP State Flags

# All of the bits are cleared
$IPT -A INPUT  -p tcp --tcp-flags ALL NONE -j DROP
$IPT -A FORWARD -p tcp --tcp-flags ALL NONE -j DROP
```