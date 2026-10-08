# 20.10 Secondary name servers

For reasons of safety against failures, at least two name servers should be operated in each zone. In the event of the failure of one computer, the second name server can still answer all requests. To keep the data consistent at any time, only one (authorized) master server must exist per zone.

Besides this, one or more secondary name servers may be configured. a secondary name server fetches its data from the primary server. If this is not available, the data stored in backup copies (*.bak) is used. If the life cycle of the data has expired, an attempt is made to fetch this data afresh from a primary server. Listing 20.17 shows an example of the file /etc/named.conf for a secondary name server.

```
zone "example.org" {
  type slave;
  masters { 192.168.3.150 };
  file "named.bak"
}
nzone "168.192.in-addr.arpa {
  type slave;
  masters { 192.168.3.150 };
  file "named.rev.bak"
}
```

Listing 20.17 The file /etc/named.conf for a secondary name server.

On the basis of the serial numbers registered in the SOA records data, a secondary name server can determine whether it has the current data of a zone. If not, a new transfer is triggered. If you specify a smaller serial number in the primary data, the secondary name server will react with an appropriate message. You should therefore keep an eye on the system log entries of all name servers to exclude this kind of error. Otherwise, secondary servers are completely maintenance-free.

# 20.11 Slave name servers

A slave server does not manage zone-related data, but only a cache, and forwards requests that cannot be answered on the basis of the cache contents to specific name servers (forwarders). This allows this computer to build up a good cache from which all users can benefit.