Each of the performance providers that generate the statistical data has its own set of performance counters. Each performance counter is identified by a unique ID, which you will also find in the statistical data. Note that these IDs are not necessarily the same in the vSphere environments.
nThe performance counters are organized in groups based on the resources they cover (Table 16.2).

# TABLE 16.2 Performance counter groups

| Group | Description |
|---|---|
| Cluster Services | Performance for clusters using DRS and/or HA |
| CPU | CPU utilization |
| Disk I/O Counters | I/O performance |
| Storage Utilization Counters | Storage utilization |
| Management Agent | Consumption of resources by the various management agents |
| Memory | All memory statistics for guests and host |
| Network | Network utilization for pNIC,vNIC, and other network devices |
| Resource Scheduler | CPU-load-history statistics about resource pools and virtual machines |
| System | Overall system availability |
| Virtual Machine Operations | Virtual machine power and provisioning operations in a cluster or datacenter |
| Host-based Replication | Host-based replication protection |
| Power | Power resources |
| Storage Capacity | Utilization |

A good source of information for the available metrics is the PerformanceManager entry. For each of the groups listed in Table 16.2, you will find a list of the available metrics.

But you can also use PowerCLI to compile a list of metrics yourself. First, it is important to know that there are only metrics for the following entities in your vSphere environment: clusters, hosts, virtual machines, and resource pools. Second, the Get-StatType cmdlet returns only the name of the metrics. (See Listing 16.5.)