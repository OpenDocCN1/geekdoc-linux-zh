
## Table A16.1 Commonly used ethereal protocol names

| Protocol | Description |
| :--- | :--- |
| arp | ARP |
| esp | Encapsulated Security Payload (VPN) |
| eth | Ethernet |
| frame | a “pseudo-protocol” to allow you to reference packet numbers and capture times. Of course these are not included in Ethernet packets but are stored with the packets in the capture file |
| ftp | FTP |
| http | HTTP |
| icmp | ICMP messages |
| ldap | LDAP |
| lpd | LPD printing |
| lanman | LAN Manager (Microsoft Windows Networking) |
| browser | network browsing (Microsoft Windows Networking) |
| netlogon | Network Logon (Microsoft Windows Networking) |
| netbios | NetBIOS (Microsoft Windows Networking) |
| nbns | NetBIOS name service (Microsoft Windows Networking) |
| nbss | NetBIOS session service (Microsoft Windows Networking) |
| nfs | Network File System |
| telnet | telnet |

## Table A16.2 Commonly used ethereal field names

| Field | Description |
| :--- | :--- |
| esp.spi | Security Parameter Index (VPN, Module 27.3) |
| eth.addr | MAC address (Ethernet) source or destination |
| eth.dst | destination MAC address (Ethernet) |
| eth.src | source MAC address (Ethernet) |
| eth.len | Ethernet packet length |
| eth.type | packet type (0800 = IP, 0806 = ARP) (Module 2.4) |
| frame.number | the frame number (packet number) in the packet list |
| icmp.type | ICMP message type (3 = destination unreachable, 11 = TTL exceeded, 8 = ping/echo request, 0 = ping/echo reply) |
| ip.addr | IP address, source or destination |
| ip.dst | IP destination address |
| ip.src | IP source address |
| ip.proto | IP protocol number (see Appendix 18) |
| tcp.dstport | TCP destination port |
| tcp.srcport | TCP source port |
| tcp.port | TCP port, source, or destination |
| udp.dstport | UDP destination port |
| udp.srcport | UDP source port |
| udp.port | UDP port, source, or destination |

For a full list of protocols and field names, see the **ethereal** manpage, which is included as a real manpage in the Linux distribution, as an HTML file in the Windows distribution, and online at:

- http://www.ethereal.com/ethereal.1.html HTML version
- http://www.uit.co.uk/book/ethereal-manpage.pdf PDF version

### Specifying fields in a packet by byte number

Instead of the *protocol-name.field-name* syntax that we used above, you can specify a component field in a packet directly, as a specific numbered byte or group of bytes, e.g.

```
icmp[0]                       byte 0
eth[12:2]                   2 bytes starting at byte 12, i.e. bytes 12 and 13
```

The byte number referred to is within this protocol’s part of the packet, not the packet as a whole, e.g. **icmp[0]** refers to the first byte of the ICMP data, whereas **eth[0]** is the very first byte of the packet as it appeared on the wire. Figure A16.1 illustrates this, showing how the ICMP data are encapsulated within an IP packet, which in turn is encapsulated in an Ethernet packet. The **icmp[....]** construct “doesn’t see” the IP or Ethernet bytes preceding the ICMP data.

![](img/a2132b646d336d5f9a21102d6320e537_829_0.png)

### Logical operators

Use logical operators for comparisons. You can specify them using either symbols or alphabetic abbreviations:

| Symbol | Abbreviation | Description |
|:-------|:----|:------------------|
| `==` | `eq` | equal |
| `!=` | `ne` | not equal |
| `>` | `gt` | greater than |
| `<` | `lt` | less than |
| `>=` | `ge` | greater than or equal to |
| `<=` | `le` | less than or equal to |

### Specifying values

**integers**: you can specify integers using decimal, octal, or hexadecimal notation, e.g. the following three display filter expressions are equivalent:

```
icmp.type == 11                    decimal 11
icmp.type == 013                   octal 013 = decimal 11
icmp.type == 0xb                  hex 0xb = decimal 11
```

**IP addresses**: you can specify IP addresses as dotted-decimal IP numbers or as host names, e.g.

```
ip.addr == 192.0.2.56
ip.addr == bob.example.com
```

You can use CIDR notation to check whether an IPv4 address is contained in a certain subnet. For example, assuming **bob.example.com** has address 192.0.2.25, either of these display filters will match any address in the 192.0.2 class-C network:

```
ip.addr == 192.0.2.0/24
ip.addr == bob.example.com/24
```

**text strings**: you specify text string values in double quotes, e.g.

```
mount.path == "/datafiles"
```

**groups of bytes**: specify groups of bytes (and Ethernet addresses) as hex numbers separated by colons, dots or hyphens, e.g.

```
eth.dst == ff:ff:ff:ff:ff:ff      destination is Ethernet broadcast address
bootp.hw.address == 0-50-da-e4-61-34
```

If you're comparing a byte string containing only a single byte, the manpage says you have to specify the value using the syntax for integers, above. Consequently, if you were entering a hex value you would prefix it with 0x, as in:

```
icmp.[0] == 0xb      what the manpage says
```

On older versions of **ethereal**, that is necessary. However, on new versions, the string is automatically taken as hex, as in:

```
icmp.[0] == b        new versions only – right
icmp.[0] == 11        new versions only – wrong: 11 hex = 17 decimal
```

## Appendix 17 HTTP/1.1 server response codes

This appendix is based on RFC-2616 June 1999 *Hypertext Transfer Protocol – HTTP/1.1*. The section numbers in the table refer to sections in RFC-2616 and give an explanation of the respective response (or status) code.

The first digit of the status code defines the class of response, as shown in the table below. The last two digits do not have any categorization role (i.e. there are no conventions like “40x is a minor error, 41x is a major error”).

The response descriptions in the table (what the RFC calls “reason phrases”) are only recommendations – they may be replaced (e.g. by local-language equivalents) without affecting the protocol.

| Status Code | Section | Description |
| :--- | :--- | :--- |
| **Informational – request received, continuing process** | | |
| 100 | Module 10.1.1 | Continue |
| 101 | Module 10.1.2 | Switching Protocols |
| **Success – action successfully received, understood, and accepted** | | |
| 200 | Module 10.2.1 | OK |
| 201 | Module 10.2.2 | Created |
| 202 | Module 10.2.3 | Accepted |
| 203 | Module 10.2.4 | Non-Authoritative Information |
| 204 | Module 10.2.5 | No Content |
| 205 | Module 10.2.6 | Reset Content |
| 206 | Module 10.2.7 | Partial Content |
| **Redirection – further action must be taken to complete the request** | | |
| 300 | Module 10.3.1 | Multiple Choices |
| 301 | Module 10.3.2 | Moved Permanently |
| 302 | Module 10.3.3 | Found |
| 303 | Module 10.3.4 | See Other |
| 304 | Module 10.3.5 | Not Modified |
| 305 | Module 10.3.6 | Use Proxy |
| 307 | Module 10.3.8 | Temporary Redirect |
| **Client Error – the request contains bad syntax or cannot be fulfilled** | | |
| 400 | Module 10.4.1 | Bad Request |
| 401 | Module 10.4.2 | Unauthorized |
| 402 | Module 10.4.3 | Payment Required |
| 403 | Module 10.4.4 | Forbidden |
| 404 | Module 10.4.5 | Not Found |
| 405 | Module 10.4.6 | Method Not Allowed |
| 406 | Module 10.4.7 | Not Acceptable |
| 407 | Module 10.4.8 | Proxy Authentication Required |
| 408 | Module 10.4.9 | Request Timeout |
| 409 | Module 10.4.10 | Conflict |
| 410 | Module 10.4.11 | Gone |
| 411 | Module 10.4.12 | Length Required |
| 412 | Module 10.4.13 | Precondition Failed |
| 413 | Module 10.4.14 | Request Entity Too Large |
| 414 | Module 10.4.15 | Request-URI Too Large |
| 415 | Module 10.4.16 | Unsupported Media Type |
| 416 | Module 10.4.17 | Requested Range Not Satisfiable |
| 417 | Module 10.4.18 | Expectation Failed |
| **Server Error - the server failed to fulfill an apparently valid request** | | |
| 500 | Module 10.5.1 | Internal Server Error |
| 501 | Module 10.5.2 | Not Implemented |
| 502 | Module 10.5.3 | Bad Gateway |
| 503 | Module 10.5.4 | Service Unavailable |
| 504 | Module 10.5.5 | Gateway Timeout |
| 505 | Module 10.5.6 | HTTP Version Not Supported |
| **Extended error messages** | | |
| xxx | see below | |

HTTP status codes are extensible, i.e. a server can generate response codes other than the ones listed in the table. HTTP applications are not required to understand the meaning of all registered status codes, although such understanding is obviously desirable. However, applications must understand the class of any status code, as indicated by the first digit, and treat any unrecognized response as being equivalent to the x00 status code of that class, with the exception that an unrecognized response must not be cached. For example, if an unrecognized status code of 431 is received by the client, it can safely assume that there was something wrong with its request and treat the response as if it had received a 400 status code. In such cases, user agents should present to the user the entity returned with the response, since that entity is likely to include human-readable information that will explain the unusual status.
