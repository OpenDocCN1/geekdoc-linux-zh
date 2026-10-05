# CHAPTER 9 • ADVANCED VIRTUAL MACHINE FEATURES

```
[parameter (Mandatory=$true, ValueFromPipelineByProperty)
Name=$true,
    ParameterSetName='easyNetwork')]
```

```
[parameter (Mandatory=$true, ValueFromPipelineByProperty)
Name=$true,
    ParameterSetName='hardNetwork')
[Alias("Name")
[string]
VMName
```

```
# Destination resource pool or cluster to relocate vm to
[parameter (Mandatory=$false, ValueFromPipeline=$true,
    ParameterSetName='easyNetwork')]
[parameter (Mandatory=$false, ValueFromPipeline=$true,
    ParameterSetName='hardNetwork')]
[Vm.Automation.ViCore.Types.V1.Inventory.]
VIContainer
```

```
$Cluster
# Destination VMHost to relocate vm to
[parameter (Mandatory=$true, ValueFromPipeline=$true,
    ParameterSetName='easyNetwork')]
[parameter (Mandatory=$true, ValueFromPipeline=$true,
    ParameterSetName='hardNetwork')]
[Vm.Automation.ViCore.Impl.V1.VMHostImpl]
$VMHost
```

```
# Destination Datastore to relocate vm to
[parameter (Mandatory=$true, ValueFromPipeline=$true,
    ParameterSetName='easyNetwork')]
[parameter (Mandatory=$true, ValueFromPipeline=$true,
    ParameterSetName='hardNetwork')]
[Vm.Automation.ViCore.Impl.V1.DatastoreManagement.]
$Datastore
```

```
# Destination PortGroup to migrate VM Networking to
```