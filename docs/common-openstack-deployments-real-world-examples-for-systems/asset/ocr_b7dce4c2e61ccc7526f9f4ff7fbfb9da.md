# ## Storage and Clusters

Swift operates as a cluster. A production cluster will span storage devices and zones where data is stored. As we’ll discuss, you will be using Rings to map where data is located on your cluster so Swift components like the proxy-server and object-replicator find the actual device to store, retrieve or replicate your data.

> **Tip**
> Swift is built to distribute the files over a large number of commodity servers and directly attached disk devices to provide inexpensive, redundant and fast storage.
> As such, using Network-Attached Storage (NAS) for Swift is unnecessary because it introduces the potential for higher latency and possible overlap of redundancy that Swift already attempts to provide.
> However if it’s more convenient in your environment, you may use NAS storage with Swift.

As we’ll review later when we pull the components together, there are four different types of daemons in Swift: Proxy, Account, Container and Object. These are often deployed together, and a production cluster is made up of multiple physical proxy and storage nodes. In Figure 9.2 later in this chapter, you should imagine the Swift API ultimately connecting to any of these servers in the cluster with your containers and back ends, depending on the actions performed and objects you’re requesting.

# ### Rings

As you configure Swift you’ll quickly become familiar with the concept of the Ring. It can be considered part database and part configuration file. Rings are used to determine where your data should reside on the Swift object storage cluster and describe options like the number of times data is replicated across the cluster. Rings exist for various layers of your cluster, with Rings existing for account and container databases, as well as handling individual object storage policies. They are built and managed with a Swift utility called ring-builder.
While you’re getting started with the Ring, you’ll also become familiar with the concepts of devices, partitions, replicas and zones which the Ring uses for its mapping of objects onto the physical location.

+   - **Zones**—Distinct, physically and operationally separated locations for data. A zone may be a rack or groups of racks of hardware that has its own power and connectivity separate from other zones. Beyond Zones you may also have Regions, which isolate the data further.
+   - **Devices**—The physical storage location for data, typically a disk. Devices can be weighted so that, for instance, bigger drives are assigned a higher weight and smaller drives a smaller weight. Throughout the standard life cycle of hard drives, you will add and remove devices from a Swift cluster.
+   - **Partitions**—Objects are located on Swift partitions. Partitions are what are replicated. The administrative documentation for Swift recommends a minimum of 100 partitions per drive to make sure there is even distribution across the drives and provides advice about calculating the number of partitions per drive. Be cautious not