# Configuring Storage I/O Control

Storage I/O Control (SIOC) uses the average latency of all virtual disks across a datastore to calculate latency. This average is then weighted by the number of input/output operations per second (IOPS). When this weighted latency goes above the configured threshold, SIOC limits throughput to the array by resizing the device queue. Therefore, SIOC only runs during times of congestion.

SIOC has seen significant changes since the first edition of this book. First, NFS datastores have been supported since vSphere 5.0; all of storage protocol-based datastores can be enabled for SIOC. Next, PowerCLI version 5.0 added the StorageIOControlEnabled parameter to the Set-Datastore cmdlet. Consequently, the SIOC functions described in the first edition of this book are no longer required. SIOC can be enabled on a datastore without pre-checks for NFS and can be turned on a simple one-line command (Listing 4.15).

+   Listing 4.15 Enabling SIOC on a datastore

```
Set-Datastore -Datastore ISCI01 -StorageIOControlEnabled=$true
Select-Object Name, StorageIOControlEnabled
```

# Datastore Clusters

Datastore clusters were introduced in vSphere 5 and enable the grouping of individual datastores into logical clusters to permit easier management. Coupled with the Distributed Resource Scheduler (SDRS), datastores can now be managed by vCenter in a similar fashion to VMs with DRS. With available space and storage performance statistics, vCenter is able to migrate VMs around the datastore cluster to improve resource utilization.

PowerCLI introduced support for datastore clusters in version 5.1. Listing 4.16 demonstrates how to create a datastore cluster.

+   Listing 4.16 Creating a datastore cluster

```
New-DatastoreCluster -Name DatastoreCluster01 -Location Prod0
```

Only the name and location can be specified at creation time. To configure some of the more interesting settings, such as SDRS and I/O metrics, you must use the Set-DatastoreCluster cmdlet, post-creation. Listing 4.17 demonstrates how to enable SDRS for Full Automation, enable I/O metrics with a 10-millisecond latency threshold, and set a Space Utilization Threshold value of 90%.