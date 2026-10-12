# ## 6.6 Dividing your network into sub-nets – motivation

We mentioned in Module 4.3 that TCP/IP was extended from the old A/B/C address classes to support *sub-nets*. There are many reasons why you might want to sub-divide a single network:

+   1. performance reasons: to limit the number of broadcasts on a given segment, or to limit traffic, e.g. between this file server and its clients (Figure 6.12). However, with UTP switches, this is not as significant as in the days of Thick Ethernet and ThinNet. (In the early days of switches, when they were very expensive, you would often use a switch only on the backbone – to speed up traffic between the segments, as this often involved heavy server-to-server traffic – but still use hubs on the individual sub-networks because they were cheaper.)

+   2. physical limitations on the cable length in a single network segment (although again this is not so significant with UTP cabling, hubs/switches.)

+   3. to accommodate different physical networking technologies (e.g. Ethernet, point-to-point for remote small offices, Token Ring). A mixture of different network hardware is especially common when companies merge

+   4. you have several branches. Each office's own LAN forms a separate sub-net and the only traffic that leaves a branch sub-net is traffic intended for a different branch. The network diagram will be identical to that in Figure 6.12, but the backbone will be linking separate geographical branches instead of departments within the same building.

+   5. flexibility in configuring your internal network layout, by hiding the structure of your internal network from the rest of the world. For example, if your external address range is a single class B, external routers need only a single routing table entry for your entire site. Internally, you can divide the network however you want, and change the internal layout of routers and network segments without having to inform the external world. (Without sub-netting, you might have dozens of class-C addresses, say, all of which have to be known to external routers, giving larger routing tables and reducing your internal flexibility.)

+   6. to divide your network to match your geographical and administrative organization. This is similar to sub-netting by branch but you may have several levels of hierarchy. For example, you might organize your sub-networks as follows:

+   -   human resources department
+   -   operations department
+       -   operations, sub-net for sales
+       -   operations, sub-net for technical
+   -   finance department

with responsibility and administration for each sub-net delegated locally. Your organizational units can hide internal changes from the company network as a whole, in just the same way as changes on your overall site are insulated from the Internet. Delegation in this way has proven to work very well on the Internet, for administration of DNS, e-mail, etc.