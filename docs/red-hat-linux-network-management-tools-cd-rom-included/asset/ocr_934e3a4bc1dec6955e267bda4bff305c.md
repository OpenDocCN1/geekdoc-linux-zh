```
# snmpwalk cisco-gw5 public .1 > walk.out
```

This command uses the .1 as the starting point to begin listing objects. Doing this will ensure that every object will be displayed because .1 is the root of the entire MIB tree and all objects are accessible from this point. Walking the entire MIB tree with an agent will help identify certain MIB objects or give you an idea of exactly how many objects a particular agent may support. To see the approximate number of objects the cisco-gw5 supports, count the number of lines in the file. Because the snmpwalk command displays each MIB object on its own line (unless the line is longer than the maximum number of characters for a line), we can then use the UNIX wc command to total the number of lines within the walk.out file. Thus, the command

```
# wc -l walk.out
```

produces the following output:

```
2242 walk.out
```

This command output shows that the agent contained within the cisco-gw5 device supports roughly 2242 MIB objects. When no object is specified with the snmpwalk command, it will search the MIB-II object tree by default. When the snmpwalk command reaches the end of the MIB within the agent, it will display the message End of MIB.

Note that the use of snmpwalk is a rather inefficient means to obtain a large number of MIB objects from an agent. This is because the command continuously queries a single MIB object to obtain an associated value. It is recommended that the snmpbulkwalk command be used whenever possible to reduce network traffic and load on the agent system. This command significantly reduces the work involved for a lower level to obtain a large amount of information from an agent. See the snmpbulkwalk section for additional information.

# Snmppbulkwalk Tool

The snmpbulkwalk tool communicates with a network entity using SNMPv2 bulk-request. Like the snmpwalk tool, snmpbulkwalk will