When we ping the database server, which is the host telesto, we get the following output:

```
PING telesto.raleigh.ibm.com (9.27.175.24) from 9.27.175.25 : 56(84) bytes of data.
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=1 ttl=64 time=1.96 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=2 ttl=64 time=0.384 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=3 ttl=64 time=0.448 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=4 ttl=64 time=5.61 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=5 ttl=64 time=0.382 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=6 ttl=64 time=0.389 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=7 ttl=64 time=0.677 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=8 ttl=64 time=0.356 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=9 ttl=64 time=1.99 ms
64 bytes from telesto.raleigh.ibm.com (9.27.175.24):icmp_seq=10 ttl=64 time=1.19 ms
```

Comparing the turnaround time for both outputs, it is clear that something is not right with the connection to the database server. To investigate the cause of this problem, the recommended approach is to try first from the lowest level—hardware, connections, NIC, and network drivers—before even going into tuning the TCP/IP stack. An important question to ask is “What speed and duplex are being used by the database server’s network card?”

To determine the speed and duplex of the database server’s network card, we log on to the database server and issue the command mii-tool. Unfortunately, the mii-tool on the database server fails with the following message:

```
SIOCGETMIIPHY on `eth0' failed: Operation not supported
```

A tool that is useful when the mii-tool does not work is ethtool. We issue ethtool on the database server (we know that eth0 is the interface that we are using on this server) as follows:

```
# ethtool eth0
```

Output from ethtool follows:

```
Settings for eth0:
  Supported ports: [ TP ]
  Supported link modes: 10baseT/Half 10baseT/Full
                       100baseT/Half 100baseT/Full
                       1000baseT/Full
  Supports auto-negotiation: Yes
  Advertised link modes: 10baseT/Half 10baseT/Full
                        100baseT/Half 100baseT/Full
                        1000baseT/Full
  Advertised auto-negotiation: Yes
  Speed: 10Mb/s
  Duplex: Half
```