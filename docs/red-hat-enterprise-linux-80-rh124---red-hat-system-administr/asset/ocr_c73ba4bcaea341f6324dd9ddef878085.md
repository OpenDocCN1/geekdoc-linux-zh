# 6. Display and activate the connection.

6.1. View all connections.

```
[student@servera ~]$ nmcli con show
NAME UUID TYPE DEVICE
ens3 884a490d-694c-4e5c-a672-01b0826a966e ethernet -
static-ens3 15aaa901-555d-40cb-94c6-cea6f9151634 ethernet -
Wired connection 1 9b531978-64e7-d32c-a574-38d723c7c8dc ethernet
```

# 6.2. View the active connection.

```
[student@servera ~]$ nmcli con --active
ens3 884a490d-694c-4e5c-a672-01b0826a966e ethernet ens3
```

# 6.3. Activate the static-ens3 connection.

```
[student@servera ~]$ sudo nmcli con up "static-ens3"
Connection successfully activated (D-Bus path: /org/freedesktop/NetworkManager/ActiveConnection/3)
```

# 6.4. Verify the active connection.

```
[student@servera ~]$ nmcli con show --active
NAME UUID TYPE DEVICE
static-ens3 15aaa901-555d-40cb-94c6-cea6f9151634 ethernet ens3
```

# 7. Test connectivity using the new network addresses.

7.1. Verify the IP address.

```
[student@servera ~]$ ip addr show ens3
2: ens3<BROADCAST, MULTICAST, LOWER_UP mtu 1500 qdisc fq_codel state UP default qlen 1000
link/ether 52:00:00:fa0:a0 ff:ff:ff:ff:ff:ff
 inet 172.25.250/24 brd 172.25.255 global noprefixroute ens3
 valid forever preferred_lift forever
inet6 fe80::6556:0cd9:ce15:1484/64 scope link6
 valid forever preferred_lift forever
```

# 7.2. Verify the default gateway.

```
[student@servera ~]$ ip route
deault via 172.25.250.254 dev ens3 proto kernel scope src 172.25.250.10 metric 100
```

# 7.3. Ping the DNS address.

```
[student@servera ~]$ ping -c 3 172.25.250.254
PING 172.25.250.254 (172.25.250.254) 56(84) bytes of data.
```