The database file format is not too strict, but some conventions that have jelled over time. Sticking to these conventions will make your life easier and will smooth the way for the administrator who takes over your creation.

> **TIP:** Comment liberally. In this file, comment lines begin with a semicolon. Although there isn't a lot of technology about what's going on in a DNS database file, a history of the changes is a useful reference about what was being accomplished and why.

Every database file must start with an SOA record and contain at least one NS record. Everything else is optional. (Of course, "everything else" is what makes the file useful!) You may find the following general format helpful to follow:

```
SOA record
NS records
MX records
A and CNAME records
```

For example, here is a complete zone configuration file for a single domain with four hosts:

```
@ IN SOA domain.com. hostmaster.domain.com. (
    1999022300 ; serial number
    10800 ;Refresh every 3 hours
    1800 ;Retry every 30 minutes
    1209600 ;Expire in 2 weeks
    604800 ) ;Minimum 1 week
    IN NS ns.domain.com.
    IN MX 10 mail.domain.com.
imp IN A 192.168.1.1 ; Internet gateway
mail IN A 192.168.1.2 ; mail server
techies IN A 192.168.1.3 ; web server
www IN CNAME techies
ns IN A 192.168.1.4 ; name server
peanutbutter IN A 192.168.1.5 ; firewall
```

And here is the corresponding reverse file:

```
@ IN SOA 1.168.192.in-addr.arpa. hostmaster.domain.com. (
    1999010501 ; Serial
    10800 ; Refresh rate (3 hours)
    1800 ; Retry (30 minutes)
    1209600 ; Expire (2 weeks)
    604800 ) ; Minimum (1 week)
    IN NS ns.domain.com.
1 IN PTR imp.domain.com.
2 IN PTR mail.domain.com.
```