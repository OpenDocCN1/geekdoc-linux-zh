
```powershell
elseif ($ESXIHost -isnot [VMware.VimAutomation.VCore.Impl.V1.Inventory.VMHostImpl]){
    Write-Warning "You did not pass a string or a VMHost object"
    continue
}

# --- Create Host Maintenance Spec
try {
```powershell
$VSANHostDecommissionModeObjectAction = `
New-Object VMware.Vim.VsanHostDecommissionModeObjectAction `
-Property @value = $VSANModeValue
```

```powershell
$VSANHostDecommissionMode = `
New-Object VMware.Vim.VsanHostDecommissionMode `
-Property "ObjectAction" = $VSANHostDecommissionModeObjectAction
```

```powershell
$HostMaintenanceSpec = `
New-Object VMware.Vim.HostMaintenanceSpec `
-Property "VSANMode" = $VSANHostDecommissionMode
```
}
catch [Exception] {
    $ErrorText = "Unable to create Host Maintenance Spec for $ESXIHost"
    throw
}

# --- Put in Maintenance Mode with VSAN Option
try {
    if ($PSCmdlet.ShouldProcess($ESXIHost)) {
```powershell
$MaintenanceModeTask = $ESXIHost.ExtensionData.EnterMaintenanceMode_Task(0,$true,$HostMaintenanceSpec)
$Task = Get-Task -Id $MaintenanceModeTask
```
![](img/62596f5acc979040608a4e5111beb7d6_192_0.png)

# 162 CHAPTER 4 • AUTOMATING STORAGE

```powershell
while ((($Task.State -ne 'Success') -and ($Task.State -ne 'Error'))) {
```

```powershell
Write-Verbose "Waiting for VSAN Maintenance Mode task to complete ($($Task.PercentComplete)% done)"
Start-Sleep -Seconds $PollSeconds
```

```powershell
$Task = Get-Task -Id $MaintenanceModeTask
}
if ($Task.State -eq 'Success') {
``````powershell
Write-Verbose "VSAN Maintenance Mode task for ESXiHost succeeded! The timespan for the operation: '$(New-TimeSpan -Start $Task.StartTime -End $Task.FinishTime)'"
Get-VMHost $ESXiHost | Select-Object Name,ConnectionState
```

```powershell
if ($Task.State -eq 'Error') {
``````powershell
Write-Warning "VSAN Maintenance Mode task for $ESXiHost failed"
}
}
catch [Exception] {
``````powershell
$ErrorText = "VSAN Maintenance Mode task for $ESXiHost failed"
throw
}
catch [Exception] {
    if ($ErrorText) {
        throw "Unable to set VMHost $($ESXiHost) to VSAN Maintenance Mode. Error is: $($ErrorText)"
    }
    else {
        throw "Unable to set VMHost $ESXiHost into VSAN Maintenance Mode"
    }
}
}
end {

Typical use would be similar to the following example:

```hell
PS C:\ Get-VMHost vsanesxi101* | Set-VMHostMaintenanceMode -VSANMode Evacuate
```

## Storage Policy

Earlier in this chapter, we showed how to create storage policies. With VSAN, you can create a storage policy using some of its capabilities. (We created vCenter tags that were used in the previous examples.) Listing 4.33 demonstrates how to create a storage policy using the VSAN capabilities VSAN.hostFailuresToTerate and VSAN.cacheReservation and assign it to VMs with the wildcard Server*.

## LISTING 4.33 Creating a VSAN storage policy and assigning it to VMs

```powershell
$Rule1 = New-SpbmRule -Capability (Get-SpbmCapability) -Name 'VSAN.hostFailuresToTerate' -Value 1
$Rule2 = New-SpbmRule -Capability (Get-SpbmCapability) -Name 'VSAN.cacheReservation' -Value 10
$VSANRuleSet = New-SpbmRuleSet -AllOfRules $Rule1,$Rule2
$VSANStoragePolicy = New-SpbmStoragePolicy -Name 'VSAN Storage Policy 01' -Description 'VSAN Storage Policy' -AnyOfRuleSets $VSANRuleSet | Get-VMServer* | Set-SpbmEntityConfiguration -StoragePolicy $VSANStoragePolicy
```

## Using Advanced vSphere Features

IN THIS CHAPTER, YOU WILL LEARN TO:

- CONFIGURE EVC 166
- VFLASH READ CACHE 171
- MANAGE DRS GROUPS 184
- USE FAULT TOLERANCE 194
- USE DISTRIBUTED POWER MANAGEMENT 196
- CONFIGURE HOST PROFILES 204
- CONFIGURE ACTIVE DIRECTORY INTEGRATION 207

At this point, we have shown that vSphere is the virtualization platform of choice for a myriad of reasons. This chapter focuses on some of the most advanced features vSphere offers. Be aware that many of these features require Enterprise licensing to be used.

## Configure EVC

Have you ever tried to use hardware in the same cluster as newly purchased servers? Did you encounter a condition where virtual machines would not vMotion between generations? CPU features between the newer and older generations are incompatible. VMware uses EnhancedMotion Compatibility (EVC) to mask the features of newer-generation CPUs so that they appear to have the same capabilities as the older generation. This facilitates vMotion across CPUs of the same manufacturer, even when they are vastly different. One thing to note, though, that EVC doesn't allow you to vMotion from AMD to Intel, or vice versa.

In recent versions of PowerCLI, VMware has added the ability to configure EVC for a cluster using the standard Set-Cluster cmdlet, as shown in Listing 5.1.

## LISTING 5.1 Setting the EVC mode using PowerCLI

```powershell
Get-Cluster $clustername | Set-Cluster -EVCMode nehalem
```
That snippet sets the EVC mode; it masks CPU features for all Intel processors so that they are at the level of the Nehalem platform. For ESXi 5.5 the supported EVC modes are:

- nehalem
- penryn
- westmere
- sandybridge
- ivybridge
- amd-rev-e
- amd-greyhound-now
- amd-greyhound
- amd-bulldozer
- amd-driver
- amd-piled
- amd-streamroller
- intel-haswell
- westwell

ESXi 6 adds support for these architectures as well:

For each manufacturer, the list builds on the less capable architecture. This means that your cluster can only support the EVC mode of the least capable architecture. Unfortunately, there is no quick way to determine what mode should be. You will have to do it with trial and error. Fortunately, PowerCLI has access to this information, so you can create a simple function to determine the maximum EVC setting for any cluster. Take a look at Listing 5.2.

## 5.2 The Get-MaxEvMode function

```powershell
Get-MaxEvMode {
.SYNOPSIS
Get the highest EVC level for a cluster

.DESCRIPTION
Function to get the highest EVC level supported by all VMHosts in a cluster. Useful to easily determine the highest EVC level one might set for the cluster based on the VMHosts that are a part of the cluster and their hardware types.

.EXAMPLE
Get-MaxEvMode -Cluster (Get-Cluster clusterName)
Get the EVC mode for cluster "clusterName"
}
```

# CHAPTER 5 • USING ADVANCED VHERE FEATURES

.EXAMPLE
Use the pipeline to get the EVC mode for the given clusters.
Get-Cluster someCluster,someOtherCluster | Get-MaxEvMode

.PARAMETER Cluster
The cluster whose maximum EVC mode to determine.

.INPUTS
VMware.VimAutomation.VCore.Impl.V1.Inventory.ClusterImpl

.OUTPUTS
PSCustomObject

```powershell
[CmdletBinding()]
param(
    Mandatory=$true,
    ValueFromPipeline=$true
)
    [VMware.VimAutomation.VCore.Impl.V1.Inventory.ClusterImpl]
    $Cluster
)
process {
    $hosts = $Cluster | Get-VMHost

    # get the max supported for each host
    $nodeMaxEvMode = @{}

    $hosts | Foreach-Object {
        $nodeMaxEvMode.Add(
            $_.Name,
            $_.ExtensionData.Summary.MaxEVCKey
        )
    }

    # check to see if there are different CPU manufacturers
    $lastManufacturer = ""

    $incompatible = $false

    $nodeMaxEvMode.GetEnumerator() | Foreach-Object {
        $currentManufacturer = ($_.Value.split "-") [0]
        if ($lastManufacturer -eq "") {
            $lastManufacturer = $currentManufacturer
        }

        if ($lastManufacturer -ne $currentManufacturer) {
            Write-Warning "Hosts have Intel and AMD CPUs"
            $incompatible = $true
        }

        # check to see if they are all the same
        [Array]$evcGroups = $nodeMaxEvMode.GetEnumerator() |
        Group-Object -Property Value

        if ($evcGroups.Count -eq 1) {
            # they're the same, print out the first one
            $obj = $ | Select-Object MaxEvcMode
            $obj.MaxEvcMode = $evcGroups[0].Name
            $obj
        }
        elseif ($incompatible -eq $false) {
            # they're not the same, let's figure out the least common denominator
            # collect all available EVC modes
            $evcModes = @{
                'intel' = @();
                'amd' = @();
            }

            $serviceInstance = Get-View ServiceInstance

            $serviceInstance.Capability.SupportedEVCMode | Foreach-Object {
                $procManufacturer = ($_.key -split "-") [0]
```
