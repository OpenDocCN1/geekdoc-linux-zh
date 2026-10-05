```
options {
forwards { 192.168.42.10; 192.168.42.20; };
}
```

This sends unresolved queries to the two servers mentioned instead of sending them to local caching DNS. This can be advantageous when there's a premium on outside traffic. all internal servers resolve outside names via one or two servers, those servers build huge caches, meaning that more queries are resolved inside the building walls. Otherwise, all the servers might be making identical queries to the outside world.
If for some reason the forwarder cannot answer the query, the query is tried via the normal server caching DNS. To absolutely forbid any non-local query from a DNS server, place a forwarder-only; statement right below the forwarders statement. Doing this makes the forwarder server(s) a single point of failure, so it's not recommended.

# DNS Zone Data Files

Zone data files are pointed to the file statements in the boot file's zone sections and contain all data about the zone. The first thing to understand is that the syntax of a zone data file is totally different from the syntax of the boot file named.conf.

# Zone Data File Syntax Is Totally Different from Boot File Syntax

It's important to remember that the syntax of the zone data files is not the same as that of the DNS boot file (named.conf). The zone data file comment character is the semicolon. For each line, DNS will fail if the name data item has spaces before it.

> Note
The name data item is normally the first on the line and must not be preceded with spaces. Occasionally, however, the name data item can be absent from the line, giving the appearance of space before the first data item. What's really happening is that the name data item was left off the line, allowing it to default to the name data item in the nearest previous line containing a name data item. For all practical purposes, the next data item after the name is either the word IN or a number representing a “Time To Live” (followed by IN). Knowing this can help you avoid much confusion.