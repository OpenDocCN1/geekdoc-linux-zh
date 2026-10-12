**Warning:** there is an added complication to all this. In different circumstances Windows sometimes regards a name either as a NetBIOS name or as a DNS name. The order above applies to NetBIOS names; for details of DNS name resolution order, see Appendix 22. (See also the note on NetBIOS v. “real” TCP/IP programs, Module 18.3.)

# How to specify which resolution methods to use

Windows-NT defaults to B-node. If you enable WINS, the type is set to H instead. To use something other than B or H types, you have to set the node type explicitly, either by using DHCP or by editing the Windows Registry (see Notes).

# Verifying name resolution order

You can easily use `tcpdump` or `ethereal` to check what’s happening on the wire by running the command `net view badxxx` on Dave, where the name **badxxx** isn’t configured anywhere, so the PC will try in turn every resolution method it’s configured to use. The figures below show what happens:

+   a. on B-node (i.e. no WINS)
+   b. on H-node (i.e. WINS server **bob** specified) but no DNS server numbers configured
+   c. on H-node, with DNS configured to use server Carol, and Control Panel > Network > Protocols > TCP/IP > Properties > WINS > Enable DNS for Windows Resolution = YES.

(We use `net use badxxx` instead of `ping badxxx` because of the difference between DNS and NetBIOS names mentioned above.)

(a)
| Time | Source | Destination | Protocol | Info |
|------|--------|-------------|----------|------|
| 0.00 dave |  | 132.0.2.127 | NBNS | Name query NB BADXXX |
| 0.74 dave |  | 132.0.2.127 | NBNS | Name query NB BADXXX |
| 1.49 dave |  | 132.0.2.127 | NBNS | Name query NB BADXXX |

(b)
| 0.00 dave | bob |  | NBNS | Name query NB BADXXX |
| 0.00 bob | dave |  | NBNS | Name query response |
| 0.00 bob | dave |  | NBNS | Name query NB BADXXX |
| 0.00 dave | 132.0.2.127 |  | NBNS | Name query NB BADXXX |
| 0.74 dave | 132.0.2.127 |  | NBNS | Name query NB BADXXX |
| 1.49 dave | 132.0.2.127 |  | NBNS | Name query NB BADXXX |

(c)
| 0.00 dave | bob |  | NBNS | Name query NB BADXXX | <20> |
| 0.00 bob | dave |  | NBNS | Name query response | <20> |
| 0.00 bob | dave |  | NBNS | Name query response | <20> |
| 0.00 bob | dave |  | NBNS | Name query response | <20> |
| 0.00 dave | 132.0.2.127 |  | NBNS | Name query NB BADXXX | <20> |
| 0.74 dave | 132.0.2.127 |  | NBNS | Name query NB BADXXX | <20> |
| 1.49 dave | 132.0.2.127 |  | NBNS | Name query NB BADXXX | <20> |
| 2.25 carol | dave |  | DNS | Standard query A badxxx.example.com | <20> |
| 2.30 carol | dave |  | DNS | Standard query response, Name error |  |
| 2.30 carol | dave |  | DNS | Standard query A badxxx.sales.example.com |  |
| 2.36 carol | dave |  | DNS | Standard query response, Name error |  |

As an exercise use `ping` instead of `net use` and see whether the order is different. Change your node type to M and see the effect.