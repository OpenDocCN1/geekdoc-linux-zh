# # Working with Active Directory Sites

# OBJECTIVE DOMAIN MATRIX

| TECHNOLOGY SKILL | OBJECTIVE DOMAIN | OBJECTIVE DOMAIN NUMBER |
|---|---|---|
| Introducing Active Directory Sites | Configure sites. | 2.3 |
| Configuring Active Directory Replication | Configure Active Directory replication. | 2.4 |

# KEY TERMS

+   - asynchronous replication
+   - bridgehead server
+   - change notification
+   - Classless Inter-Domain Routing (CIDR)
+   - compressed
+   - connection objects
+   - convergence
+   - cost
+   - dcdiag
+   - dual counter-rotating ring
+   - frequency
+   - intersite replication
+   - Intersite Topology Generator (ISTG)
+   - intrasite replication
+   - linked-value replication (LVR)
+   - preferred bridgehead servers
+   - Remote Procedure Calls over Internet Protocol (RPC over IP)
+   - repadmin
+   - replication partners
+   - replication topology
+   - schedule
+   - Simple Mail Transport Protocol (SMTP)
+   - site link
+   - bridge
+   - timesstamp
+   - transitive
+   - update sequence number (USN)
+   - urgent replication
+   - version ID
+   - well-connected

Woodgrove Bank is a mid-sized community bank in the northeastern United States that is in the process of expanding its branch locations by acquiring smaller banks in nearby areas. Woodgrove Bank relies on Active Directory to provide a single authentication store for its current assets, and it is in the process of migrating its new acquisitions into its existing Active Directory to provide a streamlined logon experience. To manage band-width usage between Woodgrove’s corporate headquarters and its new acquisitions, its Active Directory design team has created multiple Active Directory sites to control how replication traffic is transmitted between locations.

After completing this lesson, you will have a firm understanding of the Active Directory replication process, which is used to communicate changes from one domain controller to all other domain controllers in a domain or forest. You will be able to discuss the differ-ences between intrasite replication, which takes place within a single well-connected location, and intersite replication, which allows Active Directory changes to be communicated across WAN links to remote locations. You will understand how to implement a plan for creating and managing Active Directory sites as well as managing and monitoring the AD replication process. Because Active Directory Domain Services allows updates to the Active Directory database to be made from any writable domain controller, replication is a key concept in maintaining a healthy and functional Active Directory environment.