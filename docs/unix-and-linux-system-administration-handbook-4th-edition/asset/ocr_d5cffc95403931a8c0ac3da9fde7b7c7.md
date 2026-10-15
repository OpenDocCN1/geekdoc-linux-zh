Instead of just waiting passively for slave servers to time out, master servers for BIND (always) and NSD (if so configured) notify their slaves every time a zone changes. It’s possible for an update notification to be lost because of network congestion, so the refresh timeout should still be set to a reasonable value.

If a slave server tries to check the master’s serial number but the master does not respond, the slave tries again after the retry timeout period has elapsed. Our experience suggests that 20–60 minutes (1,200–3,600 seconds) is a good value.

If a master server is down for a long time, slaves will try to refresh their data many times but always fail. Each slave should eventually decide that the master is never coming back and that its data is surely out of date. The expire parameter determines how long the slaves will continue to serve the domain’s data authoritatively in the absence of a master. The system should be able to survive if the master server is down for a few days, so this parameter should have a longish value. We recommend a week to a month or two.

The minimum parameter in the SOA record sets the time to live for negative answers that are cached. The default for positive answers (i.e., actual records) is specified at the top of the zone file with the $TTL directive. Experience suggests values of several hours to a few days for $TTL and an hour to a few hours for the minimum. BIND silently discards any minimum values greater than 3 hours.

The $TTL, expire, and minimum parameters eventually force everyone that uses DNS to discard old data values. The initial design of DNS relied on the fact that host data was relatively stable and did not change often. However, DHCP, mobile hosts, and the Internet explosion have changed the rules. Name servers are desperately trying to cope with the dynamic update and incremental zone transfer mechanisms described later. For more information about TTLs, see page 576.

# NS records

NS (name server) records identify the servers that are authoritative for a zone (that is, all the master and slave servers) and delegate subdomains to other organizations. NS records are usually placed directly after the zone’s SOA record.

The format is

```
zone [ttl] [IN] NS hostname
```

For example:

```
NS ns1.atrust.com.
NS ns2.atrust.com.
booklab NS ubuntu.booklab.atrust.com.
NS ns1.atrust.com.
```

The first two lines define name servers for the atrust.com domain. No name is listed because it is the same as the name field of the SOA record that precedes the records; the name can therefore be left blank. The class is also not listed because IN is the default and does not need to be stated explicitly.

> NS records are specified in RFC1035 (1987).