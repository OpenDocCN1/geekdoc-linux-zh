# Start of Authority Header

The Start of Authority Header (SOA) is the first entry in the db file. The SOA indicates that this name server is the best (authoritative) source for information in this domain. There can be only one SOA entry per db file. A sample SOA looks like the following:

```
bar.org. IN SOA  foo.bar.org.  dab.bar.org. (
                         1998122300  ; Serial
                         10800       ; Refresh time - 3 hours
                         3600        ; Retry - 1 hour
                         604800      ; Expire - 1 week
                         86400       ; TTL - 1 day
                         )
```

The first part of the entry, bar.org. (note the trailing .), indicates the domain to which this db file refers. The IN indicates Internet. The SOA indicates that this is the SOA record entry for this file. The entry foo.bar.org. is the host on which you created the file, and the entry dab.bar.org is the email address of the db file’s contact. The address is converted from dab.bar.org to dab@bar.org.

> > **Tip**
> > One of the most common misconfiguration problems with name servers has to do with the use of terminating periods (.) on entries. The rule is, if you don’t want to have the domain name (bar.org.) appended to the entry, remember to include the trailing period.

The parentheses permit the data that follows to span multiple lines. The opening parenthesis must be on the first line. Within the parentheses are various values that the name server passes to querying name servers. The first is the serial number. Serial numbers are for secondary masters. They compare the current serial number with the one that they had when they downloaded the data. If the two are different, they download the new data. If the two are the same, they do not. This serial number can be any number which increments. One method is shown: the eight-digit date plus a two-digit trailing sequence number (it is unlikely you’ll make more than 99 changes to the db file in one day). Note that a ; begins a comment and continues to the end of the line.

> > **Tip**
> > Remember to change the serial number and restart the name server (ndc reload) or your changes will not take effect.

The refresh time, retry time, and expire time are also for secondary masters. These tell the secondary that it needs to refresh its data (check the serial number), and, if it is different, reload) at this interval in seconds. If the primary master is not available, it needs to retry every hour. If it cannot make contact for a week, the zone expires and the domain data needs to be flushed.

The TTL tells how long a name server that is not a secondary master is to cache the data. If your zone is static, longer times decrease the load on your name server. If you need to change the file often, you’ll want to decrease this time; however, this will cause a significant increase in queries because after this amount of time, name servers must re-query.