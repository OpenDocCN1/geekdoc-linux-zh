cal interfaces with the same information as normal interfaces. This includes, for example, the interface (Figs) field codes.

Some of the packet totals displayed from **netstat** closely match the values obtained directly from the Linux SNMP agent known as **snmpd**. The **snmpd** program is an agent that supports MIB objects that correspond to objects reported by **netstat**. The MIB objects can be mapped to the **netstat** packet counter fields and are listed in Table 4.8. See Chapter 6, “Using SNMP Agents,” for more details regarding **snmpd** and the MIB objects listed.

**Table 4.8** *Linux agent MIB objects that map to* ***netstat*** *output*

| netstat Field | MIB Objects |
| --- | --- |
| RX-OK | IfInUcastPkts + IfInNUcastPkts |
| RX-ERR | IfInErrors |
| RX-DRP | IfInDiscards |
| TX-OK | IfOutUcastPkts + IfOutNUcastPkts |
| TX-ERR | IfOutErrors |
| TX-DRP | IfOutDiscards |

If the system has a large number of interfaces and you are only interested in a particular one, use the --**interfaces** command-line option to specify the one you want. Note that the online manual specifically describes this feature, but for some reason **netstat** ignores any interface command options.

# Display Routing Information

The system uses the routing table to determine the path that will be used to send IP packets to particular hosts or networks. Normally systems are configured with a default router so that routing decisions are straightforward and simple. However, there may be instances when a machine has more than one interface, and each is attached to a different IP network. In this case, the system might also be forwarding IP packets (routing) between these networks. As a result, the routing function becomes a bit more complex. As part of the overall routing system, a routing table is defined that