# TCP/IP and Linux Protocol Implementation

Figure 6.146 ICMP, router requirement conformance: linux/net/ipv4/icmp.c.

+   * 4.3.2.8 (Rate Limiting)
* SHOULD be able to limit error message rate (OK)
* SHOULD allow extending of rate limits (OK, in the source)
* SHOULD send them
* 4.3.3.1 (Destination Unreachable)
* All the rules govern the IP layer, and are dealt with in i.p. not here.
* 4.3.3.2 (Redirect)
* MAY ignore ICMP Redirects if running a routing protocol or if forwarding
* is enabled on the interface (OK -- ignores)
* 4.3.3.3 (Source Quench)
* SHOULD NOT originate SQ messages (OK)
* MUST be able to limit SQ rate if originate them (OK as we don't
* them)
* MAY receive SQ messages (OK -- we don't)
* 4.3.3.4 (Time Exceeded)
* Requirements dealt with IP (generating TIME_EXCEEDED).
* 4.3.3.5 (Parameter Problem)
* MUST generate these for all errors not covered by other messages (OK)
* MUST include original value of the value pointed by (OK)

Figure 6.147 ICMP, router requirement conformance: linux/net/ipv4/icmp.c.

+   * 4.3.3.6 (Echo Request)
* MUST implement echo server function (OK)
* MUST process at ER of at least max(576, MTU) (OK)
* MAY reject broadcast/multicast ER (We don't, but that's OK)
* SHOULD have a config for silencing ER's (OK)
* MUST have a default value for the above = NO (OK)
* MUST have application layer interface for Echo Request/Reply (OK)
* MUST reply using same source address as the request was sent to.
* We'RE OK for uncertain ECM, and it doesn't say anything about
* how to handle broadcast ones, once its is optional.
* MUST copy data from Reply to Request (OK)
* MUST update Record Route / Timestamp (??)
* MUST use same source address for Reply if possible (NOT YET)
* 4.3.3.7 (Information Request/Reply)
* SHOULD NOT originate or respond to this (OK)
* 4.3.3.8 (Timestamp / Timestamp Reply)
* MAY implement (OK)
* MUST reply to every Timestamp message received (OK)
* MAY discard REQUESTS. (OK, but see for inconsistency)
* MUST reply using same source address as the request was sent to. (OK)
* MUST use reversed Source Reply if possible (NOT YET)
* SHOULD handle Record Route / Timestamp options (??)
* MUST pass REPLYs to transport/user layer (requires RAW, just like
CHO) (OK)
* MUST update clock for timestamp at least 16 times/sec (OK)
* MUST be 'correct within a few minutes (OK)
* 4.3.3.9 (Mask Request/Reply)
* MUST have support for receiving AMQ and responding with AMRe, (OK)
* but only as a compile-time option
* SHOULD have option for each interface for AMRe's, MUST default to