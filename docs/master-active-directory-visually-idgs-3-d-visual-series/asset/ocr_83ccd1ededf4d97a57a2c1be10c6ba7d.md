# # UNDERSTANDING REPLICATION PARTITIONS

Active Directory replication occurs at three major levels of the Active Directory. Understanding how replication occurs at these levels is important because replication can have an impact on designing an Active Directory environment. The following sections examine each of the replication partitions.

other words, the Schema (which you can learn more about in Chapter 27) contains metadata that determines what can be stored in the Active Directory and how the metadata is defined. The Active Directory Schema applies to the entire enterprise. In other words, schema changes are replicated to the fullest extent of your Active Directory environment, whether that be a tree or forest. An enterprise contains only schema that is exactly the same in all domains, trees, and forests in the environment.

# **Schema partition**

The Schema partition contains definitions for objects, classes of objects, and the attributes for each object. In

# ## Total Active Directory Environment

![](bbox=[0.24, 0.54, 0.78, 0.6])

# **Configuration partition**

The Configuration partition contains information about the physical design of the Active Directory: This includes your sites and domains and where domain

controllers physically reside on the network. Configuration replication applies to the entire enterprise and is sent to all domain controllers in every domain, tree, and forest.

# ## Total Active Directory Environment

![](bbox=[0.24, 0.8, 0.78, 0.94])