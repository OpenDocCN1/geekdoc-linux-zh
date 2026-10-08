# Appendix A

# Standards

# Using SNMP and MIBs

Simple Network Management Protocol (SNMP) is a standard protocol used for communication between a system being managed and a management application. SNMP, introduced in the 1980s, is now the de facto standard for the communication of management information. Although initially SNMP was used only to manage network components, such as routers, bridges, and hubs, it is now used for systems, software applications, and middleware products as well.

SNMP *subagents* are the processes responsible for the management of different system components. SNMP communication from a management station is forwarded to the appropriate subagent by a *master agent* process on the system being managed. SNMP communication is sent over the User Datagram Protocol (UDP). The master agent listens for requests on a well-known UDP port (161), decodes the requests, and forwards them to the appropriate subagent. Each subagent registers with the master agent at startup and indicates the requests that should be forwarded to it. The master agent also sends traps on behalf of a subagent. Figure A-1 shows all SNMP traffic going through the master agent, to or from the subagents on the system. On HP-UX, the master agent is provided through EMANATE technology, licensed from SNMP Research International, Inc. More information about EMANATE can be found at http://www.snmp.com.

SNMP subagents represent the management information that they supply in the form of a hierarchical structure called a *Management Information Base (MIB)*. Figure A-2 shows how the individual MIBs, MIB-II and RDBMS MIB, fit into the overall MIB hierarchy. MIB Browsers are often included with enterprise management frameworks, such as HP OpenView Network Node Manager. These graphical tools can allow operators to navigate the MIB tree structure, to look for specific management information. In addition to showing the MIB Object Identifier (OID), the MIB Browser typically also shows the value of the MIB object. The MIB Browser uses SNMP requests to query the subagent for the MIB values on the managed system.

Names, as well as numeric values, are assigned with each component of the MIB OIDs. For example, the MIB-II is a standard MIB for system information with a root OID of