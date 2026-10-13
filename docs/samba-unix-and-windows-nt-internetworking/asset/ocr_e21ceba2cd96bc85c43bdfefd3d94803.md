<21> RAS client

<BE> Network monitor agent

<BF> Network monitor utility

# Group Resource Type

<1C> Domain group name

<1D> Master browser name

<1E> Group name for elections

<20> Internet group

In the NetBIOS over TCP/IP (NBT) world supported by Samba, NetBIOS names are registered and resolved in one of three ways. The first and simplest method is to use a host table that manually maps NetBIOS names to IP addresses. This table is affectionately known as the LAN Manager Hosts (LMHOSTS) table. Each line in the LMHOSTS table matches a NetBIOS resource name to its home IP address (Example 8.2).

# Example 8.2 Sample Windows LMHOSTS Table

```
149.110.5.12    Wizard    #PRE    #DOM:EYRIE
149.110.5.11    Dragon
149.110.5.2     Dhyana
149.110.5.1     Tao
149.110.5.5     Rose
```

The second method registers and resolves NetBIOS names using network broadcasts (Figure 8.1). To make its presence known, a machine broadcasts its name over the network on UDP port 137. This usually occurs at system boot time when network services are starting. The machine then awaits a response indicating whether its chosen name is accepted or rejected as being already in use by another machine (Figure 8.2). The process may be repeated a number of times, because broadcast delivery is not guaranteed. Upon successful registration, the NetBIOS name and address are cached in a collaborative manner by the workgroup of machines. NetBIOS name resolution queries are handled in a similar fashion. This method can break down quickly on large, complex networks due to routing problems and/or heavy broadcast traffic.