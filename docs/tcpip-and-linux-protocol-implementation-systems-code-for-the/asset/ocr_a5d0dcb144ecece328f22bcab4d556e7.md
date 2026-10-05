# TCP/IP and Linux Protocol Implementation

+   * when sending ICMP errors. (OBSOLETE) -- RFC 1812
* MUST pass ICMP errors up to protocol level. (OK)
* SHOULD send ICMP errors with TOS = 0. (OBSOLETE -- RFC 1812)
* MUST NOT send ICMP errors in reply:
* ICMP errors (OK)
* Broadcast/multicast datagrams (OK)
* MAC broadcasts (OK)
* Non-initial fragments (OK)
* Datagram with a source address that isn't a single host. (OK)
* 3.2.2.1 (Destination Unreachable)
* All the rules govern the IP layer, and are dealt with in ip.c, not here.
* 3.2.2.2 (Redirect)
* Host NOT send ICMP_REDICTS. (OK)
* MUST update routing table in response to host or network redirects.
* (Host OK, network OBSOLETE)
* SHOULD drop redirects if they're not from directly connected gateway
* (OK -- we drop it it's not from our old gateway, which is close enough

Figure 6.144 ICMP, host reinforcement conformance: linux/net/ipv4/icmp.

+   * 3.2.2.3 (Source Quench)
* MUST pass incoming SOURCE_QUENCHs to transport layer (OK)
* Other requirements are dealt with at the transport layer.
* 3.2.2.4 (Time_EXCEEDED)
* MUST pass TIME_EXCEEDED to transport layer (OK)
* Other requirements are dealt with at IP (generating TIME_EXCEEDED).
* 3.2.2.5 (Parameter Problem)
* SHOULD generate these (OK)
* MUST pass received PARAPPROBLEM to transport layer (NOT YET)
* [Solaris 2.X seems to assert EPROTO when this occurs] -- AC
* 3.2.2.6 (Echo Request/Reply)
* MUST reply to ECHO_REQUEST, and give app to do ECHO stuff (OK. Configurable with a sysctl1.)
* MUST reply using same source address as the request was sent to.
* We're OK for unicast ECHOs, and it doesn't say anything about
* how to handle broadcast ones, since it's optional.
* MUST copy data from REPLY to REPLY (OK)
* unless it would require illegal fragmentation (OK)
* MUST pass REPLIES to transport/user layer (OK)
* MUST use any provided source (reversed) for REPLY. (NOT YET)
* 3.2.2.7 (Information Request)
* MUST implement this. (I guess that means silently discarded...?) (OK)
* 3.2.2.8 (Timestamp Request/Reply)
* MAY implement (OK)
* SHOULD be in-kernel for "minimum variability" (OK)
* MAY discard broadcast REQUESTS. OK, but see for inconsistency)
* MUST reply using same source address as the request was sent to. (OK as per ECHO (NOT YET))
* MUST pass REPLIES to transport/user layer (requires RAW, just like ECHO (OK))
* MUST update clock for timestamp at least 15 times/sec (OK)