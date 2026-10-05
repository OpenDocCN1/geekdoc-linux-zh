
# CHAPTER 9 • ADVANCED VIRTUAL MACHINE FEATURES

```powershell
$dev.Device.Backing = \
New-Object Vware.Vim.VirtualEthernetCardNetworkBackingInfo
$dev.Device.Backing.DeviceName = $destinationNetwork
```

```powershell
"VmwareVDPortGroupImpl" {
$dvs = Get-View -ViewType VmwareDistributedVirtualSwitch \
-Server $destinationVC \
-Property @("uuid", "Summary.PortGroupName") |
-Where-Object {$Summary.PortGroupName -contains $destinationNetwork.Name }
$dev.Device.Backing = New-Object Vware.Vim.VirtualEthernetCard\DistributedPortBackingInfo
}
```

```powershell
$dev.Device.Backing.Port = New-Object Vware.Vim.DistributedVirtual\SwitchPortConnection
$dev.Device.Backing.Port.Uuid = $dev.Uuid
$dev.Device.Backing.Port.PortGroupKey = $destinationNetwork.Key
}
$spec.DeviceChange += $dev
} else {
Write-Warning "Cross vCenter vMotion does not support \
motion between Standard and Distributed Switches"
break;
}
if ($PsCmdlet.ShouldProcess("Cross VC vMotion",
"Migrating $VMName to $DestinationVC") {
  # Issue Cross VC-vMotion
$task = $vm.RelocateVM_Task($spec, "defaultPriority")
```

# USE VMOTION AND STORAGE VMOTION

```powershell
$task1 = Get-Task -Id ("Task-\$($task.value)") @splat
if ($RunAsync)
{
    Write-Output $task1
} else {
    $task1 | Wait-Task
    Get-VM -Name $VMName -Server $DestinationVC
}
```

Using the function in Listing 9.6, it is possible to non-disruptively relocate a VM to a physically separate vCenter instance. There are a few gotchas. Although the port group can be remapped during the migration, the VM cannot be migrated from a standard switch to a distributed switch, or vice versa. If the source and destination vCenter instances share an SSO domain, the credentials are not needed for the vCenter. The following example migrates VM001 from VC1 to VC2:

```powershell
# Connect to source VC
Connect-VIServer -Server VC1 -Credential $creds
# Connect to destination VC
$vc2 = Connect-VIServer -Server VC2 -Credential $creds -NotDefault
# Destination target cluster or resource pool
$cluster = Get-Cluster -Name Prod01 -Server $vc2
# Destination target VMHost
$VMHost = Get-VMHost -Server $vc2 | Get-Random
# Destination Datastore to copy VM into
$datastore = Get-Datastore -Name Datastore4 -Server $vc2
$PortGroup = Get-VirtualPortGroup -Standard -Server $vc2 -Name Vlan1107
Move-CrossVC -VMName VM001 `
-VMHost $VMHost `
-Datastore $datastore `
-PortGroup $PortGroup `
-DestinationVC $VC2 `
```

![](img/62596f5acc979040608a4e5111beb7d6_352_0.png)

-DestinationCredential $creds
-Cluster $cluster

To accommodate more complex virtual machine configurations, the function also takes a hash table mapping of VM network adapter MAC address to port groups. This allows the migration of VMs that are using both standard and distributed switches. The following example migrates VM002 from v2 to v1:

```powershell
# Connect to source VC
Connect-VIServer -Server VC2 -Credential $creds
# Connect to destination VC
$vcl = Connect-VIServer -Server VC1 -Credential $creds
-NotDefault
# Destination target cluster or resource pool
$cluster = Get-Cluster - Name Prod03 -Server $vcl
# Destination target VMHost
$VMHost = Get-VMHost -Server $vcl | Get-Random
# Destination Datastore to copy VM into
$datastore = Get-Datastore -Name Datastore0 -Server $vcl
$AdvancedNetworkMap=@
  '00:50:56:ba:54:2c'
$PortGroup = Get-VirtualPortGroup -Standard -Server $vc2 -Name Vlan1107
Move-CrossVC -VMName VM001 `
-VMHost $VMHost `
-Datastore $datastore `
-PortGroup $PortGroup `
-DestinationVC $VC2 `
```
