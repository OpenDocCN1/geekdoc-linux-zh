```
| | | | | | | [1] authIpAddress* |
| | | | | | | [2] authTime |
| | | | | | | [3] authCommunityName |
| | | | | | [17] openView |
| | | | | | | [2] openViewTrapVars |
| | | | | | | [1] openViewSourceId |
| | | | | | | [2] openViewSourceName |
| | | | | | | [3] openViewObjectId |
| | | | | | | [4] openViewData |
| | | | | | | [5] openViewSeverity |
| | | | | | | [6] openViewCategory |
| | | | | | | [7] openViewFilter |
| | | | | | | [8] openViewEntity |
| | | | | | | [9] openViewAddress |
| | | | | | | [10] openViewPpid |
| | | | | | [1] hpOpenView
```

# **Monitoring Notes**

The mnemonic root OID for the HP-UNIX MIB is *iso.org.dod.internet.private.enterprises.hp.nm*. If you intend to write your own SNMP application, you need to know the numeric root OID of the HP-UNIX MIB is 1.3.6.1.4.1.11.2.

HP’s EMS HA Monitors product uses this MIB to monitor the current number of users and jobs on a system and the amount of free filesystem space.

This MIB can be a useful place to find information about the specific processes running on a system, such as their CPU utilization, priority, and resident set size. However, you may have a difficult time using a MIB Browser to wade through the numerous process table entries; this information is best queried from a customized SNMP application.

Note that this MIB contains information on NFS diskless clusters, but not on HP’s high availability or EPS clusters. Information on these clusters is provided in the following sections.

# **HP Cluster MIB**

The HP Cluster MIB is a private MIB provided by Hewlett-Packard. It defines cluster membership information for the high availability and EPS clusters.

# **MIB Definition**

Listing A-7 shows the complete specification for the HP Cluster MIB, as defined by Hewlett-Packard.