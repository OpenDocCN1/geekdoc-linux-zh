+   5. Given the scenario in question 4, how long would it take for other DCs within the head-quarters site to replicate the accounts belonging to the new users?
+   a. Replication occurs every 180 minutes by default.
+   b. Replication occurs at 15-minute intervals.
+   c. Replication occurs within 15 seconds of the account being added.
+   d. Replication occurs only between 12:00 AM and 6:00 AM.

+   6. What mechanism is used by an Active Directory domain controller to indicate that it has unreplcated changes to communicate to its replication partners?
+   a. Preferred bridgehead servers
+   b. Change notification
+   c. Site link bridges
+   d. intersite replication

+   7. When would you disable automatic site link bridging within Active Directory Sites and Services?
+   a. When you need to configure intersite replication
+   b. When you wish to configure different costs for your site links
+   c. When your physical network is not fully routed
+   d. When you wish to control the hours during which intersite replication will occur

+   8. To optimize client authentication and location of resources, which kind of object should each Active Directory site contain?
+   a. Site links
+   b. Costs
+   c. Connection objects
+   d. Subnets

+   9. Which of the following naming contexts are replicated across an entire Active Directory forest?
+   a. Configuration and Schema
+   b. Schema and DomainDNSZones
+   c. Configuration and ForestDNSZones
+   d. Schema and ForestDNSZones

+   10. When creating a site link, you can configure it to use which of the following protocols?
+   a. TCP/IP or RPC over IP
+   b. RPC over IP or SMTP
+   c. SMTP or TCP/IP
+   d. SMTP or CIDR

# ## Case Scenarios

# ### Scenario 3-1: Adding a New Site to a Network

Your company is located in the United States, and it has just added a location in Canada that will need to become part of your Active Directory network. Your network designer has provided you with the following configuration information regarding the new location servers and the connections that have been procured.

Three new servers will be installed in the Canada facility with the following specifications:

+   • Server 1: 2.4-GHz processor with 2 GB RAM will be installed as a domain controller.
+   • Server 2: 2.0-GHz processor with 1 GB RAM will be installed as a domain controller.
+   • Server 3: 2.0-GHz processor with 2 GB RAM will be installed as an application server.

Two links between the United States and Canada facilities will be available. They are as follows:

+   • A T-1 link for the primary connection
+   • A 256-Kbps link for a backup connection