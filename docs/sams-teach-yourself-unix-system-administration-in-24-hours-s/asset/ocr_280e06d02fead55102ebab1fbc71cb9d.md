```
ftp              86400  IN  CNAME   www
urlwire          86400  IN  A       63.101.93.250
staging          86400  IN  CNAME   urlwire
```

The eagle-eyed among you will have noticed that fully qualified domain names (FQDNs in DNS parlance: a domain that includes all elements—intuitive.com—versus the unqualified domain name www) always have that trailing dot, whereas subdomains do not. It's important to keep this straight, so as not to corrupt your DNS system.

5. Before we leave the discussion about zone files, let's have a peek at a different type, a reverse lookup zone file:

```
# cat /var/named/20.58.161.in-addr.arpa
$TTL 86400
@       IN      SOA     feed11.verio-web.com. hostmaster.verio-web.com. (
                        2002041200  ; serial
                        7200       ; refresh
                        3600       ; retry
                        604800     ; expiry
                        86400 )    ; minimum
                        86400      IN      NS      ns11a.verio-web.com.
                        86400      IN      NS      ns11b.verio-web.com.
91              IN      PTR     www.intuitive.com.
```

Much of this is the same as the earlier zone file, including the TTL, NS, and SOA records. The difference lies in the very last line, which lists the fourth octet of the domain IP address (for example, 91).

![](bbox=[0.3, 0.8, 0.35, 0.9])

> We only need the fourth octet here rather than the entire IP address because we're working with a Class C subnet. If your network has a Class B or Class A subnet, you will need to specify more of the IP address in the reverse lookup zone file. The name should also change to reflect the subnet for the zone. For management purposes, it is better to split your Class A or Class B subnets into Class C zones.

Notice that an inherent limitation of zone files is that we can only list one subnet per file, so a separate reverse lookup zone file is required to permit a reverse lookup for the staging.intuitive.com domain name (for example, the 63.101.93.x subnet).

Writing zone files from scratch is quite confusing, and there are few tools available to help. One that might offer some respite from the potential headache that this represents is available at www.dns tools.com, and it's well worth exploring. Unfortunately, it's only available for Linux as of this writing. Mac OS X users might find DNSsetup a useful, albeit less powerful, alternative tool (homepage.mac.com/dnssetup/).