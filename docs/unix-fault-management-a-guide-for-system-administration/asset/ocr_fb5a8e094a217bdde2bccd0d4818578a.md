MC/ServiceGuard detects numerous cluster events, such as the failure of a critical application. These events can be forwarded to a management station by using either SNMP traps or openmsg, a proprietary communication mechanism used by IT/O. Information about an MC/ServiceGuard cluster is stored in the HP Cluster and HP MC/ServiceGuard Cluster MIBs. These Cluster MIBs are listed in Appendix A. The following is a list of the MC/ServiceGuard events that trigger SNMP traps from the MC/ServiceGuard subagent:

+   - MC/ServiceGuard subagent was started
- MC/ServiceGuard cluster is reforming
- MC/ServiceGuard cluster is up on this node
- MC/ServiceGuard cluster is down on this node
- MC/ServiceGuard cluster configuration has changed
- MC/ServiceGuard package is starting
- MC/ServiceGuard package is running
- MC/ServiceGuard package is halting
- MC/ServiceGuard package is down
- MC/ServiceGuard service is down
- MC/ServiceGuard package switching flags have changed
- MC/ServiceGuard relocatable IP address added
- MC/ServiceGuard relocatable IP address removed
- MC/ServiceGuard network interface local switch
- MC/ServiceGuard subnet is up
- MC/ServiceGuard subnet is unavailable
- MC/ServiceGuard node joined the cluster
- MC/ServiceGuard node has halted
- MC/ServiceGuard node has failed

MC/ServiceGuard software detects a variety of error conditions, but it does not have a sophisticated notification mechanism for customers to learn what happened. Errors often are written to the system log, which can be used to help retrace what occurred.

Whereas MC/ServiceGuard can monitor the system, network, and processes and provide automatic recovery, ClusterView provides you with event notification of these recovery events. For example, if MC/ServiceGuard detects a local LAN card failure, it can reconfigure the IP connectivity on a backup LAN card on the local system transparently. Using ClusterView, you will see an event indicating that MC/ServiceGuard has performed a local switch to a backup LAN card. The bad LAN card should be replaced, to eliminate the LAN card as a single point of failure.

ClusterView can be used to help you with diagnosis in MC/ServiceGuard environments. ClusterView is an OpenView application with custom monitoring capabilities for MC/ServiceGuard and MC/LockManager clusters. An SNMP subagent that can be used to send events to an OpenView management station is included with the MC/ServiceGuard and MC/LockManager