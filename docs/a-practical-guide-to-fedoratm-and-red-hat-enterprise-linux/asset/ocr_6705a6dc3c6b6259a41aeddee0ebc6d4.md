is, the change number—should be incremented each time you change the SOA record.

**refresh** The elapsed time after which the primary master server notifies slave (secondary) servers to refresh the record; the amount of time between updates.

**retry** The time to wait after a refresh fails before trying to refresh again.

**expire** The elapsed time after which the zone is no longer authoritative and the root servers must be queried. The expiry applies to slave servers only.

**minimum** The negative caching (page 1262) TTL, which is the amount of time that a nonexistent domain error (NXDOMAIN) can be held in a slave server's cache. A negative caching TTL is the same as a normal TTL except that it applies to domains that do not exist rather than to domains that do exist.

The $TTL directive (page 875) specifies the default zone TTL (the maximum amount of time data stays in a slave server's cache). Jointly, the default zone TTL and the negative caching TTL encompass all types of replies the server can generate. If you will be adding subdomains or modifying existing domains frequently, set the negative caching TTL to a low number. A short TTL increases traffic to DNS for clients requesting domains that do not exist, but allows new domains to propagate quickly, albeit at the expense of increased traffic.

The following two SOA resource records are equivalent (the parentheses in the first record are optional because the record fits on one physical line):

```
@ IN SOA ns.zach.net. mgs@sobell1.com. ( 2013111247 8H 2H 4W 1D )
```

```
@ IN SOA ns.zach.net. mgs@sobell1.com. ( 
						2013111247 ; serial 
						8H				; refresh 
						2H				; retry 
						4W				; expire 
						1D )			; minimum
```

The second format is more readable because of its layout and the comments. The at symbol (@) at the start of the SOA resource record stands for the zone name (also called the origin) as specified in the named.conf file. Because the named.conf file specifies the zone name to be zach.net, you could rewrite the first line as follows:

```
zach.net. IN SOA ns.zach.net. mgs@sobell1.com. (
```

The host utility returns something closer to the first format with each of the times specified in seconds:

```
$ host -t soa zach.net 
zach.net. SOA ns.zach.net. mgs@sobell1.com. 03111 28800 7200 2419200 86400
```

**TXT** Text Associates a character string with a domain. The Name field holds the domain name. The Data field can contain up to 256 characters and must be enclosed within quotation marks. TXT records can contain any arbitrary text value. As well as general information, they can be used for things such as public key distribution. Following is a TXT resource record that specifies a company name:

```
zach.net. IN TXT		"Sobell Associates Inc."
```