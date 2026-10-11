PTR **Pointer**—Maps an IP address to a domain name and is used for reverse name resolution. The Name field holds the IP address; the Data field holds the domain name. Do not use PTR resource records with aliases. The following resource record maps 3 in a reverse zone (for example, 3 in the 0.168.192.in-addr.arpa zone is 192.168.0.3) to **grape** in the zone:

```
```
3    IN    PTR    grape
```
```

For more information refer to “Reverse Name Resolution” on page 783.

SOA **Start of Authority**—Designates the start of a zone. Each zone must have exactly one SOA record. An authoritative server maintains the SOA record for the zone it is authoritative for.

All zone files must have one SOA resource record, which must be the first resource record in the file. The Name field holds the name of the domain at the start of the zone. The Data field holds the name of the host the data was created on, the email address of the person responsible for the zone, and the following information enclosed within parentheses (the opening parenthesis must appear on the first physical line of an SOA record):

+   - **serial**: A value in the range 1–2,147,83,647. A change in this number indicates that the zone data has changed. By convention, this field is set to the string **yyyymmddnn** (year, month, day, change number). Along with the date, the final two digits—that is, the change number—should be incremented each time you change the SOA record.
+   - **refresh**: The elapsed time after which the primary master server notifies slave (secondary) servers to refresh the record; the time between updates.
+   - **retry**: The time to wait after a refresh fails before trying to refresh again.
+   - **expiry**: The elapsed time after which the zone is no longer authoritative and the root servers must be queried. The expiry applies to slave servers only.
+   - **minimum**: The negative caching TTL, which is the amount of time that a nonexistent domain error (**NXDOMAIN**) can be held in a slave server’s cache. A negative caching TTL is the same as a normal TTL except that it applies to domains that do not exist rather than to domains that do exist.

The **$TTL** directive (page 797) specifies the default zone TTL (the maximum amount of time that data stays in a slave server’s cache). Jointly, the default zone TTL and the negative caching TTL encompass all types of replies the server can generate.

The following two SOA resource records are equivalent:

```
```
@ IN SOA    ns.zach.net.    mgs@sobell.com. ( 2005111247 8H 2H 4W 1D )

@ IN SOA    ns.zach.net.    mgs@sobell.com. (
                                          ; serial
                        2005111247
                                8H    ; refresh
                                2H    ; retry
                                4W    ; expire
                                1D    ; minimum
                                )
```
```