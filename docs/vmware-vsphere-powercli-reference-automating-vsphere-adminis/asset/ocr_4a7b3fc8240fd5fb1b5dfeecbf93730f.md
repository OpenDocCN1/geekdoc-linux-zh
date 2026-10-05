```
#create an array with all available portgroups in the cluster
$clusterHosts = @($cluster | Get-VMHost)
$refPortGroups = @($clusterHosts | Get-VirtualPortGroup)
-Standard
Select-Object -Unique
```

```
#compare the hosts against the reference array
foreach ($vmHost in $clusterHosts) {
$diffPortGroups = @($vmHost | Get-VirtualPortGroup -Standard)
$differences = @(Compare-Object $refPortGroups \
$diffPortGroups)
foreach ($item in $differences) {
$objPG = "" | Select-Cluster,HostName,MissingPortGroup
$objPG.Cluster = $cluster
$objPG.HostName = $vmHost.Name
$objPG.MissingPortGroup = $item.InputObject
objPG
}
}
```

Now let's look at the report:

```
Get-Cluster CL02 | Get-MissingPortGroup
```

| Cluster | HostName | MissingPortGroup |
|---|---|---|
| CL02 | esx001.mydomain.local | Management Network |
| CL02 | esx003.mydomain.local | Management Network |
| CL02 | esx002.mydomain.local | VLAN020 |

Notice that the hosts esx001 and esx003 are both a Management Network port group and host esx002 doesn't contain the VLAN020 port group.