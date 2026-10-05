# SNMP organization

881

Before we dive into the gritty details of SNMP, we should note that the terminology associated with it is some of the most wretched technobabble to be found in the networking arena. The standard names for SNMP concepts and objects actually lead you away from an understanding of what's going on. The people responsible for this state of affairs should have their keyboards smashed.

# SNMP organization

SNMP data is arranged in a standardized hierarchy. This enforced organization allows the data space to remain both universal and extensible, at least in theory. Large portions are set aside for future expansion, and vendor-specific additions are localized to prevent conflicts. The naming hierarchy is made up of "Management Information Bases (MIBs), structured text files that describe the data accesses through SNMP. MIBs contain descriptions of specific data variables, which are referred to with names known as object identifiers, or OIDs.

Translated into English, this means that SNMP defines a hierarchical namespace of variables whose values are tied to "interesting" parameters of the system. An OID is just a way of naming a specific piece of information.

The SNMP hierarchy is much like a filesystem. However, a dot is used as the separator character and each node is a number rather than a name. By convention, nodes are also given names for ease of reference, but this naming is really just a high-level convenience and not a feature of the hierarchy. (It is similar in principle to the mapping of hostnames to IP addresses)

For example, the OID that refers to the uptime of the system is 1.3.6.2.1.1.3. ThisID is also known by the human-readable (though not necessarily "human-readable without additional documentation") name

```
iso.org.dod.internet.mgmt.mib-2.system.sysTime
```

The top levels of the SNMP hierarchy are political artifacts and generally do not contain useful data. In fact, useful data can only be found beneath the OID iso.org.dod.internet.mgmt (numerically, 1.3.6.1.2).

The basic MIB for TCP/IP (MIB-1) defines access to common management data: information about the system, its interfaces, address translation, and protocol operations (IP, ICMP, TCP, UDP, and others). A later and more complete reworking of this MIB (called MIB-II) is defined in RFC1213. Most vendors provide an SNMP server support MIB-II. Table 21.1 on the next page presents a sampling of nodes from the MIB-II namespace.

In addition to the basic MIB, there are MIBs for various kinds of hardware interfaces and protocols, MIBs for particular hardware products.

A MIB is only a schema for management data. To be useful, a MIB must be backed up with agent-side code that maps between the SNMP namespace and the device's actual state. SNMP agents that run on UNIX, Linux, or Windows