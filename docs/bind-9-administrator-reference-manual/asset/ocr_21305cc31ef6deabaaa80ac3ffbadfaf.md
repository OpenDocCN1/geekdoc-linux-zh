# Appendix A. Appendices

8 Reserved bits

24 bits for Next Level Aggregators. This allows organizations with a TLA to hand out portions of their IP space to client organizations, so that the client can then split the network further by filling in more NLA bits, and hand out IPv6 prefixes to their clients, and so forth.

There is no particular structure for the Site topology section. Organizations can allocate these bits in any way they desire.

The Interface Identifier must be unique on that network. On ethernet networks, one way to ensure this is to set the address to the first three bytes of the hardware address, "FFFF", then the last three bytes of the hardware address. The lowest significant bit of the first byte should be complemented. Addresses are written as 32-bit blocks separated by a colon, and leading zeros of a block may be omitted, for example:

```
3fe:8050:201:9:a00:fe61:2b32
```

IPv6 address specifications are likely to contain long strings of zeros, so the architects have included a shorthand for specifying them. The double colon ('::') indicates the longest possible string of zeros that fit, and can be used only in one address.

# # A.4. Bibliography (Suggested Reading)

# ## A.4.1. Request for Comments (RFCs)

Specification documents for the Internet protocol suite, including the DNS, are published as part of the Request for Comments (RFCs) series of technical notes. The standards themselves are defined by the Internet Engineering Task Force (IETF) and the Internet Engineering Steering Group (IESG). RFCs can be obtained online via FTP at ftp://www.isi.edu/in-notes/RFC,xxx.txt (ftp://www.isi.edu/in-notes/) (where xxx is the number of the RFC). RFCs are also available via the Web at http://www.ietf.org/rfc/

# # Bibliography

# ## Standards

[RFC2974] C. Partridge, Mail Routing and the Domain System, January 1986.

[RFC1034] P.V. Mockapetris, Domain Names — Concepts and Facilities, November 1987.