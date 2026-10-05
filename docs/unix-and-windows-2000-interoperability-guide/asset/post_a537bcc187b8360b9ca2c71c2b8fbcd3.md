
# Network Application Interfaces

![](img/1c1e7552b53cca888836b6c6895bdb48_84_0.png)

> Figure 5-1 Windows 2000 application programming interfaces. Both APIs use TCP and UDP. From Microsoft Windows 2000 Server TCP/IP Core Networking Guide, p. 17.

NetBT utilizes a different name resolution scheme, employing things as broadcasts, LMHOSTS files, and the Windows Internet Naming Service (WINS). Therefore, you need to manage both WinSock and NetBIOS name resolution in a Windows-based network. However, as stated in Chapter 2, the Windows 2000 workstation and server services support direct host hosting—but for computers running Windows 2000 only. With direct hosting, clients use DNS to resolve names and send communication to TCP port 445 (where NetBIOS session communication normally takes places).

## 5.3.2 HP-UX

As late as version 10.20, HP-UX TCP/IP is Berkeley sockets-based. In version 11, it is now STEAMS-based. Uresh Vahalia, in UNIX Internals: The Frontiers. (Prentice Hall, 1996), p. 548, describes it: "A stream is a full-duplex processing and data transfer path between a driver in kernel space and a process in user space. STEAMS is a collection of system calls, kernel resources, and kernel utility routines that create, use, and dismantle a stream."

STREAMS-based network applications resolve host names and IP addresses, using either a HOSTS file, DNS, Network Information Services (NIS), or a combination of all three. There is no need to use WINS or the equivalent of an LMHOSTS file unless you install a product such as Hewlett-Packard’s Advanced Server/9000, which installs NetBIOS into the kernel.

## 5.4 Conclusion

We looked at the two protocols found at the transport layer of the TCP/IP protocol suite: the connection-oriented TCP and the connectionless UDP. You can tune TCP parameters in both HP-UX and Windows 2000, though exactly which ones depends on the operating system. NFS and NetBIOS have used UDP extensively for years, though the trend is toward TCP. Network APIs for Windows 2000 include WinSock and NetBIOS. HP-UX has transitioned from Berkeley sockets to STREAMS.

## References

- 1. Thomas Lee and Joseph Davies, Microsoft Windows 2000 TCP/IP Protocols and Services Technical Reference. (Microsoft Press, 2000).
- 2. Microsoft Corporation, Microsoft Windows 2000 Server TCP/IP Core Networking Guide. (Microsoft Press, 2000).
- 3. Uresh Vahalia, UNIX Internals: The New Frontiers. (Prentice Hall, 1996).

# Name Resolution

As stated in Chapter 5. "The Transport Layer." Windows 2000 networking services are NetBIOS-based. Traditionally, this has required using the NetBIOS name cache, LMHOSTS files, and WINS to resolve NetBIOS computer and service names to IP addresses. Beginning with Windows 2000, such entities are not necessary as long as you have Windows 2000 systems in your network. As of this writing, though, a Windows 2000-only network is unlikely, not to mention that this book assumes you have UNIX-based clients and servers running in your enterprise. Pre-Windows 2000 systems and the tools that make UNIX interoperable with Windows systems currently use NetBIOS. Therefore, it is highly likely that you will continue to have to manage both NetBIOS name resolution and TCP/IP host resolution.

## 6.1 Windows 2000

### 6.1.1 Computer Names

A Windows 2000 full computer name is the same thing as a fully qualified domain name (FQDN). An FQDN consists of a host name plus the primary DNS suffix. These can be set when you install the system or by right-clicking on My Computer, choosing Properties, and then clicking on the Network Identification tab. Click on the Properties button and you will see the Identification Changes Box, like the one in Figure 6–1.

# Identification Changes.

![](img/1c1e7552b53cca888836b6c6895bdb48_87_0.png)

Figure 6–1 Setting the host name. In this example, the full computer name is the host name followed by a period. The primary DNS suffix has not been set. Clicking on the More... button enables you to set it.

Filling in the Computer name: box sets the host name. If you want to set the primary DNS suffix, click on the More... button. You will get the DNS Suffix and NetBIOS Computer Name box. See Figure 6–2.

![](img/1c1e7552b53cca888836b6c6895bdb48_87_1.png)

Figure 6–2 Setting the primary DNS suffix. This box enables you to set the primary DNS suffix, which combined with the host name, creates the full computer name. The NetBIOS computer name defaults to the host name and is provided to enable communication with pre-Windows 2000 systems.

# Windows 2000

However, you can have more than one FQDN for a system, because Windows 20 allows you to have a different DNS suffix for each.

## 6.1.2 Lookup DNS

Windows 2000 departs from the tradition of going through NetBIOS. Instead, it works the other way: it first checks DNS.

When a user uses an application like Ping, it calls the gethostaddr() function, which:

1. Checks the local HOSTS file.
2. Queries DNS.
3. If all else fails, it uses NetBIOS.

Server TCP/IP Core Networking Guide, pp. 338–339

The Windows 2000 resolver caches information received from a DNS query, be it positive (host found) or negative (host name not found). After undergoing name transformation as previously described, if needed, all queries first go through this cache. The DNS cache also contains the entries in the HOSTS file, loaded automatically upon system startup.

## 6.1.3 Windows 2000 Resolver

The first step the Windows 2000 resolver takes is to determine what kind of name is being submitted. Name types include:

- FQDNs: These are names terminated with a period (for example, mysystem.com). These names are immediately submitted to DNS.
- Multiple-label, unqualified domain names: These either look like FQDNs without a terminating period (for example, mysystem) or incomplete FQDNs (for example, mysystem). In the former, the resolver appends a period to create an FQDN and then submits it. In the latter, it appends DNS suffixes (specifiable by the user) and submits each to DNS.
- Single-label, unqualified domain names: These are simply host names (for example, mysystem). In this case, the resolver appends DNS suffixes in the manner described in the previous bullet until resolution succeeds.

For both types of unqualified domain names, the DHCP server can set the primary DNS suffix and the connection-specific DNS suffix. The DNS name resolution process can be quite complex. For more information, including some excellent flow charts illustrating the process, see the Microsoft Windows 2000 Server TCP/IP Core Networking Guide, pp. 344–354.
