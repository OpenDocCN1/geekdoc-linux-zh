
# UNDERSTAND SOME BASIC CONCEPTS

| | | | |
|---|---|---|---|
| 390 coreUtilization | cpu | average |
| 391 coreUtilization | cpu | maximum |
| 392 coreUtilization | cpu | minimum |
| 397 costop | cpu | summation |

## Instances

Instance is the last concept we want to introduce before we show some practical examples. The official definition of an instance comes from the VMware vSphere API Reference documentation: "An identifier that is derived from configuration names for the device associated with the metric. It identifies the instance of the metric with its source.

Let's try to make this a bit more understandable through an example.

Take the CPU-related metrics for a host. If the host is, for example, equipped with a quad-core CPU, there will be four instances for each CPU-related metric: 0, 1, 2, and 3. In this case, each instance corresponds with the numerical position of the core within the CPU block. And there will be an additional instance, the so-called aggregate, which is the metric averaged over all the other instances.

Each instance gets a unique identifier, which is included in the returned statistical data. The aggregate instance is always represented by a blank identifier.

If you want to list the available instances for a metric on a specific entity, you will have to make use of an SDK method QueryAvailablePerfMetric, as shown in Listing 16.8.

+ Listing 16.8 Listing available instances

```powershell
function Get-StatInstance {
  <
  .SYNOPSIS
  Returns the available instances for a specific metric and entity
  .DESCRIPTION
  The function returns all the available instances for a metric on an entity. The entity can be an ESXI host, a cluster, a resource pool or a virtual machine.
  .PARAMETER Entity
  The entity or entities for which the instances should be returned
  .PARAMETER Stat
  The metric or metrics for which the instances should be returned
  .PARAMETER Realtime
```
```

![](img/62596f5acc979040608a4e5111beb7d6_592_0.png)

PART IV

# CHAPTER 16 USING STATISTICAL DATA

Switch to select the realtime metrics

.EXAMPLE

```powershell
Get-StatInstance -Entity (Get-VM 'Guest1') \
>> -Stat "cpu.usage.average"
```

.EXAMPLE

```powershell
Get-StatInstance -Entity esx -Stat 'cpu.usage.average' \
>> -Realtime
```

.EXAMPLE

```powershell
Get-VMHost MyExS | Get-StatInstance \
>> -Stat 'disk.devicelatency.average'
```

```powershell
[CmdletBinding()]
Param(
    [parameter(ValueFromPipeline = $true, Mandatory = $true, HelpMessage = 'Enter an entity')]
    [PObject]$Entity,
    [parameter(Mandatory=$true, HelpMessage = 'Enter a metric')]
    [string[]]$Stat,
    [switch]$Realtime
)
```

```powershell
begin{
    # Create performance counter hashtables
    $si = Get-View ServiceInstance
    $perfMgr = Get-View $si.content.PerfManager
    $pTable = New-Object Hashtable
    foreach($pC in $perfMgr.PerfCounter){
        if($pC.Level -ne 99) {
            $pKeyComponents = $pC.GroupInfo.Key,
            $pC.NameInfo.Key,
            $pC.RollupType
            $pKey = $pKeyComponents -join '.'
            $pKey = $pKey.ToLower()
            if(!$ptable.ContainsKey($pKey)){
                $ptable.Add($pKey,$pC.Key)
            }
        }
    }
}
```

# UNDERSTAND SOME BASIC CONCEPTS 563

```powershell
process{
    $entSDK = $entity | Get-View
}

# Handle the Realtime switch
$numinterval = $null
if($Realtime) {
    $provsum = $perfMgr.QueryPerfProviderSummary($entSDK.MoreRef)
    $numinterval = $provsum.refreshRate
}

# Get the metrics for the entity
entSDK | Foreach-Object {
    $metrics += $perfMgr.QueryAvailablePerfMetric($_.MoreRef,
    null,
    null,
    $numinterval)
}

# Check is stat is valid
foreach($st in $stat){
  if($pcTable.ContainsKey($st.ToLower())){
    Throw "-Stat parameter $st is invalid."
  }
  else{
    $ids += $pcTable[$st]
  }
  foreach($metric in $metrics){
    if($metric.CounterId -eq $pcTable[$st.ToLower()]){
      $obj = [ordered]{
        StatName = $st
        Instance = $metric.Instance
      }
      New-Object PSObject -Property $obj
    }
  }
}
end()
```

![](img/62596f5acc979040608a4e5111beb7d6_594_0.png)

With the Get-StatInstance function, you can list the instances that are available for one or more metrics (Listing 16.9).

# LISTING 16.9 Listing the available instances for a metric

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

```powershell
Get-StatInstance \
>> -Entity (Get-VMHost) | Select-Object
```

# Gather Statistical Data

When you're comfortable with these concepts, the following list of Get-Stat cmdlets gives you access to statistical data on your ESXi server(s).

The most important cmdlet in this list is the Get-Stat. Let's look at the parameters you can use with the Get-Stat cmdlet:

- **Entity**: This parameter specifies the entity or entities for which the instances should be returned. You can pass the name of the entity, but be aware that there will be execution overhead.
- **Stat**: This parameter specifies the metric or metrics for which the instances should be returned. If you want to retrieve more than one, specify them as a string array. The names of the metrics are not case sensitive.
- **Start**: This defines the beginning of the time range for you want to retrieve statistics.
- **Finish**: Specifies the end of the time range for which you want to retrieve statistics.
- **Realtime**: This parameter specifies that you want to retrieve real-time statistics. These come directly from your ESXi server(s) and by default use a 20-second interval.

# What Is in the Statistical Data?

The Get-Stat cmdlet returns the statistical data as one or more MetricSample objects. To have a good grasp of what you can do with the returned data, you should know what is present in the Sample object. With the Get-Member cmdlet, it is easy to check what properties are available; see Listing 16.10.

# LISTING 16.10 Using the Get-Stat and Get-Member cmdlets to obtain statistical data

```powershell
Get-Stat -Entity (Get-VMHost) | \
>> Select-First 1) -Stat "cpu.usage.average" \
>> -MaxSamples 1 | Select-Object *
```

| | |
|---|---|
| Value | 17.95 |
| Timestamp | 6/19/2015 2:00:00 AM |
| MetricId | mem.usage.average |
| Unit | % |
| Description | Memory usage as percentage of total configured or available memory |
| Entity | esx1.local.test |
| EntityId | HostSystem-host-10 |
| IntervalSecs | 86400 |
| Instance | |
| Uid | /VIServer=local\lucd@vcenter6:443/VMHost=HostSystem-host-10/FloatSample=mem.usage.average\6357027600000000|

Type: VMware.VimAutomation.ViCore.Impl.V1.Stat.FloatSample

| MemberType Definition |
| :--- |
| Description Property System.String Description {get;set;}\ |
