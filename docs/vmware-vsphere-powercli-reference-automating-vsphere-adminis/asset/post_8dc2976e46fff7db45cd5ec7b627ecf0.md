
## SET UP THE NETWORK

Select-Object -ExpandProperty MoRef

```powershell
try {
    Get-VIObjectByVIView `
    $dvSwitchManager.QueryCompatibleHostForExistingDvs($MoRef,
    $r, $Vds.MoRef)
} catch {
    Write-Warning "No compatible host found in ($VIObject.name)"
}
```

For the next exercise, we're interested in identifying any VMHost in the Prod01 datacenter that is capable of being added to our new VDS (Listing 3.15).

## LISTING 3.15 Finding VDS VMHost candidates

```powershell
Get-Datacenter PROD01 | Get-DistributedSwitchCandidate -DistributedSwitch 'PROD01-VDS02' -Recurse
```

| Name | ConnectionState | PowerState |
|---|---|---|
| vesxi05.sunndyle... | Connected | PoweredOn |
| vesxi06.sunndyle... | Connected | PoweredOn |

The code in Listing 3.15 specifically located two vSphere hosts that can be added to our new VDS. Next, identify the pNIC that will bind to the VDS uplinks. Remember, you can use the Get-VMHostDetailedNetworkInfo function from Listing 3.2 to help identify the correct pNICs to assign the right places.

Now you're ready to add your hosts. To accomplish this task, use the code shown in Listing 3.6 to add the following:

- VMHost: vesxi06
- pNIC: vmnic2, vmnic3, vmnic4, vmnic5
- vDS: PROD01-VDS02

## LISTING 3.16 Adding a VMHost to a vDS

```powershell
$VMHost = Get-VMHost 'vesxi06*'
$NetworkAdapters = $VMHost | \
Get-VMHostNetworkAdapter \
-Name vmnic2,vmnic3,vmnic4,vmnic5 -Physical
$VDSSwitch02 = Get-VDSSwitch -Name 'PROD01-VDS02'
Add-VDSSwitchVMHost -VDS $VDSSwitch02 -VMHost $VMHost
Add-VDSSwitchPhysicalNetworkAdapter -DistributedSwitch $VDSSwitch02 -NIC $NetworkAdapters -Confirm:$false
```

There you have-from nothing to a VDS ready to host VMs. Now, if you're thinking, "I bet that all could be combined into one step," you'd be right! Take what you learned from the VDS listings and combine the steps into one single step.

If you wish to modify the pNIC mappings after the fact, you'll need to use the Remove-VDSSwitchPhysicalNetworkAdapter cmdlet, as shown in Listing 3.17.

## LISTING 3.17 Modifying an existing VDS-to-VMHost pNIC mapping

```powershell
# Remove Adapters vmnic4 and vmnic5
$VMHost | Get-VMHostNetworkAdapter -Name vmnic4,vmnic5 -Physical | \
Remove-VDSSwitchPhysicalNetworkAdapter -Confirm:$false
```

If you need to remove a host completely, you can use the Remove-VDSSwitchVMHost cmdlet (Listing 3.18). You can remove a host (in our example, vesxi06) from the distributed switch (PROD01-VDS02). This cmdlet is easily handled if you're removing a vSphere host from vCenter Server.

## LISTING 3.18 Removing a VMHost from a VDS

```powershell
$VMHost = Get-VMHost 'vesxi06*'
$VDSSwitch02 = Get-VDSSwitch -Name 'PROD01-VDS02'
$VDSSwitch02 | Remove-VDSSwitchVMHost -VMHost $VMHost -Confirm:$false
```

So, what about VMkernel network adapters in a DVPG? While a little more complicated than their VDS cousins, not only can they be used, but they can also be automated using PowerCLI. In Listing 3.19, we are creating a new VDS network adapter that meets the following specifications:

- VDS: PROD-VDS02
- DVPG: vMotion, VLAN 853
- vSphere host: vesxi06
- IP: 192.168.2.40/24
- vMotion enabled

NOTE If you are following the examples in order, be sure to re-Listing 3.16 at this point so that you have a host added to the VDS, before running Listing 3.19.

![](img/62596f5acc979040608a4e5111beb7d6_128_0.png)

PART I

## Listing 3.19 Creating network adapters on a DVPG

```powershell
$VMHost = Get-VMHost 'vesxi06'
$VDSwitch2 = Get-DVSwitch -Name 'PROD01-VDS02'
$vMotionDVPG = $VDSwitch | New-DVPortgroup -Name 'vMotion' -VlanId 853
$vmk = New-VMHostNetworkAdapter -VMHost $VMHost \
-PortGroup $vMotionDVPG -VirtualSwitch $VDSwitch2 \
-IP 192.168.2.40 -SubnetMask 255.255.255.0
$vmk | Set-VMHostNetworkadapter -vMotionEnabled:$true -Confirm:$false
```

Follow-on management is straightforward with the Set-VMHostNetworkAdapter cmdlet for updating settings and Remove-VMHostNetworkAdapter for removing an adapter.

You will quickly realize the power these functions provide when you have to do something such as enable fault tolerance (FT) on a VMware adapter across an entire cluster. As shown in Listing 3.20, even this task is a snap in PowerCLI.

## Listing 3.20 Enabling FT logging across a cluster

```powershell
[System.Collections.Array]$IPAddresses = '192.168.5.10', '192.168.5.11'
$VDSwitch2 = Get-VDSwitch -Name 'PROD01-VDS02'
$FTDVPG = $VDSwitch2 | New-DVPortgroup -Name 'FT' -VlanId 700
foreach ($VMHost in (Get-Cluster Cluster01 | Get-VMHost)) {
    $vmkFT = New-VMHostNetworkAdapter -VMHost $VMHost \
    -PortGroup $FTDVPG -VirtualSwitch $VDSS02 \
    -IP $IPAddresses[0] -SubnetMask 255.255.255.0
    $vmkFT | Set-VMHostNetworkAdapter \
      -FaultToleranceLoggingEnabled:$true -Confirm:$false
    $IPAddresses.RemoveAt(0)
}
```

## Creating a Copy of a Distributed Switch

If there is a requirement to deploy a new distributed switch, it might require configuration consistent with those already existing in vCenter for items such as the Discovery Protocol and the Administrator Contact details. The VDS module contains a method to do this via the New-VSwitch cmdlet. Listing 3.21 demonstrates how to copy the configuration from the PROD01-VDS02 VDS to create a new use of the -WithoutPortGroups if the port groups do not have to be copied.

## LISTING 3.21 Creating a Copy of a VDS

```powershell
$Datacenter = Get-Datacenter -Name 'PROD01'
$VDSwitch02 = Get-VDSwitch -Name 'PROD01-VDS02'
$VDSwitch02 | New-VSwitch -Name 'PROD01-VDS02-Copy' -Location $Datacenter -WithoutPortGroups
```

## Back Up and Restore a Distributed Switch

More functionality included with the VDS module is the possibility to back up the configuration of a DVS and to later restore that file to vCenter.

## LISTING 3.22 Backing up a switch

```powershell
Get-VDSwitch -Name 'PROD01-VDS02' | Export-VDSwitch -Path "C:\Scripts\PROD01-VDS02.zip"
```

## LISTING 3.23 Restoring a distributed switch

```powershell
Import-VDSwitch -Name 'PROD01-VDS02' -Path "C:\Scripts\PROD01-VDS02.zip"
```

## Moving VMs to a New Port Group

A common admin task is moving VMs from one port group to another. Maybe there are behind-the-scenes networking changes that involve a redesign of the network, a change to VLANs, or possibly a migration from standard to switches. The Move-VMToNewGroup function takes source and target port groups as input, each VM in the source port group, and moves them to the new port group (Listing 3.24).

## LISTING 3.24 Moving VMs from one port group to another

```powershell
function Move-VMToNewGroup {
    .SYNOPSIS
    Move VMs from one Port Group to another.
    .DESCRIPTION
    Move VMs from one Port Group to another.
    .PARAMETER Source
    Name of Port Group to move from
    .PARAMETER Target
    Name of Port Group to move to
    .PARAMETER Cluster
    Name of Cluster containing Vms
    .EXAMPLE
    Move-VMToNewGroup -Source PortGroup1 -Target PortGroup2 -Cluster Cluster01

    [CmdletBinding(SupportsProcess=$true)]
    Param(
        [parameter(Mandatory=$true, HelpMessage='Name of Port Group to move from')]
        [ValidateNotNullOrEmpty()]
        [string]$Source,

        [parameter(Mandatory=$true, HelpMessage='Name of Port Group to move to')]
        [ValidateNotNullOrEmpty()]
        [string]$Target,

        [parameter(Mandatory=$false)]
        [ValidateNotNullOrEmpty()]
        [string]$Cluster
    )
    process {
        try {
            if ($Cluster) {
                Get-Cluster $Cluster | Get-VM | Get-NetworkAdapter |
                Where-Object {$_.NetworkName -eq $Source } |
                Set-NetworkAdapter -portgroup $Target -Confirm:$false
            } else {
                Get-VM | Get-NetworkAdapter |
                Where-Object {$_.NetworkName -eq $Source } |
                Set-NetworkAdapter -portgroup $Target -Confirm:$false
            }
        } catch [Exception] {
            throw "Unable to move VMs from source to target Port Group"
        }
    }
}
```
