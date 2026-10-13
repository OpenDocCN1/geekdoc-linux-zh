# FIGURE 12-6

A special route for a specific network device

![](bbox=[0.35, 0.18, 0.82, 0.68])

When applied, it writes a route-eth0 file in the /etc/sysconfig/network-scripts directory. The following is the complete contents of that file:

```
ADDRESS0=192.168.0.0

NETMASK0=255.255.255.0

GATEWAY0=192.168.122.1
```

When the network service is restarted, it's applied to the routing table. Based on the previously configured routing table, the following is the result:

| Destination | Gateway | Genmask | Flags | Metric | Ref | Use | Iface |
|---|---|---|---|---|---|---|---|
| 192.168.0.0 | 192.168.122.1 | 255.255.255.0 | UG | 0 | 0 | 0 | eth0 |
| 192.168.122.0 | 0.0.0.0 | 255.255.255.0 | U | 1 | 0 | 0 | eth0 |
| 0.0.0.0 | 192.168.122.1 | 0.0.0.0 | UG | 0 | 0 | 0 | eth0 |