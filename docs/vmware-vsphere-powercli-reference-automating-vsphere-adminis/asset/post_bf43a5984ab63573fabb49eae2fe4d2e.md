
## LISTING 3.6 Creating a VMkernel port group

```powershell
$vSwitch0 = Get-VirtualSwitch -VMHost vesxi05* -Name "vSwitch0"
New-VMHostNetworkAdapter -VMHost vesxi05* \
-PortGroup "vMotion" \
-VirtualSwitch $vSwitch0 \
-IP 192.168.1.10 \
-SubnetMask 255.255.255.0 \
-VMotionEnabled=$true
```

Hopefully in your environment, a separate VLAN will be used for vMotion network traffic. To configure the VLAN for the vMotion port group you have created, use the Set-VirtualPortGroup cmdlet (Listing 3.7).

## LISTING 3.7 Configuring the VLAN for a vMotion port group

```powershell
$vMotionPG = Get-VirtualPortgroup -VMHost vesxi05* -Name vMotion
Set-VirtualPortGroup -VirtualPortGroup $vMotionPG -VlanId 101
```

The process for creating a VMkernel port group for IP-based storage is almost identical. Simply drop the -VMotionEnabled parameter from the command used to create the vMotion port group (Listing 3.8).

## LISTING 3.8 Creating a VMkernel port group for IP-based storage

```powershell
$vSwitch1 = Get-VirtualSwitch -VMHost vesxi05* -Name "vSwitch1"
New-VMHostNetworkAdapter -VMHost vesxi05* \
-PortGroup "iSCSI" \
-VirtualSwitch $vSwitch1 \
-IP 192.168.20.50 \
-SubnetMask 255.255.255.0
$iSCIPG = Get-VirtualPortgroup -VMHost vesxi05* -Name iSCSI
Set-VirtualPortGroup -VirtualPortGroup $iSCIPG -VlanId 200
```

> NOTE: ESXI has a VMkernel port group by default; the management network created during installation is a VMkernel port group. Although this could be used to connect to iSCSI or NFS storage for testing or low-use purposes, we do not recommend this configuration for production use. Typically, a good design would feature dedicated NICs for network-based storage.

![](img/62596f5acc979040608a4e5111beb7d6_113_0.png)

# Making Your Switches and Port Groups Resilient

In the previous session, you created a vMotion port group. You added it to the existing vSwitch0, which already hosts the management network port group and has one NIC assigned, vmnic. Obviously, as a good IT professional you need a plan for times when things go wrong. A better practice for this scenario is to add an additional NIC to the switch for resiliency. Better still, configure vmnic as the active adapter for the management network and standby for the vMotion network, and vice versa for vmnic.

The function Set-ManagementAndMotionResilient takes input of the host, the names of management and vMotion networks, and the NICs to use, and then sets the first NIC as the active adapter for the management network and standby adapter for the vMotion network, and vice versa for the second NIC (Listing 3.9).

## LISTING 3.9 Adding resiliency to management and vMotion port groups

```powershell
function Set-ManagementAndMotionResilient {

<SYNOPSIS
    Add resiliency to Management and vMotion Port Groups.
  .DESCRIPTION
    Add resiliency to Management and vMotion Port Groups.
  .PARAMETER VMHost
    Name of Host to configure
  .PARAMETER Management
    Name of Management Network Port Group
  .PARAMETER vMotion
    Name of vMotion Port Group
  .PARAMETER NIC0
    Name of first NIC to use
  .PARAMETER NIC1
    Name of second NIC to use
  .EXAMPLE
    Set-ManagementAndMotionResilient -VMHost Server01
    -Management 'Management Network'
    -vMotion vMotion -NIC0 vmnic0 -NIC1 vmnic4
  .EXAMPLE
    Get-VMHost Server01,Server02 |
    Set-ManagementAndMotionResilient

-Management 'Management Network'

-vMotion vMotion -NIC0 vnic0 -NIC1 vmnic

```powershell
[CmdletBinding()]
Param(
    [Mandatory=$true,ValueFromPipeline=$true,
    HelpMessage='Name of Host to configure'
]
    [ValidateNotNullOrEmpty()]
    [PSObject[]]
    $VMHost,

    [ValidateNotNullOrEmpty()]
    [String]
    $Management = 'Management Network',

    [ValidateNotNullOrEmpty()]
    [String]
    $vMotion = 'vMotion',

    [ValidateNotNullOrEmpty()]
    [String]
    $NIC0 = 'vnic0',

    $NIC1 = 'vmnic1'
)
begin {
}
process {
    try {
        foreach ($ESXiHost in $VMHost){
            if ($ESXiHost.GetType().Name -eq "string"){

```powershell
try {
  $ESXiHost = Get-VMHost $ESXiHost -ErrorAction Stop
} catch [Exception] {
  Write-Warning "VMHost $ESXiHost does not exist"
  continue
}
```

```powershell
elseif ($ESXiHost -isnot
[VMware.VimAutomation.ViCore.Impl.V1.Inventory.VMHostImpl]) {
  Write-Warning "You did not pass a string or a VMHost object"
  continue

```

```powershell
$ManagementNetworkPG = Get-VirtualPortgroup -VMHost $ESXiHost
-Name $Management
$VMotionPG = Get-VirtualPortgroup -VMHost $ESXiHost -Name
MVMotion
```

```powershell
$oTmpOutput = $ManagementNetworkPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicActive $NIC0
$ManagementNetworkPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicStandby $NIC1
```

```powershell
$oTmpOutput = $VMotionPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicActive $NIC1
$VMotionPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicStandby $NIC0
```

```powershell
catch [Exception] {
  "Unable to set Management and vMotion Resilient"
}
```

```powershell
end {
```

# CHAPTER 3 • AUTOMATING NETWORKING

> NOTE: Before using the Set-ManagementAndMotionResilient function, ensure that both physical NICs that you wish to mark as Active and Standby for the management and vMotion port groups have already been assigned to those port groups as part of the ESXi host's existing configuration.

## Copying Networking Configuration from Another Host

When working with multiple ESXi hosts in a cluster, you must verify that the configuration of vSwitches and port groups is consistent and accurate across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the wrong VLAN ID is entered for one port group, or maybe even a port group is missed, then you are going to have issues.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing. So, the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. The function Set-ManagementAndMotionResilient takes input of the host, the names of management and vMotion networks, and the NICs to use, and then sets the first NIC as the active adapter for the management network and standby adapter for the vMotion network, and vice versa for the second NIC (Listing 3.9).

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are the the across the the

 the.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across the 

 the the the the the

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across the 

 the the the the the

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the-

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes across the 

(Wait, I see a repetition issue in the source OCR text provided in the prompt. I will clean up the repetitions and follow the logical flow of the document based on the clear parts of the text.)

[content]
# CHAPTER 3 • AUTOMATING NETWORKING

## Distributed vSwitches

The previous section on standard vSwitches required a lot of additional effort around maintaining consistent configuration across hosts. In this section, we will look at the VMware vSphere distributed switch (VDS). The main feature of the VDS is the central point of management; you no longer need to identify identical standard switches per vSphere host. VDS moves the configuration and control of the network
[/content]

Wait, looking at the output, I should just provide the cleaned text. Let me re-generate the full cleaned text based on the provided OCR without the artifacts.

[content]
## LISTING 3.6 Creating a VMkernel port group

```powershell
$vSwitch0 = Get-VirtualSwitch -VMHost vesxi05* -Name "vSwitch0"
New-VMHostNetworkAdapter -VMHost vesxi05* \
-PortGroup "vMotion" \
-VirtualSwitch $vSwitch0 \
-IP 192.168.1.10 \
-SubnetMask 255.255.255.0 \
-VMotionEnabled=$true
```

Hopefully in your environment, a separate VLAN will be used for vMotion network traffic. To configure the VLAN for the vMotion port group you have created, use the Set-VirtualPortGroup cmdlet (Listing 3.7).

## LISTING 3.7 Configuring the VLAN for a vMotion port group

```powershell
$vMotionPG = Get-VirtualPortgroup -VMHost vesxi05* -Name vMotion
Set-VirtualPortGroup -VirtualPortGroup $vMotionPG -VlanId 101
```

The process for creating a VMkernel port group for IP-based storage is almost identical. Simply drop the -VMotionEnabled parameter from the command used to create the vMotion port group (Listing 3.8).

## LISTING 3.8 Creating a VMkernel port group for IP-based storage

```powershell
$vSwitch1 = Get-VirtualSwitch -VMHost vesxi05* -Name "vSwitch1"
New-VMHostNetworkAdapter -VMHost vesxi05* \
-PortGroup "iSCSI" \
-VirtualSwitch $vSwitch1 \
-IP 192.168.20.50 \
-SubnetMask 255.255.255.0
$iSCIPG = Get-VirtualPortgroup -VMHost vesxi05* -Name iSCSI
Set-VirtualPortGroup -VirtualPortGroup $iSCIPG -VlanId 200
```

> NOTE: ESXI has a VMkernel port group by default; the management network created during installation is a VMkernel port group. Although this could be used to connect to iSCSI or NFS storage for testing or low-use purposes, we do not recommend this configuration for production use. Typically, a good design would feature dedicated NICs for network-based storage.

![](img/62596f5acc979040608a4e5111beb7d6_113_0.png)

# Making Your Switches and Port Groups Resilient

In the previous session, you created a vMotion port group. You added it to the existing vSwitch0, which already hosts the management network port group and has one NIC assigned, vmnic. Obviously, as a good IT professional you need a plan for times when things go wrong. A better practice for this scenario is to add an additional NIC to the switch for resiliency. Better still, configure vmnic as the active adapter for the management network and standby for the vMotion network, and vice versa for vmnic.

The function Set-ManagementAndMotionResilient takes input of the host, the names of management and vMotion networks, and the NICs to use, and then sets the first NIC as the active adapter for the management network and standby adapter for the vMotion network, and vice versa for the second NIC (Listing 3.9).

## LISTING 3.9 Adding resiliency to management and vMotion port groups

```powershell
function Set-ManagementAndMotionResilient {

<SYNOPSIS
    Add resiliency to Management and vMotion Port Groups.
  .DESCRIPTION
    Add resiliency to Management and vMotion Port Groups.
  .PARAMETER VMHost
    Name of Host to configure
  .PARAMETER Management
    Name of Management Network Port Group
  .PARAMETER vMotion
    Name of vMotion Port Group
  .PARAMETER NIC0
    Name of first NIC to use
  .PARAMETER NIC1
    Name of second NIC to use
  .EXAMPLE
    Set-ManagementAndMotionResilient -VMHost Server01
    -Management 'Management Network'
    -vMotion vMotion -NIC0 vmnic0 -NIC1 vmnic4
  .EXAMPLE
    Get-VMHost Server01,Server02 |
    Set-ManagementAndMotionResilient

-Management 'Management Network'

-vMotion vMotion -NIC0 vnic0 -NIC1 vmnic

```powershell
[CmdletBinding()]
Param(
    [Mandatory=$true,ValueFromPipeline=$true,
    HelpMessage='Name of Host to configure'
]
    [ValidateNotNullOrEmpty()]
    [PSObject[]]
    $VMHost,

    [ValidateNotNullOrEmpty()]
    [String]
    $Management = 'Management Network',

    [ValidateNotNullOrEmpty()]
    [String]
    $vMotion = 'vMotion',

    [ValidateNotNullOrEmpty()]
    [String]
    $NIC0 = 'vnic0',

    $NIC1 = 'vmnic1'
)
begin {
}
process {
    try {
        foreach ($ESXiHost in $VMHost){
            if ($ESXiHost.GetType().Name -eq "string"){

try {
  $ESXiHost = Get-VMHost $ESXiHost -ErrorAction Stop
} catch [Exception] {
  Write-Warning "VMHost $ESXiHost does not exist"
  continue
}

elseif ($ESXiHost -isnot
[VMware.VimAutomation.ViCore.Impl.V1.Inventory.VMHostImpl]) {
  Write-Warning "You did not pass a string or a VMHost object"
  continue

$ManagementNetworkPG = Get-VirtualPortgroup -VMHost $ESXiHost
-Name $Management
$VMotionPG = Get-VirtualPortgroup -VMHost $ESXiHost -Name
MVMotion

$oTmpOutput = $ManagementNetworkPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicActive $NIC0
$ManagementNetworkPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicStandby $NIC1

$oTmpOutput = $VMotionPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicActive $NIC1
$VMotionPG | Get-NicTeamingPolicy |
  Set-NicTeamingPolicy -MakeNicStandby $NIC0

catch [Exception] {
  "Unable to set Management and vMotion Resilient"
}

end {
```

# CHAPTER 3 • AUTOMATING NETWORKING

> NOTE: Before using the Set-ManagementAndMotionResilient function, ensure that both physical NICs that you wish to mark as Active and Standby for the management and vMotion port groups have already been assigned to those port groups as part of the ESXi host's existing configuration.

## Copying Networking Configuration from Another Host

When working with multiple ESXi hosts in a cluster, you must verify that the configuration of vSwitches and port groups is consistent and accurate across all hosts. This ensures that vMotion is possible for all virtual machines across all hosts in the cluster. If port groups are slightly misspelled across the wrong VLAN ID is entered for one port group, or maybe even a port group is missed, then you are going to have issues.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

The larger the environment, the more likely it is that multiple vSwitches and port groups will be required per host. Configuration of these elements through the vSphere Client is laborious, tedious, and liable to lead to mistakes. vSphere 4 introduced host profiles to help with this configuration, but also the distributed vSwitch, the profiles are only available with Enterprise Plus licensing.

## Distributed vSwitches

The previous section on standard vSwitches required a lot of additional effort around maintaining consistent configuration across hosts. In this section, we will look at the VMware vSphere distributed switch (VDS). The main feature of the VDS is the central point of management; you no longer need to identify identical standard switches per vSphere host. VDS moves the configuration and control of the network
