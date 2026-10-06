# 508 Chapter 21 · Installing and Configuring Primary Network Services

The contents of a correct named.ca hint file can be obtained via FTP ftp://ftp.rs.internic.net/domain/named.root. The remaining files must be coded by hand. A forward zone file typically specifies:

+   - The host is the start of authority (SOA) for the zone
- The e-mail address of the administrator responsible for the zone
- Mappings from host names to IP addresses for hosts in the zone

In addition, the zone file may specify secondary name servers, mail exchange records, and host aliases (called canonical names or CNAMEs). Here is a typical forward zone file:

```
@ IN SOA azusapacific.com.
root.azusapacific.com. (
200002051 ; serial time
43200 ; refresh time
3600 ; retry time
3600000 ; expire time
2419200 ; default_ttl
)
@ IN NS azusapacific.com.
@ MX 10 azusapacific.com.
localhost A 127.0.0.1
azusapacific.com. IN 192.168.1.1
bill IN 192.168.1.2
toshiba IN 192.168.1.99
router IN CNAME azusapacific.com.
www IN CNAME azusapacific.com.
ftp IN CNAME azusapacific.com.
mail IN CNAME azusapacific.com.
```

Note the usual use of a period in the e-mail address of the zone administrator (root.azusapacific.com.) and following the domain name azusapacific.com.). The underlying concept is that host names, fully qualified or not, end with a dot when specified in the zone file and other DNS configuration files. The format of the file is more fully described in the named man page.

The series of numbers in the SOA record specify:

+   - A serial number used by slaves to determine information has changed
- The refresh interval at which slaves should check the serial number, in seconds
- The interval at which a slave should retry after a failed refresh, in seconds

Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com