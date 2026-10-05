# SET UP THE NETWORK

97

+   - vSphere host: vesxi06

+   - IP: 192.168.2.40/24

+   - vMotion enabled

NOTE If you are following the examples in order, be sure to re- Listing 3.16 at this point so that you have a host added to the VDS, before running Listing 3.19.

![](bbox=[0.206, 0.215, 0.256, 0.253])

PART I

# Listing 3.19 Creating network adapters on a DVPG

```
$VMHost = Get-VMHost 'vesxi06'
$VDSwitch2 = Get-DVSwitch -Name 'PROD01-VDS02'
$vMotionDVPG = $VDSwitch | New-DVPortgroup -Name 'vMotion'
-VlanId 853
$vmk = New-VMHostNetworkAdapter -VMHost $VMHost
-PortGroup $vMotionDVPG -VirtualSwitch $VDSwitch2
-IP 192.168.2.40 -SubnetMask 255.255.255.0
$vmk | Set-VMHostNetworkadapter -vMotionEnabled:$true
-Confirm:$false
```

Follow-on management is straightforward with the Set-VMHostNetworkAdapter cmd-let for updating settings and Remove-VMHostNetworkAdapter for removing an adapter.

You will quickly realize the power these functions provide when you have to do something such as enable fault tolerance (FT) on a VMware adapter across an entire cluster. As shown in Listing 3.20, even this task is a snap in PowerCLI.

# Listing 3.20 Enabling FT logging across a cluster

```
[System.Collections.Array]$IPAddresses = '192.168.5.10',
192.168.5.11'
$VDSwitch2 = Get-VDSwitch -Name 'PROD01-VDS02'
$FTDVPG = $VDSwitch2 | New-DVPortgroup -Name 'FT' -VlanId 700
foreach ($VMHost in (Get-ClusterCluster01 | Get-VMHost)) {
$vmkFT = New-VMHostNetworkAdapter -VMHost $VMHost \
-PortGroup $FTDVPG -VirtualSwitch $VDSwitch02 \

```