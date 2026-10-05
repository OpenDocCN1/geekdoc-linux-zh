
This single command connects your PowerCLI session to the SRM services on both the local and remote vCenter servers. Additionally, like the way the vCenter connection is stored in a global variable, so is the SRM connection: $global:DefaultSrmServers. You can use this variable to address the SRM connection whenever you need to.

## On SRM Recovery Plans

Connecting to the SRM server is one thing, but let's do something useful. The next bit of code (Listing 22.2) shows how to use the SRM API to view your recovery plans:

### LISTING 22.2 Listing SRM recovery plans

```powershell
$srmApi = $global:DefaultSrmServers[0].ExtensionData
$recoveryPlans = $srmApi.Recovery.ListPlans()
$recoveryPlans = % { $_.GetInfo().Name }
```

The code in Listing 22.2 prints the name of each of the recovery plans known by the SRM server. To get additional information, let's look at some of the methods provided by the API. One of the most critical aspects of SRM is ensuring that the datastores are being replicated. The storage for the virtual machine must be replicated between array-based replication (depending on your vendor), or using VMware's vSphere Data Protection technology, referenced as host-based replication by SRM. Without mirroring the storage for a virtual machine, you cannot expect it to be available at the remote location. Listing 22.3 shows how to use the SRM API to list the datastores that are protected. Note that this code snippet will only work with datastores that are using array-based replication.

### LISTING 22.3 Showing protected datastores

```powershell
$srmApi = $global:DefaultSrmServers[0].ExtensionData
$srmApi.Protection.ListProtectionGroups() | % {
  Write-Host "Datastores protected by group $($_.GetInfo())"
}

$_.ListProtectedDatastores | % {
  try {
    $_.UpdateData("Name")
    Write-Host "$($_.Name)"
  } catch {
    return
  }
}
```

There are some interesting things about the SRM API that you won't see other places. Much of this is because the PowerCLI cmdlets mask complexity, but in this case, you don't have cmdlets to use. The first thing to note is that you are executing methods directly in the API. To determine which methods are available, you can pipe the API object to the Get-Member cmdlet, as shown in List 22.4.

### LISTING 22.4 Showing available options and values

```powershell
$srmApi = $global:DefaultSrmServers[0].ExtensionData
$srmApi.Protection | Get-Member
```

| Name | MemberType | Definition |
| :--- | :--- | :--- |
| Name: | Property | VMware.VimAutomation.Srm.Views.SrmProtection |
| CreateProtection | Method | VMware.Vim |
| CreateProtectionGroup | Method | VMware.Vim |
| Equals | Method | bool (System) |
| GetHashCode | Method | int GetHashCode() |
| GetProtectionGroupFolder | Method | VMware.Vim |
| GetType | Method | type GetType() |
| ListInventoryMappings | Method | VMware.Vim |
| ListProtectedDatastores | Method | System.Collection |
| ListProtectedVms | Method | System.Collection |
| ListProtectionGroups | Method | System.Collection |
| ListReplicatedDatastores | Method | System.Collection |
| ListUnassignedReplicatedDatores | Method | System.Collection |
| ListUnassignedReplicatedVms | Method | System.Collection |
| ToString | Method | string ToString() |
| MoRef | Property | VMware.Vim.Manage |

Anything listed in the return is a function that can return or a property that contains data. If your PowerShell window is wide enough, you will be able to see the return value along with any parameters that need to be supplied. If your screen isn't wide enough, you can force PowerShell to display the full listing using the Format-List cmdlet:

```powershell
$srmApi.Protection | Format-List
```

The second thing to notice about the code in Listing 22.3 is that the output does not contain full objects but rather managed object references. This means you must update the data (using UpdateData() method) to populate the fields and information that you need.

Now that you have a basic understanding of how the SRM API works, let's look at some additional information about your recovery plans. Listing 22.5 shows how to use the SRM API to list the protected virtual machines for a recovery plan.

### LISTING 22.5 Showing protected virtual machines

```powershell
$srmApi = $global:DefaultSrmServers[0].ExtensionData
$srmApi.Protection.ListProtectionGroups() | % {
  Write-Host "Virtual machines protected by group $($_.GetInfo().Name)"
  $_.ListProtectedVms() | % {
    try {
      $_.Vm.UpdateData("Name")
      Write-Host "$($_.Vm.Name)"
    } catch {
      return
    }
  }
}
```

The code in Listing 22.5 gives you a simple list of VM names that are being protected by SRM. Although this is useful, it is arguably more useful to see which VMs are being replicated but not protected, which is demonstrated in Listing 22.6. This would imply that you have virtual machines in replicated datastores but have not been added to the protection plan. Note that this will only work when using vSphere Protection.

### LISTING 22.6 Showing unprotected virtual machines

```powershell
$srmApi = $global:DefaultSrmServers[0].ExtensionData

# a local protection group
$protectionGroup = $srmApi.Protection.ListProtectionGroups() |
  Where-Object {
    $_.GetInfo().Name -eq $localPlanName
}

# get the MoRef for each of the VMs
$Vms = (Get-Cluster $clusterName | Get-VM).ExtensionData.MoRef

# get the virtual machines which can be protected
$protectionGroup.QueryVmProtection($Vms) | Where-Object {
  $_.Status -ne "IsProtected"
} | ForEach-Object {
  $_.Vm.UpdateData("name")
  $_.Vm.Name
}
```

## Protecting Virtual Machines

To gain value from SRM, you want to make sure that virtual machines are protected by the protection plan. Even if the virtual machine is created in a datastore that is protected by either host-based or array-based replication that SRM is aware of, it will still not be protected by the plan.

To add the virtual machine to a protection group, you need to execute the ProtectVms method on the object. We have created a function to abstract this functionality and pipelining of the virtual machine object in order to simplify workflow. Listing 22.7 shows the function that adds a virtual machine to a protection plan.

### LISTING 22.7 The Add-SrmProtection function

```powershell
function Add-SrmProtection {
  # SYNOPSIS
  Adds a virtual machine to an SRM protection group

  .EXAMPLE
  Get-VM $vmName | Add-SrmProtection -ProtectionGroup "Super Protected"
  Adds a virtual machine to SRM

  .PARAMETER VM
  The virtual machine to protect.

  .PARAMETER ProtectionGroup
  The name of the protection plan to add the VM to.

  .INPUTS
  [VMware.VimAutomation.ViCore.Impl.V1.Inventory.VirtualMachineImpl]
#>
[CmdletBinding()]
param(
  [parameter(
    Mandatory=$true,
    ValueFromPipeline=$true
  ))
  [VMware.VimAutomation.ViCore.Impl.V1.Inventory.VirtualMachineImpl]
  $VM,

  [parameter (Mandatory=$true)]
  [String]$ProtectionGroup
)
process {
  if ($global:DefaultSrmServers.length -lt 1) {
    throw "Not connected to SRM server"
  }

  $srmApi = $global:DefaultSrmServers[0].ExtensionData

  # get the protection group object
  $protectionGroup = $srmApi.Protection.ListProtectionGroups() |
    Where-Object { $_.GetInfo().Name -eq $ProtectionGroup }

  # if you are using vSphere Advanced Protection (VADP/VDR),
  # which is referred as Host Based Replication (HBR) by SRM,
  # then you will need to associate the VM with the protection
  # group before executing the ProtectVms operation. To do this,
  # uncomment the following code block:
  # if (
    $protectionGroup.ListAssociatedVms().MoRef -contains $VM.Id
  ) {
    Write-Verbose "Associating VM '$($VM.Name)' with protection \
    group '$($protectionGroup.GetInfo().Name)'

    $protectionGroup.AssociateVms($VM.Id)

    # create the spec to specify the VM to be protected
    $ProtectionSpec = New-Object VMware.VimAutomation.Srm.Views.SrmGroupVmProtectionSpec
    $ProtectionSpec.Vm = $VM.ExtensionData.MoRef

    # update the group to add the Vm
    $protectionGroup.ProtectVms(@($ProtectionSpec))
  }
}
```

You can take advantage of this by pipelining the virtual machines in a replicated datastore into the function.

Get-Datastore "Replicated" | Get-VM | Add-SrmProtection -ProtectionPlan $planName

## Unprotecting a Virtual Machine

Removing virtual machines that no longer require protection is important because it frees resources for those virtual machines that need the extra protection. Fewer virtual machines to power on at the destination means faster recovery. Less data to replication between sites means the replication may be able to happen faster, and provides a lower recovery point objective (RPO) and recovery time objective (RTO).
