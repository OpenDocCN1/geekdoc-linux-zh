Further, when devices, such as SNMPv1 devices, that don’t support MIB views are queried, and the same command is executed on a device called `dips`, we get the following:

```
`Timeout: No Response from dips`
```

This error message is displayed for the following reason: When the community string doesn’t match the password configured within it, an SNMPv1 agent disregards the request. If authentication traps are enabled, it then sends the associated trap. The important thing to remember is that when polling for specific objects, don’t assume that objects are not available despite the generation of error messages suggesting that they are unavailable. It might be helpful to execute an **snmpwalk** against the agent if questions come up regarding which objects are indeed supported by the agent.

# ## Snmpgetnext Tool

The **snmpgetnext** command retrieves one or more MIB objects using SNMP query requests. For each object specified on the command line, **snmpgetnext** gets the next lexicographical MIB object found in the MIB tree. This tool is very useful for returning a series of objects when the exact structure of the MIB object that is being retrieved is unknown. Also, it permits the discovery of the structure of a MIB view dynamically. For example, the command:

```
`# snmpgetnext probe public system.SysContact.0`
```

will obtain the next MIB object after the **sysContact.0** object:

```
`system.sysName.0 = "AXON" Hex: 41 5B 4F 4E`
```

The **sysName.0** object is displayed because it is *lexicographically next* to the **sysContact.0** object. How do we know this for sure? Well, the simplest approach is to display the entire **system** group. An **snmpwalk** of the group displays the following:

```
`system.sysDescr.0 = "AXON LANServant - Ethernet (4.1.6)"
system.sysObjectID.0 = OID: enterprises.370.2.2
system.sysUpTime.0 = Timeticks: (868306) 2:24:43.06
system.sysContact.0 = "3Com Corporation"
system.sysName.0 = "AXON" Hex: 41 5B 4F 4E
system.sysLocation.0 = " "
system.sysServices.0 = 15`
```