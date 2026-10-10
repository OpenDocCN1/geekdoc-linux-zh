# Network Services 259

# EXERCISE 9.1: Making a Name Server Authoritative

In this exercise, you will learn how to make a secondary name server authoritative for a domain for a server running Bind 9 as you are about to decommission the existing primary name server.

+   1. In the `named.conf` file on the secondary server, check to see whether it is designated as the secondary for the zone you are interested in.

+   2. Change `type secondary` to `type master`.

+   3. Change the `allow update` option to `none`.

+   4. Power down the master server and then reboot the server you have just changed to master.

+   5. This new server should now be authoritative for this domain.  ▪

# Network Time Protocol

NTP is the defined protocol for synchronizing clocks of computer systems over a network, including the Internet. There are many time servers located across the world, and the source can be an atomic clock or via a satellite receiver. The accuracy that is obtained is very good and is typically no more than a few milliseconds. Like DNS servers, there is a hierarchy with primary or Stratum 1 timeservers and secondary or Stratum 2 servers. Those servers at a lower level always synchronize themselves to a server at a higher level. There are a number of public timeservers available, and those operated by the National Institute of Science and Technology (NIST) and US Naval Observatory (USNO) within the United States are particularly reliable.

Within the Linux system, there is an NTP client which is implemented as a continuously running daemon process. This process runs in the kernel space due to the sensitivity of timing.

The main configuration file for NTP is /etc/ntp.conf, and the servers you will synchronize to, as well as what networks are allowed to synchronize to your server, are described. You need to define a number of servers to synchronize to ensure there is redundancy in case of network or server failures. To specify a pair of servers to synchronize to, the ntp.conf will need to be modified as such:

```
server lerc-dns.lerc.nasa.gov # Stratem 1 server
server ntp.time.edu           # Stratem 2 server
```

You must then restrict the access that you allow these time servers; for instance, you do not want them to query your NTP server.