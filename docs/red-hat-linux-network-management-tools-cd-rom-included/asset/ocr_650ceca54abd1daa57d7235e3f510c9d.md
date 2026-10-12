probing an agent for specific information or learning the structure and format of new MIBs.

![](bbox=[0.06, 0.15, 0.95, 0.47])

**Figure 2.3** *MIB browser*.

The MIB Browser window contains several sections, as shown in Figure 2.3. The first panel provides a hierarchical view of MIBs that can be used to *navigate* to the desired MIB object or branch. The next panel shows detailed information regarding the object. The third shows the value obtained from the MIB object specified. More detailed information regarding this tool can be found in Chapter 8, "SNMP Tools."

# Object Types

Within an MIB, different object types represent data structures or values contained in an agent. The objects can represent physical agent attributes, configuration information, or other data. These object types are derived from the Abstract Syntax Notation (ASN.1) standard rules. ASN.1 provides a detailed mechanism for the implementation and encoding of basic data types that are machine-independent and can be transmitted over the network in an unambiguous way.

Why is this important to SNMP or network management? Because network management must address a heterogeneous net-