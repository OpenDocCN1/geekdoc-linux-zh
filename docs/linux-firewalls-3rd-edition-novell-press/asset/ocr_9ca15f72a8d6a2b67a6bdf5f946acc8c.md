```
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PREROUTING ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
if [ "$1" = "stop" ]
then
echo "Firewall completely stopped! WARNING: THIS HOST HAS NO FIREWALL RUNNING."
exit 0
fi
```

```
# Unlimited traffic on the loopback interface
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT
```

```
# Set the default policy to drop
$IPT --policy INPUT DROP
$IPT --policy OUTPUT DROP
$IPT --policy FORWARD DROP
$IPT -t nat --policy PREROUTING DROP
$IPT -t nat --policy OUTPUT DROP
$IPT -t nat --policy POSTROUTING DROP
$IPT -t mangle --policy PREROUTING DROP
$IPT -t mangle --policy OUTPUT DROP
```

```
# Create the user-defined chains
for i in $USER_CHAINS; do
    $IPT -N $i
done
```

```
#######################################################
# DNS Caching Name Server (query to remote, primary server)
$IPT -A EXT-output -p udp --sport 53 --dport 53 \
    -j local-dns-server-query
$IPT -A EXT-input -p udp --sport 53 --dport 53 \
    -j remote-dns-server-response
# DNS Caching Name Server (query to remote server over TCP)
$IPT -A EXT-output -p tcp \
    --sport SUNPRIVPORTS --dport 53 \
    -j local-dns-server-query
```