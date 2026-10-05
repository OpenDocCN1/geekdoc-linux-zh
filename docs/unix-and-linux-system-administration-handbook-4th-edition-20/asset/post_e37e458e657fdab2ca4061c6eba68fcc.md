
# Chapter 17 DNS: The Domain Name System

When an administrative boundary falls in the middle of a byte, you have to be sneaky. You must also work closely with the domain above or below you. The trick is for this: each possible host address in the natural-addr.arpa zone, a CNAME that deflects the lookup to a zone controlled by the owner of the appropriate subnet. This scheme makes for messy zones on the parent, but it lets you delegate authority to the actual users of each subnet.

Here is the scheme in detail. The parent organization (in one case, the ISP) creates CNAME records for each possible IP address with an extra component (dot-separated chunk) that represents the subnet. For example, in the /26 scenario, the first quarter of the addresses would have a "0-63" component, the second quarter would have a "64-127" component, and so on. Here’s what it looks like:

```
$ORIGIN 243.138.128.in-addr.arpa
1 IN CNAME 1.0-63
2 IN CNAME 2.0-63

63 IN CNAME 63.0-63
64 IN CNAME 64.64-127
65 IN CNAME 65.64-127
```

To delegate the 0-63 piece of the reverse zone to the customer that has been signed that subnet, add the following NS records:

```
0-63 IN NS ns1.customer.com.
0-63 IN NS ns2.customer.com.
```

customer1.com's site would have a zone file that contained the reverse mappings for the 0-243.138.128.in-addr.arpa zone.

For example,

```
1 IN PTR host1.customer.com.
2 IN PTR host2.customer.com.
```

By adding this extra, we create a "cut" at which to perform delegation. When someone looks up the reverse mapping for 128.138.243.1, for example, the CNAME record at 1.243.138.128.in-addr refocuses the search to the name 1.0-243.138.128.in-addr.arpa, which is controlled by the customer.

The customer’s files are clean; only the ISP must deal with an elegant configuration mess. But things can get more complicated. Customer could itself be an ISP that wants to further subdivide its addresses. But that’s OK: chains of CNAMEs can be up to eight links, and since a byte has only eight bits, we can never run out. CNAME chains are discouraged but not forbidden in the RFCs; they slow down name resolution each link in a CNAME chain causes the link to be followed and a new query for the target to be initiated.

# SRV records

Early in the life of the CNAME hack, the $GENERATE command was added to BIND's repertoire to facilitate the creation of resource records in the parent zone. For example, the following lines produce the records for the first subnet:

```
$ORIGIN 243.138.128-in-addr.arpa.
$GENERATE 0-63 CNAME $0-63
0-63 NS ns1.customer1.com.
0-63 NS ns2.customer1.com.
```

The $ in the $GENERATE command (itself a B extension) iterates from 0 to 63 and creates 64 different CNAME records. The other /26 networks would be handled similarly.

# SRV records

An SRV record specifies the location of services within a domain. For example, the SRV record lets you query a remote domain for the name of its FTP server. Before SRV, you had to hope the remedy sysadms followed the prevailing custom and added a CNAME for "ftp" to their server's DNS records.

SRV records make more sense than CNAMEs for this application and certainly a better way for sysadms to move around and control their use. However, SRV records must be explicitly sought and parsed by clients, so it will be a while before their effects are felt. They are used extensively by Windows.

SRV records resemble MX records with fields that tell the DNS administrator steer and load-balance connections from the outside world.

```
service.proto.name [ttl] [IN] SRV priority weight target
```

where service is defined in the IANA assigned numbers database (iana.org/numbers.htm), proto is either tcp or udp, name is the domain to which the SRV record refers, priority is an MX-style priority, weight is a weight for load balancing among several servers, port is the port on which the service runs, and target is the hostname of the server that provides the service. To avoid a round trip, DNS servers usually return the A record of the target with the answer.

A value of 0 for the "wt" for the target means that no special load balancing should be done. A value is snatched from the RFC2782 and trusted for:

```
_ftp_tcp SRV 0 0 21 ftp-server.atrust.com.
; 1/4 of the connections to old box, 3/4 to the new one
_ssh_tcp SRV 0 1 22 old-slow-box.atrust.com.
SRV 0 3 22 new-fast-box.atrust.com.
```

```
; main server on port 80, backup on new server
_ftp_tcp SRV 0 0 8000 www-server.atrust.com.
SRV 10 0 8000 new-fast-box.atrust.com.
```

```
; both http://www.atrust.com and http://atrust.com work
_http.tcp SRV 0 0 80 www-server.atrust.com.
SRV 10 0 8000 new-fast-box.atrust.com.
```

```
; all other services (target = )
*_tcp SRV 0 0 0
*_udp SRV 0 0 0
```

This example illustrates the use of both the weight parameter (for SSH) and the priority parameter (HTTP). Both servers are used, with work split between them. The backup server is used when the principal service is unavailable.

# IPv6 resource records

The records are specified in RFC1886 (1995). IPv6 is a new version of the IP protocol. It has spent over 15 years in the specification process and has spawned around 250 RFCs, yet it still isn't really done.¹ IPv6 was originally motivated by a perceived need for more IP addresses; however, the stopgap solutions to this problem (CIDR, private addresses, NAT, stricter control of addresses) have been so successful that a mass migration to IPv6 has turned out to be as essential as originally envisioned–least, not quite. The adoption of IPv6 is now being driven by Asia, where IPv4 addresses are spread more thinly.

IPv6 DNS records are totally separate from the transport protocol used to deliver them. Publishing IPv6 records in your DNS zones does not mean that you must answer queries for them with IPv6. About half the query on the root server (k.root-servers.net) consists of queries for IPv4 A records, and one quarter consists of queries for IPv6 AAAA records. However, 99% of all actual queries use IPv4 transport.

# IPv6 forward records – AAAA

The format of a AAAA record is

```
hostname [ttl] [IN] AAAA ipaddr
```

For example:

```
f.root-servers.net. IN  AAAA  2001:500:2:f:
```

Each colon-separated chunk of the address with leading zeros omitted. Two adjacent digits stand for “enough zeros to fill the 128 bits of a complete IPv6 address.” An address can contain at most one such double colon.

See page 582 for a discussion of the IPv4 version of PTR records.

# IPv6 reverse records – PTR

In IPv6, the reverse mapping information corresponding to a AAAA address is a PTR record in the ipv6.arp top-level domain.

The “nibble” format represents an AAAA address by expanding each colon-separated chunk to the full 4 hex digits and reversing the order of those digits and tack on ipv6.arp at the end. For example, the PTR record that corresponds to our sample AAAA record would be

```
f.0.0.0.0.0.0.0.0.0.0.0.0.0.0.f.2.0.0.5.0.1.0.2.ipv6.arp
```

```
PTR f.root-servers.net.
```

(This line has been folded to the fit page.) It’s unfortunately not very friendly for a sysadmin to type or debug or ever read. In your actual DNS zone files, the $ORIGIN statement could hide some of the complexity.

# TXT records

A TXT record adds arbitrary text to a host's DNS records. The format of a TXT record is

name [ttl] [IN] TXT info

All info items must be quoted. You can use a single string or multiple strings that are individually quoted. Be sure the quotes are balanced—missing quotes wreak havoc on the records between the next occurrence of quote disappears with your DNS data. With other resource records, return TXT records in random order. To encode length as addresses, use text lines longer than a collection of several TXT records.

Because TXT records have no particular format, they are sometimes used to test prospective of DNS records without requiring changes to the DNS system. For example, SPF records (see page 590) were originally implemented as TXT records. Now that a dedicated record type has been created, the TXT version is no longer recommended, but many sites do it.

¹14. Tony Li, an active member of the IETF community, once described IPv6 as “too little, too soon.”
