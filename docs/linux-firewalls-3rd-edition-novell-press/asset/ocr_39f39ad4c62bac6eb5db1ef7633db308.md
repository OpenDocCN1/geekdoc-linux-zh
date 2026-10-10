# TABLE 3.19
TOS Match Extension

| `-m | --match tos OPTION` | DESCRIPTION |
|---|---|
| `--tos <value>` | Matches on the IP TOS setting |

The tos value can be one of either the string or numeric values:

+   minimize-delay, 16, 0x10
+   maximize-throughput, 8, 0x08
+   maximize-reliability, 4, 0x04
+   minimize-cost, 2, 0x02
+   normal-service, 0, 0x00

# THE VALUE OF TOS BITS

> The TOS bits are of historical interest only. Linux does support their use locally, and various Linux firewall documents refer to the bits and their uses. Nevertheless, the fact remains that the TOS bits are not used or examined generally.

The TOS field has been redefined as the Differentiated Services (DS) field for use by the Differentiated Services Control Protocol (DSCP).

For more information on Differentiated Services, see these sources:

+   RFC 2474, "Definition of the Differentiated Services Field (DS Field) in the IPv4 and IPv6 Headers"
+   RFC 2475, "An Architecture for Differentiated Services"
+   RFC 2990, "Next Steps for the IP QoS Architecture"
+   RFC 3168, "The Addition of Explicit Congestion Notification (ECN) to IP"
+   RFC 3260, "New Terminology and Clarifications for DiffServ"

# unclean filter TABLE MATCH EXTENSION

The specific packet-validity checks performed by the unclean module are not documented. The module is considered to be experimental, and the iptables authors recommend against its use for now.