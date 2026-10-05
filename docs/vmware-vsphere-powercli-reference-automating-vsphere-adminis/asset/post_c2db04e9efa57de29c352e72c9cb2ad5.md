
```powershell
{
  'VendorUrl':
{
    spec.Product[0].Info.VendorUrl = $vendorUrl
    $msg = "{0} vendor URL:{1}" - f $msg, $vendorUrl
  },
  'ProductUrl':
{
    spec.Product[0].Info.ProductUrl = $productUrl
    $msg = "{0} product Url:{1}" - f $msg,
    $productUrl
  },
  'AppUrl':
{
    spec.Product[0].Info.AppUrl = $AppUrl
    $msg = "{0} App Url:{1}" - f $msg, $AppUrl
  }
}
if ($PSCmdlet.ShouldProcess($vApp.Name, $msg)) {
  $vApp.ExtensionData.UpdateVAppConfig($spec)
  if ($?) {
    Start-Sleep -Milliseconds 500
    Get-vAppProductInfo -vApp $vApp
  } else {
    Write-Warning "Failed to set vApp product info check"
  }
}
```

Using the Set-vAppProductInfo function, you can configure the product information on a custom or home-grown vApp, as seen in Listing 10.28.

# LISTING 10.28 Configuring product information for App01

```powershell
Set-vAppProductInfo -Name App01 \
  -Vendor Acme -version 1.1 \
  -FullVersion 1.1.0.1 \
  -VendorURL www.acme.com \
  -ProductUrl www.acme.com/go/App01

vApp                  : App01
Name         : App01
Vendor       : Acme
Version      : 1.1
FullVersion  : 1.1.0.1
VendorURL    : www.acme.com
ProductUrl   : www.acme.com/go/App01
AppUrl       :
```

Although vApps haven't taken over the world as we predicted in the previous edition, they are still extremely powerful and should be part of any vSphere infrastructure—if for nothing else than control the startup and shutdown order of a complex virtual application. Either way, using the tools provided in this chapter, any administrator can easily automate vApp operations in a repeatable means with PowerCLI.

# Securing Your vSphere Environment

- CHAPTER 11: BACKING UP AND RESTORING YOUR VIRTUAL MACHINES
- CHAPTER 12: ORGANIZE YOUR DISASTER RECOVERY
- CHAPTER 13: HARDENING THE VSPHERE ENVIRONMENT
- CHAPTER 14: MAINTAIN SECURITY IN YOUR VSPHERE ENVIRONMENT

# Backing Up and Restoring Your Virtual Machines

IN THIS CHAPTER, YOU WILL LEARN TO:

- WORK WITH SNAPSHOTS 376
- CREATE DO-IT-YOURSELF BACKUPS 376
- RESTORE YOUR VMS FROM A DIY BACKUP 381
- CHANGE BLOCK TRACKING 382
  Checking CBT Status. ............................................ 383
  Enabling/Disabling CBT. ............................................ 383
- PROVIDE POWERSHELL SUPPORT FOR CORPORATE BACKUP APPLICATIONS 386
  Dell ................................................................................ 387
  Veeam ............................................................................... 392

# CHAPTER 11 • BACKING UP AND RESTORING YOUR VIRTUAL MACHINES

One of the most critical areas of any infrastructure—whether or not is virtual—is backup, the replication of key data to an alternate location in case of data or hardware loss. Many organizations have a full backup strategy with complex replication scenarios and standby on separate sites in case a disaster strikes. Other aspects of backup protect the system administrator and the users of the virtual infrastructure and their VMs from more day-to-day data or operating system corruption. This chapter will show how you can use PowerCLI in both of these areas to help back up your VMs and also how you can use a PowerShell-enabled product from a third-party vendor to automate your backup tasks.

# CHAPTER 11

## Work with Snapshots

Using VMware snapshots can be a great way to enable a quick and easy method to return to a particular point in time without needing to restore backups. A snapshot captures the state of a virtual machine and its configuration. Snapshots are a powerful tool for the VMware administrator as, once created, act as a safety net ensuring any changes to the VM can be reverted. They are a restore point and should be created prior to installing new software, patching operating systems, or even making configuration changes. If you are unfamiliar with creating, maintaining, and restricting the creation of snapshots, see Chapter 9, “Advanced Virtual Machine Features"

> Because of the way in which snapshots are created, they are a great mechanism for a quick backup plan, but do not leave them in place for a long time, as could cause issues with space on datastores or reduced speed and performance when multiple snapshots are created on the same VM. Remember to keep track of them and remove snapshots that are no longer needed. You might also find it useful to restrict the creation of snapshots in your environment. You'll find scripts to assist you with these tasks in Chapter 9.

## Create Do-It-Your Backups

Many organizations employ complex, commercially available products for backups. But what if you wanted to perform your own backups? Perhaps you want to copy your VM offsite to another datacenter—set, and waiting to protect in the event of disaster. Perhaps you just want to make a copy of the VM or VMs on a scheduled basis to ensure that your data has a backup. With the code in Listing 11.1, you can make a copy of the VMs to an alternate datastore. The script creates a snapshot of the VM and then, from this snapshot, it clones the image to create a new VM on an alternate datastore. The script can backed up one or more VMs. As written, the log currently outputs to screen, but you can easily write to a log file or email the details as they are completed.

# LISTING 11.1 DIY backups

```powershell
function Backup-VM {
.SYNOPSIS
Backs up a virtual machine to specified datastore.
.DESCRIPTION
The function will back up a virtual machine to a given datastore.
.PARAMETER VM
The Virtual Machine to back up
.PARAMETER Datastore
The datastore to use when creating the backup
.INPUTS
String,System.Management.Automation.PSObject
.OUTPUTS
VMware.VimAutomation.Core.Impl.V1.VirtualMachine
.EXAMPLE
Backup-VM -VM Server01 -Datastore "NFS1"
.EXAMPLE
Get-VM Test01,Test02 | Backup-VM -Datastore "NFS1"
[CmdletBinding(SupportsProcess,Confirm="High")]
[OutputType('VMware.VimAutomation.Core.Impl.V1.VirtualMachine[]')]
Param(
  [parameter(Mandatory=$true,ValuePipeline=$true)]
  [PSObject[]]$VM,

  [parameter(Mandatory=$true,ValidateNotNullEmpty()]
  [PSObject]$Datastore
)

begin {
  # -- Set date for clone names
  $Date = Get-Date -Format "yyyyMMdd"

  # -- Check the Datastore
  if ($Datastore.GetType().Name -eq "string") {
    try {
      $Datastore = Get-Datastore $Datastore -ErrorAction Stop
    }
    catch [Exception]{
      throw "Datastore $Datastore does not exist"
    }
  }
  elseif ($Datastore -isnot [VMware.VimAutomation.Core.Impl.V1.Datastore.NasDatastore] -or $Datastore -isnot [VMware.VimAutomation.Core.Impl.V1.Datastore.VmfsDatastore]) {
    throw "You did not pass a string or a Datastore"
  }
}

process {
  try {
    foreach ($CurrentVM in $VM) {
      if ($CurrentVM.GetType().Name -eq "string") {
        try {
          $CurrentVM = Get-VM $CurrentVM -ErrorAction Stop
        } catch [Exception]{
          Write-Warning "VM $CurrentVM does not exist"
          continue
        }
      }
      else ($CurrentVM -isnot [VMware.VimAutomation.Core.Impl.V1.VirtualMachine]) {
        Write-Warning "You did not pass a string or a VM object"
        continue
      }

      Write-Verbose "$($CurrentVM.Name) Backing up"
      Write-Verbose "$($CurrentVM.Name) Creating Snapshot"

      if ($PSCmdlet.ShouldProcess($CurrentVM)) {
        # --- Create snapshot for clone
        $CloneSnap = $CurrentVM | New-Snapshot -Name "Snapshot created on $(Date by backup script)"

        # - Get managed object view
        $VMView = $CurrentVM | Get-View -Property Parent, Snapshot

        # --- Get folder managed object reference
        $CloneFolder = $VMView.Parent
        $CloneVM = "BAK-$CurrentVM-$Date"

        Write-Verbose "$($CurrentVM.Name) Cloning from snapshot to $CloneVM"

        # Build clone specification
        $CloneSpec = New-Object Vmare.Vim.VirtualMachineCloneSpec
        $CloneSpec.Snapshot = $VMView.Snapshot.CurrentSnapshot

        # Make linked disk specification
        $CloneSpec.Location = New-Object Vmare.Vim.VirtualMachineRelocateSpec
        $CloneSpec.Location.Datastore = $Datastore.Id
        $CloneSpec.Location.Transform = [Vmware.Vim.VirtualMachineRelocateTransformation]::flat

        # Create clone
        $CreateClone = $VMView.CloneVM($CloneFolder, $CloneVM, $CloneSpec)

        Write-Verbose "$($CurrentVM.Name) Clone created"
        Write-Verbose "$($CurrentVM.Name) Removing Snapshot"

        # Remove Snapshot created for clone
        Get-Snapshot -VM (Get-VM -Name $CurrentVM) -Name $CloneSnapshot
        Remove-Snapshot -confirm:$False
        Write-Verbose "$($CurrentVM.Name) Backup completed"

        # Output the VM object
        $OutputVM = Get-VM $CloneVM
        Write-Output $OutputVM
      }
    }
  }
}
```
