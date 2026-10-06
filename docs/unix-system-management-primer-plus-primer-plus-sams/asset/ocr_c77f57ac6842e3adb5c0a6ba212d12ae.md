For example, if you mistype the new IP address of a recently moved Web server in a zone with three-hour TTL, you fix the error five minutes later, caching name servers that asked for the address in those five minutes will hang onto that bad address for three hours. Even more frustrating is the fact that you have little control over the behavior of such caching servers.

The only control you have is the TTL of the zone in question. TTLs are between one and twenty-four hours, which is a long time to wait for changes to propagate. You could permanently set it to something small like five minutes, but may significantly increase traffic and load on your authoritative name servers and waste bandwidth.

The best solution in this case is to temporarily reduce the TTL to five minutes for the duration of your change and testing procedures. That way, you can back out any changes in a couple of minutes rather than a couple of hours. When testing, you can reset the TTL to your normal value.

The key to this is remembering that the TTL is part of the zone itself, so too will be cached; Therefore, any changes you make to the TTL must be at least one TTL length ahead of time. If the TTL is three hours, you should change its value at least three hours before you make your other changes so the new value is guaranteed to be seen by all caching servers. The TTL is stored in a zone's statement of authority (SOA); BIND 8.2 and higher require you to set a minimum TTL in the SOA and the $TTL directive which specifies the default TTL for all records, as shown in Listing 10.2.

# LISTING 10.2 A Typical SOA Record with a Default TTL of 3 Hours (10,800)

| $TTL | IN SOA ns1.example.com. hostmaster.example.com. |
| | 200203401 ; serial number (YYYYMMDDxx) |
| | 1800 ; refresh (30 min) |
| | 600 ; retry (10 min) |
| | 64800 ; expire (1 week) |
| | 600 ; Minimum TTL (10 min) |

# Using Redundant Mail Hubs

SMTP is another essential service, as it is responsible for sending, routing, and receiving email across the Internet. While mail agents like sendmail will queue outgoing messages on a mail hub for later delivery when destinations are unavailable, this queue is not infinite in size; mail will eventually be lost if the queued messages take up all available space on the mail hub.

An MX record, or mail exchange, is a DNS resource record that specifies where mail for a particular domain should be routed. Multiple MX records can be specified for one domain with varying priority levels to provide a simple form of redundancy. MX records with higher priority are preferred over ones with lower priorities. Lower priority MX records will be used only if the higher priority records are unavailable. Many administrators choose to use their ISP's hub as a lower priority MX record so mail has some place to go if their mail hub or network goes down.