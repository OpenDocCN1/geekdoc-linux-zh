# 20.2 BIND (DNS) in a Cluster

One of the most recognizable components of TCP/IP (or the Internet in general) is the Domain Name System (DNS). The most common DNS option in use today is the ubiquitous Berkeley Internet Name Domain (BIND). You will see it everywhere you turn due to the common World Wide Web identifiers in many advertisements today (i.e., www.bruden.com). As you may know, BIND is just a scalable scheme to provide the ability to translate node names (whatz.ting.ugot.com) into IP addresses (193.12.23.45) or vice versa. To make a very long story very short, BIND is implemented through a series of servers that provide addressing information to other servers and ultimately to a client.

Your cluster can be configured to run as a BIND server, a BIND client, or both. If you configure the cluster as a BIND server, only one member actually does the serving (the first server will typically be the member on which you ran the bindconfig(8) or "sysman dns" command). This will be the only member running the BIND server daemon (appropriately named named(8)). The named daemon is implemented as a CAA resource; so in the case of member failure, another member will take over the server responsibilities. Remember, only one member at a time is actually doing the serving.

```
# caa_stat -t named
Name        Type        Target    State    Host
------------------------------------------------
named       application ONLINE    ONLINE   molari
```

The other BIND servers (and clients) should reference the default cluster alias to identify the name of the BIND server in their /etc/resolv.conf file (which is cluster-wide).

# 20.3 DHCP in a Cluster

The Dynamic Host Configuration Protocol (DHCP) provides a mechanism whereby a system can be presented with an IP address dynamically. This is usually (but not necessarily) done at boot time. If you have a DSL connection to the Network, you are probably getting an IP address through DHCP sent to your PC as you boot it. The address is probably different each time you boot.

The cluster cannot function as a DHCP client because clusters require static addresses, but it can function as a DHCP server. The server will have access to a database that identifies the pool of IP addresses to be loaned out and identifies the legitimate clients. The cluster will function as a DHCP server and also provide failover capabilities through CAA.

```
# caa_stat -t dhcp
Name        Type        Target    State    Host
------------------------------------------------
dhcp        application ONLINE    ONLINE   sheridan
```