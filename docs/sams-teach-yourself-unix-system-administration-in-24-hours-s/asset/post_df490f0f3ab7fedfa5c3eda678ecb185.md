
```
Domain Name: INTUITIVE.COM
Registrar: NETWORK SOLUTIONS, INC.
Whois Server: whois.networksolutions.com
Referral URL: http://www.networksolutions.com
Name Server: NS11A.VERIO-WEB.COM
Name Server: NS11B.VERIO-WEB.COM
Updated Date: 05-nov-2001

>>> Last update of whois database: Fri, 19 Apr 2002 05:03:06 EDT <<<

The Registry database contains ONLY .COM, .NET, .ORG, .EDU domains and Registrars.
```

You can see in this record that the authoritative name servers are NS11A.VERIO-WEB.COM and NS11B.VERIO-WEB.COM. But where does the information that these are the authoritative name servers for this specific domain come from? A DNS server...

- 2. To be an authoritative name server, the most important part of the configuration is to have a zone file for each domain.

Zone files describe the domain you are providing name services for, and the individual hosts that have been given names. Each domain will usually contain two zone files, one for normal lookups and one for reverse lookups (converting an IP address to its fully qualified domain name).

Zone files typically contain one or more lines of directives, followed by multiple lines listing individual resource types and their hostname and IP address pairs. Here's a typical entry, the one that serves as the start of authority (SOA) for intuitive.com:

> By convention, these zone files are stored in /var/named/ and have filenames that match the domain name, so this is called /var/named/intuitive.com.zone on our server.

```
# cat /var/named/intuitive.com.zone
$ORIGIN intuitive.com.
$TTL 86400

@ IN SOA feed11.verio-web.com. hostmaster.verio-web.com. (
    2002041100 ; serial
    7200       ; refresh
    3600       ; retry
    604800     ; expiry
    86400 )    ; minimum
86400 IN NS ns11a.verio-web.com.
86400 IN NS ns11b.verio-web.com.
86400 IN MX 50 mail-fwd.verio-web.com.
www.intuitive.com. 86400 IN MX 50 mail-fwd.verio-web.com.
intuitive.com. 86400 IN A 161.58.20.91
ftp 86400 IN A 161.58.20.91
smtp 86400 IN A 161.58.20.91
www 86400 IN A 161.58.20.91
urlwire 86400 IN A 63.101.93.250
staging 86400 IN CNAME urlwire
```

There’s a lot in this zone file, so let’s take it one step at a time. First off, notice that the very first line has a trailing dot after the domain name (for example, intuitive.com.). It turns out that this trailing dot is very important, and omitting it is a common mistake for DNS administrators: If you forget, then the hostname is automatically prepended, which is usually wrong.

The second line has the Time-To-Live (TTL) directive, and it’s in units of seconds: 86,400 = 24 hours. Think of this as the expiration date: Once the TTL has expired, any DNS cache is required to request a fresh copy of the data.

- 3. The remainder of the zone file is comprised of resource records. The first resource record is a Start of Authority (SOA), and it has its own TTL, administrative address associated with the domain record (albeit with the usual @ replaced with a dot), and a number of configuration parameters, as detailed in Table 18.1.

### Table 18.1 Start of Authority Fields in a Zone File

| Name | Exemplary Value | Explanation |
|---|---|---|
| Serial | 2002041100 | A unique serial number for this version of this domain record. This should change each time the zone file is edited. By convention, most sysadmins use YYYYMMDD and tack on a two-digit revision value, so this serial number represents a zone file last modified on April 11, 2002. |
| Refresh | 7200 | Number of seconds that secondary servers can use this record without it expiring and needing to be refreshed. |
| Retry | 3600 | How frequently a secondary server should try to contact the primary server to refresh the DNS data in the cache. |
| Expiry | 604800 | The length of time after which the secondary server should stop responding as an authority on the domain when no response has been received from the master. |
| Minimum | 86400 | The length of time other name servers should cache this information, in seconds. |

Notice that the zone file inherently includes the concept of having a secondary, as well as a primary, domain server. This is a smart fail-safe architecture: By having multiple servers able to act authoritatively, users are less likely to have a DNS query fail if the primary server is offline. However, having multiple primary servers leads to a puzzle that this also solves—which of the multiple servers “owns” the domain name record? That’s what all the refresh, expiry, and other values specify—they tell authoritative, but nonprimary, name servers how to interact with the primary for this specific domain name.

- 4. All the subsequent lines in the zone file specify explicit types of domain information. Notice the column that has NS, MX, A, and CNAME values—those indicate whether the specified record is a name server, mail exchange, address records, or alternate (canonical) name, respectively.

For example, we can see explicitly that ns11a.verio-web.com and ns11b.verio-web.com are the name servers (NS) for this domain, and that e-mail receipt queries resolve to mail-fwd.verio-web.com. The second MX record, explicitly listing www.intuitive.com, allows mail sent to a user @www.intuitive.com to resolve properly and drop into the correct mailbox.

![](img/5ced0c78d748bd190e9027e5549a3622_373_0.png)

> This is an important nuance: The same domain name can return different IP addresses, based on the type of query specified. This zone file specifies that all general queries for intuitive.com resolve to 161.58.20.91, except mail exchange queries, which are answered by mail-fwd.verio-web.com.

Finally, there is a set of resource records that actually map domain and subdomain names to explicit IP addresses. Here we can see that intuitive.com and the host ftp, smtp, and www are assigned the same IP address as the main domain record, but urlwire is a completely different IP address. This correctly implies that Web and mail queries to urlwire.intuitive.com are handled by a different server.

The very last record demonstrates a helpful shorthand available in zone files: A CNAME record is essentially an alias, so the line

```
staging 86400 IN CNAME urlwire
```

indicates that queries for staging.intuitive.com should be answered exactly the same as queries for urlwire.intuitive.com.

Commonly, www subdomains are aliases to the main Web server through a CNAME in just this fashion. Indeed, the zone file would be just as valid if the last few lines were written as

```
intuitive.com. 86400 IN A 161.58.20.91
www 86400 IN A 161.58.20.91
smtp 86400 IN CNAME www
ftp 86400 IN CNAME www
urlwire 86400 IN A 63.101.93.250
staging 86400 IN CNAME urlwire
```

The eagle-eyed among you will have noticed that fully qualified domain names (FQDNs in DNS parlance: a domain that includes all elements—intuitive.com—versus the unqualified domain name www) always have that trailing dot, whereas subdomains do not. It's important to keep this straight, so as not to corrupt your DNS system.

- 5. Before we leave the discussion about zone files, let's have a peek at a different type, a reverse lookup zone file:

```
# cat /var/named/20.58.161.in-addr.arpa
$TTL 86400
@       IN      SOA     feed11.verio-web.com. hostmaster.verio-web.com. (
                        2002041200  ; serial
                        7200       ; refresh
                        3600       ; retry
                        604800     ; expiry
                        86400 )    ; minimum
86400   IN      NS      ns11a.verio-web.com.
86400   IN      NS      ns11b.verio-web.com.
91      IN      PTR     www.intuitive.com.
```

Much of this is the same as the earlier zone file, including the TTL, NS, and SOA records. The difference lies in the very last line, which lists the fourth octet of the domain IP address (for example, 91).

![](img/5ced0c78d748bd190e9027e5549a3622_374_0.png)

> We only need the fourth octet here rather than the entire IP address because we're working with a Class C subnet. If your network has a Class B or Class A subnet, you will need to specify more of the IP address in the reverse lookup zone file. The name should also change to reflect the subnet for the zone. For management purposes, it is better to split your Class A or Class B subnets into Class C zones.

Notice that an inherent limitation of zone files is that we can only list one subnet per file, so a separate reverse lookup zone file is required to permit a reverse lookup for the staging.intuitive.com domain name (for example, the 63.101.93.x subnet).

Writing zone files from scratch is quite confusing, and there are few tools available to help. One that might offer some respite from the potential headache that this represents is available at www.dnstools.com, and it's well worth exploring. Unfortunately, it's only available for Linux as of this writing. Mac OS X users might find DNSsetup a useful, albeit less powerful, alternative tool (homepage.mac.com/dnssetup/).
