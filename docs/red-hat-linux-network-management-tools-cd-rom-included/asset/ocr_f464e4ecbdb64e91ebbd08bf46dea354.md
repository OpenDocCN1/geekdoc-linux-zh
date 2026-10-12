1.

34



**OID:**

*ipRouteEntry.12*

**Object Type:**

*Integer*

**Access Mode:**

*read-write*

**Description:**

An alternate routing metric for this route

**Object Name:**

*ipRouteInfo*

**OID:**

*ipRouteEntry.13*

**Object Type:**

*Object Identifier*

**Access Mode:**

*read-only*

**Description:**

The MIB definition reference to the routing protocol responsible for this route

The *ipNetToMediaTable* table is an address translation table that contains entries that correspond to IP addresses and physical addresses. Figure 6.8 shows the tree view of this table.

![](bbox=[0.187, 0.561, 0.631, 0.727])

**Figure 6.8**

*The ipNetToMediaTable table view.*

The information contained within this table is basically the same as that of the *at* table. The only difference is the *ipNetToMediaType* object, which lists the type of mapping used.

**Object Name:**

*ipNetToMediaIfIndex*

**OID:**

*ipNetToMediaEntry.1*

6