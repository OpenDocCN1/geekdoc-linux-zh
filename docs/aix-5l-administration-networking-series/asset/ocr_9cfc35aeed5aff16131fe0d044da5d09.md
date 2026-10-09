# # HACMP CLUSTER ADMINISTRATION

This section provides a list of tasks you perform to start and shut down cluster services, maintain shared LVM components, make dynamic changes, and monitor the cluster.
The following administrative tasks for an HACMP system are described here:

+   - Starting and stopping cluster services
+   - Maintaining shared LVM components with C-SPOC
+   - Dynamic reconfiguration
+   - Monitoring cluster activity

# ## Starting the Cluster

You can start HACMP on each of the cluster nodes or use the Cluster Single Point of Control (C-SPOC) utility, which starts (or stops) cluster services on *all* nodes that you specify.

Starting cluster services starts the HACMP daemons that enable the coordination required between nodes in a cluster and trigger the execution of certain HACMP scripts that acquire the highly available resources. Before starting cluster services, you must have a thorough understanding of the node interactions it causes and the impact on your system’s availability.

To start HACMP on a single node, you can type `smitty clstart` or use the **Start Cluster Services** SMIT menu. You have the following cluster start-up options:

+   - Start now
+   - Start on system restart
+   - Start now *and* on system restart (both options together)
+   - Start and reacquire resources that were manually changed or taken offline after the cluster has been forced down

> **NOTE** When starting HACMP on system restart, the `/etc/inittab` entry for HACMP *must* be the very last entry in this startup file, since it takes over control of the system resources.

# ## Stopping the Cluster

Stopping cluster services stops the HACMP daemons on a node that enable the coordination required between nodes in a cluster and may or may not cause the execution of additional HACMP scripts, depending on the type of shutdown you perform. Before stopping cluster services, you must have a thorough understanding of the node interactions it causes and the impact on your system’s availability. Next we briefly describe when you may need to shut down the cluster and what are the different cluster shutdown options.