
# TCP/IP 概述

TCP/IP 已成为互联网上的首选协议——这个“网络之网络”从 ARPANet 演变而来，ARPANet 是一种分组交换网络，其本身源于 20 世纪 70 年代美国政府高级研究计划署 (ARPA)。随后，ARPA 获得了国防前缀并变为 DARPA。在 DARPA 的支持下，TCP/IP 协议成为了一套流行的互联协议集——“互联”是描述网络之间通信的术语。

TCP/IP 之能繁荣有几个原因。一个重要原因是该协议是开放的，这意味着协议的术描述出现在公共文档中，因此任何人可以在特定的硬件和软件上实现 TCP/IP。

TCP/IP 成功的另一个更重要的原因是提供了示例实现。与其在纸面上描述网络架构和协议，不如 TCP/IP 协议族的每个组件从诞生之初就作为一个带有示例实现的规范存在的。

## 审视 RFCs

TCP/IP 协议的细节（包括 TCP 和 IP，以及 SMTP 和 FTP 等特定服务协议）在被称为“意见请求”（RFCs）的文档中描述。这些文档在互联网上免费分发。你可以从 http://www.cls.ohio-state.edu/hypertext/information/rfc.html 获取 RFC（点击 Index 链接查看完整的 RFC 列表或通过关键词搜索）。另一个用于 RFC 的良好 URL 是 http://www.faqs.org/rfc。

事实上，用于统一方式命名互联网资源的符号本身就记录在某个 RFC 中。这种被称为“统一资源定位符”（URL）的符号在 RFC 1738 中描述；它由万维网 (WWW) 的创始人 T. Berners-Lee 等人编写。

你可以将 RFC 视为互联网研究与开发社区的工作论文。所有的互联网标准都以 RFC 的形式发布。然而，许多 RFC 并没有规定标准；它们仅仅是信息性文档。

以下是你可能感兴趣的一些 RFC：

- RFC 768, "User Datagram Protocol (UDP)"
- RFC 791, "Internet Protocol (IP)"
- RFC 792, "Internet Control Protocol (ICMP)"
- RFC 793, "Transmission Control Protocol (TCP)"
- RFC 854, "TELNET Protocol Specification"
- RFC 950, "Internet Standard Subnetting Procedure"
- RFC 959, "File Transfer Protocol (FTP)"
- RFC 1034, "Domain Names: Concepts and Facilities"
- RFC 1058, "Routing Information Protocol (RIP)"
- RFC 1112, "Host Extensions for IP Multicasting"
- RFC 1155, "Structure and Identification of Management Information for TCP/IP-based Internets"
- RFC 1157, "Simple Network Management Protocol (SNMP)"
- RFC 1519, "The Point-to-Point Protocol (PPP)"
- RFC 1661, "Classless Inter-Domain Routing (CIDR) and Assignment Strategy"
- RFC 1738, "Uniform Resource Locators (URL)"
- RFC 1796, "Not All RFCs Are Standards"
- RFC 1855, "Netiquette Guidelines"
- RFC 1886, "DNS Extensions to Support IP Version 6"
- RFC 1918, "Address Allocation for Private Internets"
- RFC 1939, "Post Office Protocol, Version 3 (POP3)"
- RFC 1945, "HyperText Transfer Protocol—HTTP/1.0"
- RFC 2026, "The Internet Standards"
- RFC 2028, "The Organizations Involved in IETF"
- RFC 2045, "Multipurpose Internet Mail (MIME) Parts"
- RFC 2060, "Internet Message Access—Version 4 (IMAP)"
- RFC 2131, "Dynamic Host Configuration (DHCP)"
- RFC 2146, "U.S. Government Domain Names"
- RFC 2151, "A Primer on Internet and TCP/IP Tools and Utilities"
- RFC 2305, "Simple Mode of Facsimile Using Mail"
- RFC 2328, "Shortest Path First (OSPF) Version 2"
- RFC 2368, "URL scheme"
- RFC 2373, "IP Version 6 Architecture"
- RFC 2396, "Uniform Resource Identifiers (URI): Syntax"
- RFC 2460, "Internet Protocol, Version 6 (IPv6) Specification"
- RFC 2535, "Domain Name Extensions"
- RFC 2616, "HyperText Transfer Protocol—HTTP/1.1"
- RFC 2660, "The HyperText Transfer Protocol"
- RFC 2821, "Simple Mail Transfer Protocol (SMTP)"
- RFC 2822, "Internet Message Format"
- RFC 2853, "Generic Security Version 2: Bindings"
- RFC 2854, "The 'text/html' Media Type"
- RFC 2865, "Remote Authentication Dial (RADIUS)"
- RFC 2870, "Root Name Server Operational Requirements"
- RFC 2871, "A Framework for Telephony over IP"
- RFC 2900, "Internet Official Standards"
- RFC 2910, "Protocol/1.1: Encoding and Transport"
- RFC 2911, "Protocol/1.1: Model and Semantics"
- RFC 3013, "Recommended Internet Provider Services and Procedures"
- RFC 3022, "Traditional IP Address Translator (NAT)"
- RFC 3076, "Canonical Version 1.0"
- RFC 3130, "Notes from the State-Technology: DNSSEC"
- RFC 3174, "US Hash Algorithm 1 (SHA1)"
- RFC 3196, "Protocol/1.1: Implementer's Guide"
- RFC 3275, "(Extensible Markup Language) XML-Signature Syntax and Processing"
- RFC 3330, "Special-Use IPv4 Addresses"
- RFC 3344, "IP Mobility Support for IPv4"

随着新技术的出现，RFC不断演进。如果你从事网络工作，应该关注 RFC 以监控新兴的网络协议。你可以在 http://www.faqs.org/rfcs/ 查看 RFC。

![](img/b418dfc0d37b54b9876d5e801170c507_176_0.png)

## 理解 IP 地址

当网络上有许多计算机时，你需要一种方法来唯一地标识每一个。在 TCP/IP 网络中，计算机的地址被称为 IP 地址。因为 TCP/IP 处理的是网络互连，所以地址基于网络地址和主机地址的概念。你可以将网络地址和主机地址的想法理解为提供两个地址来唯一标识计算机：

- 网络地址——指示计算机所在的网络。
- 主机地址——指示该网络上的特定计算机。
