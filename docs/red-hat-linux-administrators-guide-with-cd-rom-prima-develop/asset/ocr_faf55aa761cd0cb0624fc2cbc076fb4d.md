```
echo "Done!"
```

```
# ------------------------------------------- Basic
```

```
Services - echo -n "Services.."
```

```
#ftp-data (20) and ftp (21)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 20 -j ACCEPT
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 21 -j ACCEPT
echo -n ".."
#ssh (22)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 22 -j ACCEPT
echo -n ".."
#telnet (23)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 23 -j ACCEPT
echo -n ".."
#smtp (25)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 25 -j ACCEPT
echo -n ".."
# DNS (53)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 53 -j ACCEPT
$IPCHAINS -A input -p udp -s $REMOTENET -d $LOCALNET 53 -j ACCEPT
echo -n ".."
```

```
# DHCP on LAN side (67/68)
# $IPCHAINS -A input -i $INTERNALIF -p udp -s $REMOTENET
-d 255.255.255.255/24 67 -j ACCEPT
# $IPCHAINS -A output -i $INTERNALIF -p udp -s $REMOTENET
-d 255.255.255.255/24 68 -j ACCEPT
# echo -n ".."
```

```
#http (80)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 80 -j ACCEPT
echo -n ".."
#POP-3 (110)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 110 -j ACCEPT
echo -n ".."
```

```
#identd (113)
$IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 113 -j ACCEPT
echo -n ".."
# nntp (119)
# $IPCHAINS -A input -p tcp -s $REMOTENET -d $LOCALNET 119
```