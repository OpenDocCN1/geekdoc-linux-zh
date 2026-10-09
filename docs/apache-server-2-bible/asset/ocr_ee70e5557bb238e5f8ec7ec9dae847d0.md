Here’s what’s going on in the preceding configuration:

+   * The first line starts a DNS record called the Start of Address (SOA), which specifies the serial number, refresh rate, retry rate, expiration time, and time-to-live (TTL) values.

+   * The serial number is used by DNS servers to determine whether or not they need to update their cached records. For example, the given example is set to 20011201001, which states that the last update was on 12/01/2001 and it is the first (001) change in that day. Now if the DNS administrator changed the DNS configuration on 12/02/2001 the serial number should be changed to reflect that, so that any remote DNS server that has cached the records can compare the serial numbers between the cached version and the new version and decide whether to upload new DNS data.

+   * The refresh rate says how often should the records be refreshed by the DNS server.

+   * The retry value states that in case of a failure the remote DNS server quering this DNS server retry again at the given interval.

+   * The expiration time tells remote DNS servers to forcefully expire any cached data they have on the given domain after specified number of days.

+   * The final entry in SOA states that records have a specified minimal time-to-live value. Note that anything following a semi-colon is treated as a comment line and ignored.

+   * The next two noncomment lines state that the DNS servers responsible for the newdomain.com are ns1.domain.com and ns2.domain.com. If you do not have a second DNS server, you should consider using a third-party secondary DNS service such as http://www.secondary.com.

# Setting up DNS for new virtual hosts

You can set up DNS for each new virtual host on Linux as follows:

+   1. Create a zone file for the new domain. (See the preceding section for more on zone files.)

+   2. In the /etc/named.conf file, add the following lines to enable the newdomain zone.

```
zone "newdomain.com" IN {
    type master;
    file "newdomain.zone";
    allow-update { none; };
};
```

This tells the named (DNS daemon) that the zone file for newdomain.com is /var/named/newdomain.zone and that it is the primary (master) DNS server for this zone.