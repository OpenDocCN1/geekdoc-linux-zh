
## LISTING 10.1 Getting the OVF metadata

```powershell
Get-OvfConfiguration \VMware-vCenter-Server-Appliance-6.0.0.ova
```

```
Common : System.Object
DeploymentOption : VMware.VimAutomation.ViCore.Impl.V1.Ovf.OvfPropertyImpl
IpAssignment : System.Object
NetworkMapping : System.Object
vami : System.Object
```

You can then leverage the metadata to programmatically deploy a complete vApp from any OVA/OVF. Listing 10.2 fully assures the deployment of the vCenter appliance.

## LISTING 10.2 Deploying vCenter Server appliance from PowerCLI

```powershell
# Read Metadata and create the configuration object
$Path = "\VMware-vCenter-Server-Appliance-6.0.0.ova"
$OvfConfig = Get-OvfConfiguration -Ovf $Path
```

```powershell
# Set all the required configuration parameters.
$OvfConfig.NetworkMapping.Network_1.Value = 'Public'
$OvfConfig.DeploymentOption.Value = 'tiny'
$OvfConfig.Common.guestinfo.cis.appliance.addr.family.Value = "ipv4"
$OvfConfig.Common.guestinfo.cis.appliance.net.mode.Value = "static"
$OvfConfig.Common.guestinfo.cis.appliance.net.addr_1.Value = "192.168.2.8"
$OvfConfig.Common.guestinfo.cis.appliance.net.prefix.Value = "24"
$OvfConfig.Common.guestinfo.cis.appliance.net.gateway.Value = "192.168.2.1"
$OvfConfig.Common.guestinfo.cis.appliance.net.dns.servers.Value = "192.168.2.1"
$OvfConfig.Common.guestinfo.cis.appliance.vmdir.password.Value = "VMware!"
$OvfConfig.Common.guestinfo.cis.appliance.root.password.Value = "VMware!"
$OvfConfig.Common.guestinfo.cis.appliance.time.tools_sync.Value = "True"
```

![](img/62596f5acc979040608a4e5111beb7d6_364_0.png)

```powershell
$OvfConfig.Common.guestinfo.cis.appliance.ssh.enabled.Value = "True"
```

```powershell
# create a hash table with all the configuration
$Splat = @{
  'Name' = 'VCSA'
  'VMHost' = (Get-VMHost ESX1)
  'Source' = $Path

  'OvfConfig' = $OvfConfig
  'DiskStorageFormat' = 'Thin'
}
```

## Import the vApp using Splat to inject parameters
```powershell
Import-VApp @Splat
```

Virtual appliances can simplify the deployment of a new VM. vApps bring simplicity at a scale that was previously only available to the largest hosting providers.

## Create Your Own vApps

vApps are a resource pool at their base, so when creating a new vApp, resource guarantees are where it all starts. There are three ways to create a new vApp in your environment.

- Create a new vApp.
- Clone an existing vApp.
- Import a vApp from an OVF/OVA.

Listing 10.3 creates a new vApp that conforms to the following specification:

- Name: App01
- Location: Cluster Prod1
- Reserve 4 GHz CPU
- Reserve 6 GB of RAM

## LISTING 10.3 Creating a vApp

```powershell
New-VApp -Name App01 \
-Location (Get-Cluster prod01) \
-CpuExpandableReservation $true \
-CpuReservationMhz 4000 \
-MemExpandableReservation $true \
-MemReservationGB 6
```

vApps can be cloned with the New-VApp cmdlet. As shown in Listing 10.4, App01 is cloned to a new vApp named App02. Be aware that when a vApp is cloned, the clone includes any child VMs or vApps.

## LISTING 10.4 Cloning an existing vApp

```powershell
New-VApp -Name App02 \
-Location (Get-Cluster prod01) \
-VApp (Get-VApp App01) \
-Datastore datastore
```

The third way to create a vApp is to import from one of OVF. This is often either as an inactive vApp backup or to copy vApps between vCenter servers. Before a vApp can be imported, it must first be exported. For that, PowerCLI provides the Export-VApp cmdlet. Like cloning, exporting a vApp results in the VMs being exported as well. This is very useful because it enables systems to be transported using one logical container. Nothing is lost in the move—settings as the startup order, IP address, and resource allocation are all encompassed in the exported OVF. Listing 10.5 exports App02 into an OVF container.

## LISTING 10.5 Exporting an existing vApp

```powershell
Export-VApp -App (Get-VApp App02) \
-Name "$app -Format (Get-Date)"
```

Once a vApp is exported, importing is similar to importing a virtual appliance. The difference is that when you import OVF, the whole vApp is re-created along with its child vApps and VMs. To import vApp App02 that was exported in Listing 10.5, simply point the Import-VApp cmdlet to the OVF file, VMHost, and a datastore (Listing 10.6).

## LISTING 10.6 Importing a vApp from OVF

```powershell
Import-VApp -Source App02.ovf \
-Name 'App02'
-VMHost 'ESX1'
-Datastore datastore
```

> NOTE If App02 exists on your system, the import will be unsuccessful.

To remove an existing vApp from the system, Remove-vApp cmdlet is provided within PowerCLI. By default the cmdlet will merely remove vApp from inventory. To permanently delete the vApp and delete the data from disk, you must apply the DeletePermanently switch. Listing 10.7 removes App02 from the environment, deleting its metadata and removing the child VMs from datastores.

## LISTING 10.7 Removing an existing vApp

```powershell
Remove-vApp -vApp App02 -DeletePermanently
```

Over the last few years, vApps have grown in importance and are now integral to advanced systems such as vCloud Director. They are on par with VMs when it comes to deployment options, with one notable exception: there is no way to target a specific hard drive or VM to a datastore when deploying a vApp. This leads to a two-step process when there is a need to spread the load. Deploy to a datastore large enough to hold the entire vApp, and then, after it's been deployed, Move individual disks and VMs to different datastores.

## Maintain vApps

With the basics of vApps established, the fun really starts: maintaining and modifying vApps, using not only as a provisioning mechanism but as a logical management container to group a service into a single container regardless of the number of VMs that comprise it. That is where the true power of apps begins to shine. To add an existing VM to a vApp, use the standard Move-VM cmdlet and target the vApp as destination (Listing 10.8).

## LISTING 10.8 Adding VMs to an existing vApp

```powershell
Get-VM Web01, Web02, SQL01 | Move-VM -Destination (Get-vApp -Name 'App01')
```

## Setting the Start Order

Start order sequencing is perhaps the most powerful feature of a vApp. By setting the start order, you ensure that any administrator can safely power on or off an application no matter how. Unfortunately, PowerCLI doesn't contain any cmdlets for managing the startup order. Listing 10.9 provides the Get-vAppStartOrder function for purpose.

## LISTING 10.9 The Get-vAppStartOrder function

```powershell
#
.SYNOPSIS
Get the vApp Startup Order for a given VM
.DESCRIPTION
Get the vApp Startup Order for a given VM if no VM is provided will return the startup order for every VM in the vApp.
.PARAMETER VM
VM to retrieve the startup order for.
.PARAMETER vApp
vApp to retrieve the startup order from.
.EXAMPLE
Get-VM | Get-vAppStartOrder
.EXAMPLE
Get-vAppStartOrder -VM (Get-VM sql01)
#
function Get-vAppStartOrder {
  [CmdletBinding()]
  Param(
    [parameter (ValueFromPipeline=$true)]
    [VMware.VimAutomation.ViCore.Impl.V1.Inventory.VirtualMachineImpl]
    $VM,

    [parameter (ValueFromPipeline=$true)]
    [VMware.VimAutomation.ViCore.Impl.V1.Inventory.VAppImpl]
    $vApp
  )
  Process {
    if ($VM) {
      try {
        $vApp = Get-VIObjectByLayerView $VM.ExtensionData.ParentVApp
      } catch {
        Write-Warning "$($VM.name) doesn't belong to a vApp."
        continue;
      }
    } else if (-vApp) {
      Write-Warning 'vApp was not specified'
      break;
    }
    $vApp.ExtensionData.VAppConfig.EntityConfig | Where-Object {$_.Key -match $VM.Id} | Select-Object @{
      Name='VM'
      Expression={Get-VIObjectByLayerView $_}
    }, @{
      Name='vApp'
      Expression={$vApp.name}
    },
    'StartOrder','StartDelay',
    'WaitingForGuest','StartAction',
    'StopDelay','StopAction',
    @{
      Name='DestroyWithParent'
      Expression={if ($_.DestroyWithParent -eq $null){
        $false
      } else {
        $_.DestroyWithParent
      }}
    }
  }
}
```

Listing 10.10 retrieves the current start order settings using the Get-vAppStartOrder function.

## LISTING 10.10 Getting the start order settings for the App01 vApp

```powershell
Get-VApp App01 | Get-vAppStartOrder
```

| VM | vApp | StartOrder | StartDelay | WaitingForGuest | StartAction | StopDelay | StopAction | DestroyWithParent |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Web01 | App01 | 1 | 120 | False | powerOn | 120 | powerOff | False |
| Web02 | App01 | 2 | 120 | False | powerOn | 120 | powerOff | False |
| SQL01 | App01 | 3 | 120 | False | powerOn | 120 | powerOff | False |
