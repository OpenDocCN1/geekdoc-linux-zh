# PTR: Domain Name Pointer

The Domain Name Pointer record is used to translate an IP address to a host name. This is also called the reverse Domain Name Service. The syntax for PTR record is as follows:

```
IP-address IN PTR hostname.
```

For example:

```
206.171.50.51 IN PTR www.ad-engine.com.
```

Here the IP address 206.171.50.51 is associated with the host www.ad-engine.com. You can use a shortened version as follows:

```
51 IN PTR www
```

Typically, an ISP does the primary reverse DNS for a network.

# CNAME: Canonical Name

The Canonical Name record, CNAME, specifies an alias (host name) for the canonical (official) host name. The syntax is as follows:

```
alias IN CNAME canonical_hostname.
```

For example:

```
webserver.ad-engine.com. IN CNAME www.ad-engine.com.
```

Here, webserver.ad-engine.com is an alias for www.ad-engine.com. The shortened version is as follows:

```
webserver IN CNAME www
```

Note that when the webserver.ad-engine.com needs to be resolved to an IP address, the IP address of the www.ad-engine.com is returned. Therefore, you must make sure that at least one A record exists for the canonical host name.

# MX: Mail Exchange

The Mail Exchange record is used to specify a host name that is set up as the SMTP mail server for a domain. The syntax is as follows: