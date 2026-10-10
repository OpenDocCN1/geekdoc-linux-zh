# # The A Records

The A records map hostnames to IP addresses. Let’s consider the entry for `shevy`. The domain part of the record is specified as `shevy`, but because there is no trailing dot, the domain is relative. Thus, the true domain for the record is `shevy.roaringpenguin.com`.

The data portion of the record specifies `shevy`’s IP address, which is `192.168.2.1`.

For convenience, we also define a local host entry, although most clients will probably find the entry in their `/etc/hosts` file rather than consulting DNS.

# # The MX Records

MX records specify mail exchangers; these machines handle mail for the domain. Each record consists of a preference followed by a hostname. Machines with lower preferences are tried first; if they cannot be contacted, machines with higher preferences are tried next.

In this example, the preferred mail exchanger for `roaringpenguin.com` is `shevy.roaringpenguin.com`. If this machine is down, the secondary mail exchanger is `mail.isp.example`. Note the absolute name for the second example.

# # The CNAME Record

The CNAME record specifies a “canonical” hostname. In the example shown, we set the canonical name of `www.roaringpenguin.com` to be `shevy.roaringpenguin.com`.

# # Reverse Lookup Files

It’s fairly clear how a forward lookup is made: Given a hostname, the resolver queries the DNS server, which eventually returns an IP address. But how are reverse lookups done?

The solution is a clever hack. A pseudo domain `in-addr.arpa` is defined. To look up an IP address, a search is made in this pseudo domain. The IP address is reversed, `in-addr.arpa` is appended and a lookup for a PTR record is issued. This scheme allows the existing DNS machinery to be leveraged without adding any programming changes or complexity.

For example, to look up the name of the host with IP address `192.168.2.3`, the resolver queries the name `3.2.168.192.in-addr.arpa` for a PTR record. Let’s look at the last zone in the example `/etc/named.conf`, the zone `2.168.192.in-addr.arpa`:

```
@ IN SOA shishi.roaringpenguin.com. dfs.roaringpenguin.com.
    1999060501    ; serial
    10800         ; refresh
    3600          ; retry
```