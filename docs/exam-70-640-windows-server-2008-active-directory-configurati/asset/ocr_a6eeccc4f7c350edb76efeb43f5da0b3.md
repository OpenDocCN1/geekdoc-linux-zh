72 | Lesson 3

3. From the list of transports on the left side, choose the appropriate protocol for replication, and then click Add. The protocol will appear on the right side, showing that this server will be added to the list of Preferred Bridgehead Servers for the chosen protocol.

PAUSE. LEAVE the Sites and Services MMC snap-in open to complete the next exercise.

A site link bridge defines a chain of site links by which domain controllers from different sites can communicate. In the case where there is a centralized site that connects two branch sites via site links, the site link bridge creates a direct link between the branch sites using the total cost of both site links to the central site.

All site links that use the same transport protocol are considered to be transitive by default, which means that a domain controller in any site can connect to a domain controller in any other site by navigating a chain of site links. In a fully routed IP network, this feature generally follows your routing topology. The ISTG uses this information when creating the replication topology to automatically bridge all site links, thereby allowing two or more sites to replicate in any direction using this automatic site link bridging. However, if your network is not fully routed, it is recommended that you disable automatic site link bridging and instead configure manual site link bridges according to your network infrastructure. This allows the ISTG to create paths that are most appropriate for your topology and link speeds. The following situations warrant the manual creation of site link bridges:

+   * When your network is not fully routed, manually created site link bridges allow better performance by creating a shortcut between sites that are not directly connected.
+   * If there are many sites and the forest functional level has not been raised to the Windows Server 2003 forest level or better, creating manual site link bridges may be necessary to prevent the ISTG from becoming overloaded.

# CONFIGURING MANUAL SITE LINK BRIDGING

Site link bridging is enabled by default and works well in a fully routed network. However, disabling site link bridging in a network that is not fully connected will allow you to create the site links according to your network infrastructure or business guidelines.

# DISABLE AUTOMATIC SITE LINK BRIDGING

GET READY. Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed.

+   1. In Active Directory Sites and Services, expand the Inter-Site Transports folder.
+   2. Right-click the protocol you wish to configure and select Properties.
+   3. Remove the checkmark next to the Bridge All Site Links checkbox and click Ok.

PAUSE. LEAVE the Sites and Services MMC snap-in open to complete the next exercise.

In the previous exercise, you disabled automatic site link bridging within the Active Directory Sites and Services MMC snap-in. The next step in this situation would be to create one or more manual site link bridges to match the topology of your physical network.

# CREATE A MANUAL SITE LINK BRIDGE

GET READY. Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed. Be sure that you have disabled automatic site link bridging, as described in the previous exercise.

+   1. In Active Directory Sites and Services, expand the Inter-Site Transports folder.
+   2. Right-click the protocol you wish to bridge and select New Site Link Bridge.