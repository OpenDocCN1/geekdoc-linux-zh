
To discuss arrangements for support, contact info@isc.org (mailto:info@isc.org) or visit the ISC web page at http://www.isc.org/services/support/ to read more.

## Appendix A. Appendices

### A.1. Acknowledgements

### A.1.1. A Brief History of the DNS and BIND

Although the "official" beginning of the Domain Name System occurred in 1984 with the publication of RFC 920, the core of the new system was described in 1983 in RFCs 882 and 883. From 1984 to 1987, the ARPANet (the precursor to today's Internet) became a testbed of experiment for developing the new naming/addressing scheme in an rapidly expanding, operational network environment. New RFCs were written and published in 1987 that modified the original documents to incorporate improvements based on the working model. RFC 1034, "Domain Names-Concepts and Facilities," and RFC 1035, "Domain Names-Implementation and Specification" were published and became the standards upon which all DNS implementations are.

The first domain name server, called "Jeeves," was written in 1983-84 by Paul Mockapetris on DEC Tops-20 machines at the University of Southern California's Information Science Institute (US-ISI) and SRI's International Network Center (SRI-NC). A DNS server for universities, the Berkeley Internet Name Domain (BIND) package, was written soon after by a group of graduate students at Berkeley at the University of California under a grant from the US Defense Advanced Research Projects Administration (DARPA). Versions of BIND through 4.8.3 were maintained by the Computer Science Group (CSRG) at UC Berkeley, Douglas Terry, Mark Painter, David Ripple and Songchun Zhou made the initial BIND project team. After additional work on the software package was done by Ralph Campbell, Kevin Dunlap, a Digital Equipment Corporation employee loan to CSRG, maintained BIND for 2 years, from 1985 to 1987. Many other people also contributed to BIND development during: Doug Kingston, Craig Partridge, Smart Carl-Mitchell, Mike Jim Bloom and Mike Schwartz. BIND maintenance was subsequently handled by Mike Karels and O. K.

BIND versions 4.9.1 was released by Digital Equipment Corporation (now Compaq Corporation). Paul Viese, then a DEC employee, became BIND's primary caretaker. Paul was assisted by Phil Alquist, Robert Elz, Jan Barrett, Paul Albitz, Bryan Beecher, Andrew Part, Andrew Cherenson, Tom Limcinelli, Berthold Alffrath, Faisal Baaran, Anant Kumar, Art Hardin, Win Treese, Don Lewis, Christophe Wolffugel, and others.

BIND Version 4.9.2 was sponsored by Wix Enterprises. Paul Viese became BIND's primary architect/programmer.

BIND versions from 4.9.3 onward have been developed and maintained by the Internet Software Consortium with support being provided by ISC's sponsors. As co-architects/programmers, Bob Halley and Paul Vicxie released the first production-ready version of BIND version 8 in May 1997.
BIND development work is made possible today by the sponsorship of several corporations, and by the tireless work efforts of numerous individuals.

## A.2. Historical DNS Information

### A.2.1. Classes of Resource Records

### A.2.1.1. HS = hesiod

The [hesiod] class is an information service developed by MIT's Project Athena. It is used to share information about various systems databases, such as users, groups, printers and so on. The keyword **hs** is a synonym for hesiod.

### A.2.1.2. CH = chaos

The **chaos** class is used to specify zone data for the MIT-developed CHAOSnet, a LAN protocol created in the mid-1970s.

## A.3. General DNS Reference Information

### A.3.1. IPv6 addresses (A6)

IPv6 addresses are 128-bit identifiers for interfaces and sets of interfaces which were introduced in the DNS to facilitate scalable Internet routing. There are three types of addresses: *Unicast*, an identifier for a single interface; *Anycast*, an identifier for a set of interfaces; and *Multicast*, an identifier for a set of interfaces. Here we describe the global Unicast address scheme. For more information, see RFC 2374.

The aggregable global Unicast address format is as follows:

| 3 | 13 | 8 | 24 | 16 | 64 bits |
|---|---|---|---|---|---|
| FP | TLA | RES | NLA ID | SLA ID | Interface ID |
|---|---|---|---|---|---||
| ID | <--- Public Topology ---> | | <-Site Topology-> | <--- Interface Identifier ---> |

Where

| FP | = Format Prefix (001) |
| TLA ID | = Top-Level Aggregation Identifier |
| RES | = Reserved for future use |
| NLA ID | = Next-Level Aggregation Identifier |
| SLA ID | = Site-Level Aggregation Identifier |
| INTERFACE ID | = Interface Identifier |

The **Public Topology** is provided by the upstream provider or ISP, and (roughly) corresponds to the IPv4 network section of the address range. The **Site Topology** is where you can subnet this space, much as subnetting an IPv4/16 network into /24 subnets. The **Interface Identifier** is the address of an individual interface on a given network. (With IPv6, addresses belong to interfaces rather than machines).
The subnetting capability of IPv6 is much more flexible than that of IPv4: subnetting can now be carried out on boundaries, may vary the same as Classless InterDomain Routing (CIDR).
The internal structure of the Public Topology for an A6 global unicast address consists of:

| 3 | 8 | 24 |
|---|---|---|---|
| FP | TLA ID | RES | NLA ID |

A 3 bit FP (Format Prefix) of 001 indicates this is a global Unicast address. FP lengths for other types of addresses may vary.
13 TLA (Top-Level Aggregator) gives the prefix of your top-level backbone carrier.

8 Reserved bits

24 bits for Next Level Aggregators. This allows organizations with a TLA to hand out portions of their IP space to client organizations, so that the client can then split the network further by filling in more NLA bits, and hand out IPv6 prefixes to their clients, and so forth.

There is no particular structure for the Site topology section. Organizations can allocate these bits in any way they desire.

The Interface Identifier must be unique on that network. On ethernet networks, one way to ensure this is to set the address to the first three bytes of the hardware address, "FFFF", then the last three bytes of the hardware address. The lowest significant bit of the first byte should be complemented. Addresses are written as 32-bit blocks separated by a colon, and leading zeros of a block may be omitted, for example:

```
3fe:8050:201:9:a00:fe61:2b32
```

IPv6 address specifications are likely to contain long strings of zeros, so the architects have included a shorthand for specifying them. The double colon ('::') indicates the longest possible string of zeros that fit, and can be used only in one address.

## A.4. Bibliography (Suggested Reading)

### A.4.1. Request for Comments (RFCs)

Specification documents for the Internet protocol suite, including the DNS, are published as part of the Request for Comments (RFCs) series of technical notes. The standards themselves are defined by the Internet Engineering Force (IETF) and the Internet Steering Group (IESG). RFCs can be obtained online via FTP at ftp://www.isi.edu/in-notes/RFC.txt (where xxx is the number of the RFC). RFCs are also available via the Web at http://www.ietf.org/

## Bibliography

### Standards

[RFC2974] C. Partridge, Mail Routing and the Domain System, January 1986.

[RFC1034] P.V. Mockapetris, Domain Names — Concepts and Facilities, November 1987.

[RFC1035] P.V. Mockapetris, Domain Names — Implementation and Specification, November 1987.

### Proposed Standards

[RFC2181] R. El and R. Bush, Clarifications to the DNS Specification, July 1997.
[RFC2308] M. Andrews, Negative Caching of DNS Queries, March 1998.
[RFC1995] M. Ohta, Incremental Zone Transfer in DNS, August 1996.
[RFC1996] P. Pixie, S. Thomson, Y. Rekhter, and J. Bound, Dynamic Updates in the Domain Name System, April 1997.
[RFC2845] P. Pixie, O. Gudmundsson, D. Eastlake, 3rd, and B. Wellington, Secret Key Transaction Authentication for DNS (TSIG), May 2000.

### Proposed Standards Under Development

[RFC1886] S. Thomson and C. Huitema, DNS Extensions to support IP version 6, December 1995.
[RFC20655] D. Eastlake, 3rd and C. Kaufman, Domain Name System Security Extensions, January 1997.
[RFC2137] D. Eastlake, 3rd, Secure Domain Name Dynamic Update, April 1997.

### Other Important RFCs About DNS Implementation

[RFC1535] E. Gavron, A Security Problem and Proposed Correction With Widely Deployed DNS Software., October 1993.
[RFC1536] A. Kumar, P. Postel, C. Neuman, P. Danzig, and S. Miller, Common DNS Implementation Errors and Suggested Fixes, October 1993.
[RFC1982] R. El and R. Bush, Serial Number Arithmetic, August 1996.
