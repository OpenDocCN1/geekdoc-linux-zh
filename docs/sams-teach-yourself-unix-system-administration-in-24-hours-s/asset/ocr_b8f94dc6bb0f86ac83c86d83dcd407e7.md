```
Domain Name: INTUITIVE.COM
Registrar: NETWORK SOLUTIONS, INC.
Whois Server: whois.networksolutions.com
Referral URL: http://www.networksolutions.com
Name Server: NS11A.VERIO-WEB.COM
Name Server: NS11B.VERIO-WEB.COM
Updated Date: 05-nov-2001
```

>>> Last update of whois database: Fri, 19 Apr 2002 05:03:06 EDT <<<

The Registry database contains ONLY .COM, .NET, .ORG, .EDU domains and Registrars.

You can see in this record that the authoritative name servers are NS11A.VERIO-WEB.COM and NS11B.VERIO-WEB.COM. But where does the information that these are the authoritative name servers for this specific domain come from? A DNS server...

2. To be an authoritative name server, the most important part of the configuration is to have a zone file for each domain.

Zone files describe the domain you are providing name services for, and the individual hosts that have been given names. Each domain will usually contain two zone files, one for normal lookups and one for reverse lookups (converting an IP address to its fully qualified domain name).

Zone files typically contain one or more lines of directives, followed by multiple lines listing individual resource types and their hostname and IP address pairs. Here's a typical entry, the one that serves as the statement or zone of authority (SOA) for intuitive.com:

> By convention, these zone files are stored in /var/named/ and have filenames that match the domain name, so this is called /var/named/intuitive.com.zone on our server.

```
# cat /var/named/intuitive.com.zone
$ORIGIN intuitive.com.
$TTL 86400

@ IN SOA feed11.verio-web.com. hostmaster.verio-web.com. (
    200204110 ; serial
    7200      ; refresh
    3600      ; retry
    604800    ; expiry
    86400 )   ; minimum
```