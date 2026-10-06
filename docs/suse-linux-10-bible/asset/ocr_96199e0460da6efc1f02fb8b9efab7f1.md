# Chapter 27 ✦ Enterprise Architecture 691

Each protocol version provides a different profile for writing data depending on your network and disk latency also whether you need to guarantee your data has been saved to the remote disk or not.

+   * If you are using a high-latency connection, you may need to use protocol A. This effectively removes any issues you have with the kernel as soon as it has been written to the local disk and sent to the network buffer. This is the fastest protocol you can use if your application needs near-local write efficiency.
* If you are using a low-latency network, protocol C guarantees that data has been written to machines disks before a is returned by the kernel. If you notice that your disk writes are taking too long when using this protocol, you may want a mid point between protocol A and C.
* Protocol B returns a write only when data has been written to the local disk and has been received by the remote network buffer. This decreases the amount of time it takes for local writes but gives you some guarantee that your network is on the way to being written to the remote disk.

Choosing the best protocol is something that you must be comfortable with because it severely impacts the speed of local writes to the disk, slowing down the application that relies on the data being replicated. As we are more concerned with the integrity of the data and we have chosen protocol C.

# Defining Your Hosts

When your network and protocol have been defined, you need to specify the hosts that will be part in the replication.

In Listing 27-1, we have defined node first, telling DRDB that is the primary node.

You need to define the IP address of the node, the device to replicate, and the name of the device as it will be used by the node itself.

> After DRDB has been configured for a device, DRDB device is to be used as the device to replicate. We have defined that /dev/sdb1 should be replicated and that we use the device /dev/ndb0 to access the replicated device. For example, we can use mikiserfs/dev/ndb0 to create a Reiser filesystem that is replicated to the secondary node automatically.

For the sake of verbosity, we have also specified in the listing the TCP port that will use for sending DRDB data over the network. And we have also made a similar configuration with the configuration that is specific to the secondary node.

When saved, you can copy the drdb.conf file to the secondary node as is and start DRDB with drdrdb start.

When DRDB has started, check /proc/drdb for information what DRDB is doing and where the node is in primary or secondary node.