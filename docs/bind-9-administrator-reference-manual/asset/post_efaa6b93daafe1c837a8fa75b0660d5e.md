
# Chapter 6. BIND 9 Configuration Reference

| | |
|---|-|
| LOC | (x) for storing GPS info. See RFC 1876. Experimental. |
| MX | identifies a mail exchange for the domain. See RFC 974 for details. |
| NAPTR | name authority pointer. |
| NSAP | a network service access point. |
| NS | the authoritative nameserver for the domain. |
| NXT | used in DNSSEC to securely indicate that RRs with an owner name in a certain interval do not exist in a zone and indicate what RR types are present for an existing name. See RFC 2535 for details. |
| PTR | a pointer to another part of the domain name space. |
| PX | provides mappings between RFC 822 and X.400. |
| RP | (x) information on persons responsible for the domain. Experimental. |
| RT | (x)route-binding for hosts that do not have their own direct wide area network addresses. Experimental. |
| SIG | (“signature”) contains data authenticated in the secure DNS. See RFC 2535 for details. |
| SOA | identifies the start of a zone of authority. |
| SRV | information about well known network services (replaces WKS). |
| TXT | text records. |
| WKS | (h) information about which well known network services, such as SMTP, that a domain supports. Historical, replaced by newer RR RR. |
| X25 | (x) representation of X.25 network addresses. Experimental. |

The following classes of records are currently valid in the DNS:

| | |
|---|-|
| IN | the Internet system. |
| | For information about other, older classes of RRs, see Section A.2.1. |

RDATA is the type-dependent or class-dependent data that describes the resource:

# Chapter 6. BIND 9 Configuration Reference

| A | for the IN class, a 32 bit IP address. |
| A6 | maps a domain name to an IPv6 address, with provision for indirection for leading "prefix" bits. |
| CNAME | a domain name. |
| DNAME | provides alternate naming to entire subtree of the domain name space, rather than to a single node. It causes suffix of a queried name to be substituted with a name from the DNAME record's RDATA. |
| MX | a 16 bit preference value (lower is better) followed by a host name willing as a mail exchange for the owner domain. |
| NS | a fully qualified domain name. |
| PTR | a fully qualified domain name. |
| SOA | |

The owner name is implicit, rather than forming an integral part of the RR. For example, names internally form tree or hashes for the name space, and chain RRs off nodes. The remaining RRs are the fixed header (type, class, TTL) which is consistent for all RRs, and a variable (RDATA) that fits the needs of the resource being described.

The meaning of the TTL is a time limit on how long an RR can be kept in a cache. This limit does not apply to authoritative data in zones; it is also timed out, by the refreshing policies for the zone. Short TTLs can be used to minimize caching, and a zero TTL prohibits caching, the realities of Internet performance suggest that these schemes should be on the order of days for the TTL. If a change can be anticipated, the TTL can be reduced prior to the change to minimize inconsistency during the change, and then increased back to its former value following the change.

The data in the RDATA section of RRs is carried as a combination of binary strings and domain names. The domain names are framed as "pointers" to other data in the DNS.

# 6.3.1. Textual expression of RRs

RRs are represented in binary form in the packets of the DNS protocol, and are usually represented in highly encoded when stored in a nameserver or resolver. The examples provided in RFC 1034, a style similar to that used in master files was employed to show the contents of RRs. In this format, most of RRs are shown on a single line, although continuation lines are possible using parentheses.

The start of the line gives the owner of the RR. If a line begins with a blank, then the owner is assumed to be the same as that of the previous RR. Blank lines are often included for readability.

Following the owner we list the TTL, type, and class of the RR. Class and type use the mnemonics defined above, and TTL is an integer before the type field. In order to avoid ambiguity in parsing, type and class mnemonics are disjoint, TTLs are integers, and the type mnemonic is always last. IN class and TTL values are often omitted from examples in the interests of clarity.

The resource data or RDATA section of the RR are given using knowledge of the typical representation for the data.

For example, we might show the RRs carried in a message as:

| ISI.EDU. | MX | 10 VENERA, ISI.EDU. |
| | MX | 10 VAXA, ISI.EDU. |
| VENERA.ISI.EDU | A | 128.9.0.32 |
| | | 10.1.0.52 |
| VAXA.ISI.EDU | A | 10.2.0.27 |
| | | 128.9.0.33 |

The MX RRs have an RDATA section which consists of a 16 bit number followed by a domain name. The address RRs use a standard IP address format to contain a 32 bit internet address.

This example shows six RRs, with two RRs at each of three domain names.

Similarly we might see:

| XX.LCS.MIT.EDU. | IN A | 10.0.0.44 |
| CH | A | MIT.EDU. 2420 |

This example shows two addresses for XX.LCS.MIT.EDU, each of a different class.

# 6.3.2. Discussion of MX Records

As described above, domain servers store information as a series of resource records, each of which contains a particular piece of information about a given name (which is usually, but not always, a host). The simplest way to track a RR is as a typed pair of data, a domain name matched with a relevant datum, and stored with some additional type information to help systems determine when the RR is relevant.

MX records are used to control delivery of email. The data specified in the record is a priority and a

# Chapter 6. BIND 9 Configuration Reference

domain name. The priority controls the order in which delivery is attempted, with the lowest first. If two priorities are the same, a server is chosen randomly. If neither of those succeed, the mail will fall back to the next priority. The maximum time for negative caching is 3 hours (3h).

MX records are used to control delivery of email. The data specified in the record is a priority and a

domain name. The priority controls the order in which delivery is attempted, with the lowest first. If two priorities are the same, a server is chosen randomly. If neither of those succeed, the mail will fall back to the next priority. The maximum time for negative caching is 3 hours (3h).

# Chapter 6. BIND 9 Configuration Reference

| example.com. | IN MX | 10 | mail.com |
| | IN MX | 10 | mail2.com |
| | IN MX | 20 | backup.org |
| mail.com | IN A | 10.0.0.1 |
| mail2.com | IN A | 10.0.0.2 |

> **Note:** The $ORIGIN lines in the examples are for providing context to the examples-they do not necessarily appear in the actual usage. They are only used here to indicate that the example is relative to the listed origin.

# 6.3.3. Setting TTLs

The time to live of the RR field is a 32 bit integer represented in units of seconds, and is primarily used by resolvers when they cache RRs. The TTL describes how long an RR can be cached before it is discarded. The following three types of TTL are currently used in a zone file.

| SOA | The last field in the SOA is the negative TTL. This controls how long other servers will cache NXDOMAIN responses from you. |
| The maximum time for negative caching is 3 hours (3h). |
| TTL | The $TTL directive at the top of the zone file (before the SOA) gives a default TTL for every RR without a specific TTL. |

Each RR can have a TTL as the second field in the RR, which will control how long it. All of these TTLs default to seconds, though units can be explicitly specified, for example, 1h30m.

# 6.3.4. Inverse Mapping in IPv4

Reverse name resolution (that is, translation from IP address to name) is achieved by means of the in-addr.addrpa domain and PTR records. Entries in the in-addr.addrpa domain are made in least-to-most significant order, read left to right. This is the opposite order to the way IP addresses are usually written. Thus, a machine with an IP address of 10.1.2.3 would have a corresponding in-addr.addrpa name of 3.2.1.10. This name should have a PTR resource record whose data field is the name of the machine or, optionally multiple PTR records if the machine has more one name. For example, in the [example] domain:

| $ORIGIN | 2.1.10.in-addr.arpa |
| 3 | IN PTR foo.example.com |

> **Note:** The $ORIGIN lines in the examples are for providing context to the examples-they do not necessarily appear in the actual usage. They are only used here to indicate that the example is relative to the listed origin.

# 6.3.5. Other Zone File Directives

The Master File Format was initially defined in RFC 1035 and has subsequently been extended. While the Master File Format itself is class independent all records in a Master File must be of the same class. Master Files include $ORIGIN, $INCLUDE, and $TTL.

# 6.3.5.1. The $ORIGIN Directive

Syntax: $ORIGIN domain-name [ comment ]
