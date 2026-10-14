# 12.3 Hardware Management Revisited

In a cluster, hardware management is by and large unchanged from a standalone system, but then again, the way that hardware is handled in Tru64 UNIX (starting with version 5.0) was redesigned specifically to accommodate two things:

+   - Multiple paths to storage devices.
+   - TruCluster Server.

However, a few things have changed, and we thought that it would be a good idea to let you in on the differences.

# 12.3.1 Hardware Management Databases Revisited

The first minor change that occurs when the cluster is created is that some of the hardware databases that were previously located in the /etc directory have been relocated to each member's boot partition and replaced with CDSLs (see Figure 12-2).

Table 12-2 lists the databases and their locations respective to a cluster or standalone system.

# 12.3.2 The hwmgr (8) Command Revisited

The hwmgr command is cluster aware. It must, however, be focused on the cluster in order to see clusterwide results or you will see only member-specific information. For example, if you want to view the devices on you cluster you would use the "hwmgr -view device" command.

![](bbox=[0.09, 0.98, 0.92, 0.99])