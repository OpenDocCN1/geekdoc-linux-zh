
something like the code in Listing 16.4 to automate the level part of the statistics.
The results are shown in Figure 16.4.

Note that the vCenter Server does not allow a higher statistics level for a historical interval than the statistics level used in the preceding historical interval. For example, you can't specify a level 3 for HI14 when HI3 has a statistics level of 2.

## Listing 16.4 Changing the statistics level of a historical interval

```
Get-StatInterval -Name 'Past day' | Set-StatIntervalLevel -Level 4
-Confirm:$false
Get-StatInterval -Name 'Past week' | Set-StatIntervalLevel -Level 2
-Confirm:$false
Get-StatInterval -Name 'Past month' | Set-StatIntervalLevel -Level 2
-Confirm:$false
Get-StatInterval -Name 'Past year' | Set-StatIntervalLevel -Level 1
-Confirm:$false
```

## Figure 16.4 Resulting statistics levels

![](img/62596f5acc979040608a4e5111beb7d6_586_0.png)

## Metrics

Several managed entities provide utilization and other performance metrics. These managed entities are as follows:

- Hosts
- Virtual machines
- Compute resources (the cluster base type)
- Resource pools
- Datastores
- Networks

Each of the performance providers that generate the statistical data has its own set of performance counters. Each performance counter is identified by a unique ID, which you will also find in the statistical data. Note that these IDs are not necessarily the same in the vSphere environments.
The performance counters are organized in groups based on the resources they cover (Table 16.2).

## TABLE 16.2 Performance counter groups

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

## UNDERSTAND SOME BASIC CONCEPTS

### LIST 16.5 The Get-StatType cmdlet, which returns metrics names

```
Get-StatType -Entity (Get-VMHost) | Select-Object -First 1
```

```
cpu.usage.average
cpu.usage.minimum
cpu.usage.maximum
cpu.usagehz.average
cpu.usagehz.minimum
cpu.usagehz.maximum
cpu.reservedCapacity.average
cpu.wait.summation
cpu.ready.summation
cpu.idle.summation
cpu.used.summation
cpu.capacity.provisioned.average
cpu.capacity.usage.average
cpu.capacity.demand.average
cpu.capacity.contention.average
cpu.corecount.provisioned.average
cpu.corecount.usage.average
cpu.corecount.contention.average
```

With the following code (Listing 16.6), you can capture the metrics in text files. Notice the -Unique parameter on the Sort-Object cmdlet; this ensures there won't be any duplicate entries due to the different instances (as you'll learn later in this chapter) that can return a specific metric.

### LISTING 16.6 Retrieving the metrics

```
# Cluster metrics
Get-StatType -Entity (Get-Cluster) | Select-Object -First 1 | \
Out-File 'Cluster-metrics.txt'
# Host metrics
Get-StatType -Entity (Get-VMHost) | Select-Object -First 1 | \
Sort-Object -Unique | \
Out-File 'Host-metrics.txt'
# Virtual machine metrics
Get-StatType -Entity (Get-VM) | Select-Object -First 1 | \
Sort-Object -Unique | \
Out-File 'VM-metrics.txt'
# Resource pool metrics
```

![](img/62596f5acc979040608a4e5111beb7d6_588_0.png)

```
Get-StatType -Entity (Get-ResourcePool) | |
Select-Object -First 1) | |
Sort-Object -Unique | |
Out-File 'Resource-pool-metrics.txt'
```

While the resulting text files give you a complete list of the available metrics, there is still a lot of the available information that stays hidden. By using an SDK method, you can produce a better and more detailed report of the available metrics. The function in Listing 16.7 uses the SDK methods to return more details about the available metrics for an entity.

## LISTING 16.7 Listing available metrics

```
function Get-StatTypeDetail {
#
.SYNOPSIS
Returns available metrics for an entity
.DESCRIPTION
The function returns the available metrics for a specific entity. Entities can be ESX(i)Xi host, clusters, resource pools or virtual machines.
The function can return the available metrics for all the historical intervals together or for the realtime interval
.PARAMETER Entity
The entity for which the metrics should be returned
.PARAMETER Realtime
Switch to select the realtime metrics
.EXAMPLE
Get-StatTypeDetail -Entity (Get-VM 'Guest1')
.EXAMPLE
Get-StatTypeDetail -Entity (Get-VMHost 'esxl') -Realtime
.EXAMPLE
Get-VM 'Guest1' | Get-StatTypeDetail
#>
[CmdletBinding()]
Param(
    [parameter(ValueFromPipeline = $true, Mandatory = $true,
HelpMessage = 'Enter an entity')]
[VMware.VimAutomation.Vi
```

## UNDERSTAND SOME BASIC CONCEPTS

```
# Create performance counter hashtables
$si = Get-View
$perfMgr = $si.Content
$keyTable = New-Object
foreach($pcC in $perfMgr.PerfCounter) {
    if ($pcC.Level -ne 99) {
        $pKey = $pcC.GroupInfo.Key, $pcC.NameInfo.Key,
$pcC.RollupType
        if (!$keyTable.ContainsKey($pKey)) {
            $keyTable.Add($pKey, $pcC)
        }
    }
}
$metricslist = @()

# Get the metrics
$metrics = $perfMgr.QueryAvailableMetric(
$_.ExtensionData.MoRef,
$null,
$null)
$metricsInstances = $metrics | Where-Object {$Instance-eq ''}
foreach($pmId in $metricsInstances) {
    $pcC = $keyTable[$pmId.CounterId]
    $row = [ordered]@{
        CounterId = $pcC.Key
        Group = $pcC.GroupInfo.Key
        Name = $pcC.NameInfo.Key
        Rollup = $pcC.Rollup
    }

$mslist += New-Object -TypeName PSObject -Property
$row
}
}
{
$mslist | Sort-Object -Property Entity,Group,Name, Rollup
}
```

## CHAPTER 16 USING STATISTICAL DATA

```
Get-StatTypeDetail \
>>Entity(Get-VMHost |$ Select-Object -First 1) -Realtime \
>>SelectCounterId, Name, Group, Rollup \
>>ftAutoSize -Force
```
