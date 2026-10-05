# Chapter 6. BIND 9 Configuration Reference

set of resource information associated with a particular name is composed of separate RRs. The order of RRs in a set is not significant and need not be preserved by nmservers, resolvers, or other parts of the DNS. sorting of multiple RRs is permitted for optimization purposes, for example, to specify that a particular nearby server be tried first. See Section 6.2.14.11 and Section 6.2.14.12.

The components of a Resource Record are:

| owner name | the domain name which the RR is found. |
| type | an encoded 16 bit value that specifies the type of the resource in this resource record. Types refer to abstract resources. |
| TTL | the time to live of the RR. This field is a 32 bit integer in units of seconds, and is primarily used by resolvers when they cache RRs. The TTL describes how an RR can be cached before it should be discarded. |
| class | an encoded 16 bit value that identifies a protocol family or instance of a protocol. |
| RDATA | the type and sometimes class-dependent data that describes the resource. |

The following are types of valid RRs (some of these listed, although not obsolete, are experimental (x) or historical (h) and no longer in general use):

| A | a host address. |
| A6 | an IPv6 address. |
| AAAA | Obsolete format of IPv6 address |
| AFSDB | (x) location of AFS database servers. Experimental. |
| CERT | holds a digital certificate. |
| CNAME | identifies the canonical name of an alias. |
| DNS | delegation of reverse addresses. Replaces with another name to be looked up. Described in RFC 2672. |
| GPOS | specifies the global position. Superseded by LOC. |
| HINFO | identifies the CPU and OS used by a host. |
| ISDN | (x) representation of ISDN addresses. Experimental. |
| KEY | stores a public key associated with a DNS name. |
| KX | identifies a key exchanger for this DNS name. |

90