
## HACMP Cluster Administration

This section provides a list of tasks you perform to start and shut down cluster services, maintain shared LVM components, make dynamic changes, and monitor the cluster.
The following administrative tasks for an HACMP system are described here:

- Starting and stopping cluster services
- Maintaining shared LVM components with C-SPOC
- Dynamic reconfiguration
- Monitoring cluster activity

### Starting the Cluster

You can start HACMP on each of the cluster nodes or use the Cluster Single Point of Control (C-SPOC) utility, which starts (or stops) cluster services on *all* nodes that you specify.

Starting cluster services starts the HACMP daemons that enable the coordination required between nodes in a cluster and trigger the execution of certain HACMP scripts that acquire the highly available resources. Before starting cluster services, you must have a thorough understanding of the node interactions it causes and the impact on your system’s availability.

To start HACMP on a single node, you can type `smitty clstart` or use the **Start Cluster Services** SMIT menu. You have the following cluster start-up options:

- Start now
- Start on system restart
- Start now *and* on system restart (both options together)
- Start and reacquire resources that were manually changed or taken offline after the cluster has been forced down

> **NOTE** When starting HACMP on system restart, the `/etc/inittab` entry for HACMP *must* be the very last entry in this startup file, since it takes over control of the system resources.

### Stopping the Cluster

Stopping cluster services stops the HACMP daemons on a node that enable the coordination required between nodes in a cluster and may or may not cause the execution of additional HACMP scripts, depending on the type of shutdown you perform. Before stopping cluster services, you must have a thorough understanding of the node interactions it causes and the impact on your system’s availability. Next we briefly describe when you may need to shut down the cluster and what are the different cluster shutdown options.

### When to Stop Cluster Services

You must stop cluster services before performing the following tasks:

- Making any hardware and some software changes
- Shutting down or rebooting a node in the cluster
- Changing the name of the cluster, the name of the node, or the name of an adapter

### Cluster Shutdown Options

To stop cluster services on a single cluster node, you type `smitty clstop` or use the **Stop Cluster Services** SMIT menu. When you stop cluster services, you must decide when to stop (now, on system restart, or both). You must also decide how to handle resources that were owned by the node you are removing from the cluster. For this, you have the following options:

- In a *graceful stop*, the HACMP software shuts down its applications and releases its resources. The other nodes *do not* take over the resources of the stopped node.
- In a *graceful with takeover* stop, the HACMP software shuts down its applications and releases its resources. The surviving nodes take over these resources. This is also called *intentional failover*.
- In a *forced stop*, HACMP shuts down immediately. The node that is shutting down retains control of all its resources. Applications that do not require HACMP daemons continue to run. Typically, you use the forced option so that stopping the Cluster Manager does not interrupt users and clients. As no cluster agent is running on the node after a *forced* down, failures are not detected. This applies to hardware resources such as disks and adapters, as well as any monitored applications. If any resources defined to HACMP are disrupted, they should be restored to their prior state before restarting cluster services.

If you use an AIX shutdown command, HACMP services are stopped with the forced option. If you want resources to be taken over, you stop HACMP using the graceful with takeover option before performing the AIX shutdown.

### Cluster Single Point of Control (C-SPOC)

HACMP provides the Cluster Single Point of Control (C-SPOC) utility, which simplifies maintenance of shared LVM components. C-SPOC commands provide comparable *functions* in a cluster environment to the standard AIX commands that work on a single node. For example, the C-SPOC utility includes a command called `cllv` that provides similar functions to the AIX `cllv` command. (The C-SPOC command calls the AIX command.) By automating repetitive tasks, C-SPOC eliminates a potential source of errors and speeds up the process. You can use C-SPOC to perform the following LVM maintenance tasks:

- Create, import, extend, reduce, mirror, and unmirror shared and concurrent volume groups.
- Synchronize volume group mirrors.
- List all active shared or concurrent volume groups.
- Display characteristics of a shared (or concurrent) volume group.
- Create, make a copy of, and remove a copy of a logical volume.
- List all shared logical volumes by volume group.
- Change or view the characteristics of a shared logical volume (name, size).
- Remove a shared logical volume.
- Create, list, change, and remove shared filesystems.
- Add, replace, and remove a physical volume.

> **NOTE** C-SPOC commands operate only on shared and concurrent LVM components that are defined as part of an HACMP resource group.

When you execute a C-SPOC command, the utility determines on which node to perform the operation and then executes the required commands on that node. Typically, C-SPOC executes the command on the node that owns the LVM component (has it varied on). However, you can use C-SPOC commands (on the command line, not from SMIT) on an LVM component that is not currently activated on any cluster node. In this case, C-SPOC determines which node will own the LVM component when it is activated, as specified for the HACMP resource group, and performs the operation on that node. Using C-SPOC simplifies the steps required for all tasks. Moreover, you do not have to stop and restart cluster services in order to do the tasks.

### Dynamic Reconfiguration and Resource Group Management

When you configure an HACMP cluster, configuration data is stored in HACMP-specific object classes in the ODM. The AIX ODM object classes are stored in the default system configuration directory (DCD), `/etc/objrepos`. You can make certain changes both to the cluster topology and to the cluster resources while the cluster is running (dynamic reconfiguration).

#### Dynamic Cluster Reconfiguration (DARE)

At cluster start-up, HACMP copies HACMP-specific ODM classes into a separate directory called the Active Configuration Directory (ACD). While a cluster is running, the HACMP daemons, scripts, and utilities reference the ODM data stored in the ACD.

If you synchronize the cluster topology or cluster resources definition while the Cluster Manager is running on the local node, this action triggers a dynamic reconfiguration (DARE) event. In a dynamic reconfiguration event, the ODM data in the Default Configuration Directories (DCDs) on all cluster nodes is updated and the ODM data in the ACD is overwritten with the new configuration data. The HACMP daemons are refreshed so that the new configuration becomes the currently active configuration.

You can make many changes to the cluster topology and resources in an active cluster, dynamically, such as adding or removing nodes and adapters, changing network tuning parameters, swapping adapter cards, adding or removing resources from resource groups, and making changes to the configuration of many types of resources.

Some changes require stopping the cluster, such as changing the cluster name or changing a node name. For details on exactly which tasks can be performed dynamically and which cannot, see the HACMP manuals.

#### DARE Resource Migration

Additionally, you can use the DARE Resource Migration utility to move resource groups to other cluster nodes to perform system maintenance on a particular cluster node. DARE Resource Migration allows you to change the status (online or offline) or location of a cascading or routing resource group without stopping cluster services. You can perform DARE resource migrations from the command line and through SMIT.

You can also disable resource groups dynamically, preventing them from being acquired during a reintegration. This disabling option allows a “swap” of resources in certain situations.

## Tools for Monitoring the HACMP Cluster

By design, failures of components in the cluster are handled automatically by HACMP, but you still need to be aware of all such events. You can use several tools to check the status of an HACMP cluster; the nodes, networks, and resource groups within that cluster; and the daemons that run on the nodes. HACMP provides the following tools for monitoring a cluster:

- The HAVView utility extends Tivoli NetView services so that you can monitor HACMP clusters and cluster components across a network from a single node.
- Cluster monitoring with Tivoli allows you to monitor clusters and cluster components and (in version 4.5) also perform cluster administration tasks through your Tivoli Framework console.
- clstat (the `/usr/sbin/clstat` utility, or `xlclstat` for the X version) uses the HACMP Cluster Information Program (clinfo) API to retrieve and display the status of key cluster components—the cluster itself, its nodes, network interfaces, and resource groups—and can be viewed in an X Window, an ASCII display, or (in version 4.5) a Web browser. The clinfo daemon is a cluster monitor based on the Simple Network Management Protocol (SNMP).
