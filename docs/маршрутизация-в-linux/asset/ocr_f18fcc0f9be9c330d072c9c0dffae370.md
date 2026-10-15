# Multi-Protocol, Multicast Routing with the Multicast gated

> The multicast version of gated (www.gated.org) handles PIM-SM, Protocol Independent Multicast-Dense Mode (PIM-DM), DVMRP, and Multicast Source Discover Protocol (MSDP) all in a single program. It's not featured in this chapter because it's not freely available, but for many this program is worth the cost. This is especially true if you need to run more than one multicast program, which you might just need to do. The reasons for this are discussed in the section, "The DVMRP Linux Daemon: mrouted."

# Configuring pimd

Since pimd is a single-function daemon, the configuration is really not that complex—at least when compared to a monster tool such as gated. The configuration data is kept in the file /etc/pimd.conf. While the order of the statements does not have to strictly follow what is about to be presented, I'll walk you through the contents you might want to add to this file.

The /etc/pimd.conf file begins with the following statement:
default_source_preference value

Routers hold elections to determine which gets to be a site's upstream router. Because pimd is such a focused tool, you generally don't want it to win over something more general. Using a value of 101 here is a minimum for making sure that gated and other routing tools are going to win the election and leave pimd to do its PIM-SM handling. The next line is
default_source_metric value

This item sets the cost for sending data through this router. You want only PIM-SM data to go to this daemon; so once again, a high value is recommended to prevent accidental usage. The preferred default value is 1024.

Though you can swap the first two statements around, you must have the next statement after you set default_source_metric. This item starts with
phyint interface

phyint refers to physical interface. You fill in Interface with a reference to the ethernet card or other network interface you're telling pimd about, either with the device's IP address or name (for example, eth0). If you just want to activate this interface with default values, you don't need to put anything else on the line. However, you do have some additional items you can add. The items are, in the order you would need to use them, as follows:

+   - disable Do not send PIM-SM traffic through this interface nor listen for PIM-SM traffic from this interface.
+   - preference pref. This interface's value in an election. It will have the default_source_preference if not assigned.
+   - metric cost. The cost of sending data through this interface. It will have the default_source_metric if not assigned.