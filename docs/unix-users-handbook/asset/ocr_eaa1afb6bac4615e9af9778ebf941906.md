![](bbox=[0.08, 0.1, 0.92, 0.45])

These systems are connected to the same subnet, even though part of the third byte, normally associated with the subnet, is used for the host ID. In the future, the subnet mask could be changed to 255.255.252.0 and have four separate subnets of 12, 13, 14, and 15. This arrangement would require putting routers in place to route to these separate subnets.
Let’s now switch to the high level and look at some networking functionality.

# Using Networking

The ISO/OSI model is helpful for visualizing the way in which the networking layers interact. The model does not, however, tell you how to use the networking. Two widely used networking services that may be running on your system(s) and are worth taking a look at are ARPA and NFS.
The first networking product to try on your system is what is sometimes called ARPA Services - what I have been calling ARPA.