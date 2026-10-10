```
www IN A 123.45.67.3
ft p IN A 123.45.67.4

: Private clients on the LAN
red IN A 10.0.0.2
blue IN A 10.0.0.3
green IN A 10.0.0.4
yellow IN A 10.0.0.5

: EOF
```

The zone file for your “inside” example.com contains resource records that include information about the zone. Your DNS server uses the TTL (time-to-live) record to tell name servers that store the information that you provide for this domain how long they can keep the information before they need to throw it out and get fresh information. The first value is the default for the entire zone, and the time is in seconds. So a value of 86,400 seconds indicates that a client that is using the information should obtain fresh records about this domain every 24 hours.

The SOA line identifies the start of authority for the domain. The at (@) sign represents the example.com. name — the dot (.) must appear at the end of the domain name. The dot represents the root server of the Internet. If you leave the dot off, your DNS server appends the domain name, so the DNS server will use the name example.com.com.example.com. The hostmaster.example.com string indicates the e-mail address of the person who is to receive e-mail regarding the domain. (The first dot changes to an @ sign, resulting in hostmaster@example.com). Other information regarding the SOA record is as follows:

+   ■ **Serial** — Start with any number here; if the zone records change, increase the serial number to alert other servers that they need to get fresh data about your domain.

> WARNING If you forget to increase the serial number after changing zone records, other servers that cache this data never pick up your changes. To help remember, use the date in the serial number. The number 2009042701 would be for April 27, 2009. The 01 represents the first change made on that day.

+   ■ **Refresh** — Defines how often the slave DNS server for the zone checks for changes. (Here, 28,800 seconds represents 8 hours.)

+   ■ **Retry** — If the slave can’t reach the master, it tries again after this retry interval. (Here, 14,400 seconds represents 4 hours.)

+   ■ **Expire** — If the slave can’t contact the master within the expire time (here, 3,600,000 seconds, or 1,000 hours), the slave discards the data.

+   ■ **Minimum** — Defines the cache time to live for negative answers. (Here, it’s 86,400 seconds, or 24 hours.)

The name server (NS) records define the name server that represent this zone. In this case, NS records define hosts with the names ns1 and ns2 in example.com. The MX record indicates the location of the mail server for the domain, so that the DNS server can direct e-mail to users in