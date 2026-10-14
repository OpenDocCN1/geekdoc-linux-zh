Since the DHCP database will be available to all members of the cluster through the magic of CFS, it is relatively easy for CAA to handle the failover if necessary.

All DHCP clients must request access to the DHCP server using the default cluster alias in order to avoid having to reconfigure the DHCP software each time the serving member leaves the cluster.

# 20.4 NFS in a Cluster

NFS is a very heavily used mechanism for allowing transparent remote access to file systems. It requires a cooperative effort between the client system (doing the remote mount request) and the server system (providing the remote access).

# 20.4.1 NFS Client

Setting up a cluster member as an NFS client means that any NFS file systems mounted by the client member will be accessible to the other members of the cluster through the mounting member. Other members can also be NFS clients, but only one member can mount a particular NFS exported file system at a time. NFS clients will remotely mount file systems (or access directories) that actually exist on another system in the network. Given what we know about CFS, it is reasonable to expect that a file system that is mounted on one member will be visible to all members. This is indeed true for NFS mounted file systems as well. In truth, one member will request the remote mount, but all other members will get access to the remotely mounted file system through the member that actually did the mount. The member requesting the NFS mount automatically becomes the CFS server for that file system (see Figure 20-1).

![](bbox=[0.115, 0.69, 0.88, 0.885])

Figure 20-1: NFS Client – CFS Server