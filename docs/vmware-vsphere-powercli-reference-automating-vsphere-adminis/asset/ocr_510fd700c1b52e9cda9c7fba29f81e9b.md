# LISTING 3.16 Adding a VMHost to a vDS

```
$VMHost = Get-VMHost 'vesxi06*'
$NetworkAdapters = $VMHost | \
Get-VMHostNetworkAdapter \
-Name vmnic2,vmnic3,vmnic4,vmnic5 -Physical
$VDSSwitch02 = Get-VDSSwitch -Name 'PROD01-VDS02'
Add-VDSSwitchVMHost -VDS $VDSSwitch02 -VMHost $VMHost
Add-VDSSwitchPhysicalNetworkAdapter -DistributedSwitch $VDSSwitch02 -NIC $NetworkAdapters -Confirm:$false
```

There you have-from nothing to a VDS ready to host VMs. Now, if you're thinking,"I bet that all could be combined into one step,"you'd be right! Take what you learned from the VDS listings and combine the steps into one single

If you wish to modify the pNIC mappings after the fact, you'll need to use the Remove-VDSSwitchPhysicalNetworkAdapter cmdlet, as shown in Listing 3.17.

# LISTING 3.17 Modifying an existing VDS-to-VMHost pNIC mapping

```
# Remove Adapters vmnic4 and vmnic5
$VMHost | Get-VMHostNetworkAdapter -Name vmnic4,vmnic5 -Physical | \
Remove-VDSSwitchPhysicalNetworkAdapter-Confirm:$false
```

If you need to remove a host completely, you can use the Remove-VDSSwitchVMHost cmdlet (Listing 3.18). You can remove a host (in our example, vesxi06) from the distributed switch (PROD01-VDS02). This cmdlet is easily handled if you're removing a vSphere host from vCenter Server.

# LISTING 3.18 Removing a VMHost from a VDS

```
$VMHost = Get-VMHost 'vesxi06*'
$VDSSwitch02 = Get-VDSSwitch -Name 'PROD01-VDS02'
$VDSSwitch02 | Remove-VDSSwitchVMHost -VMHost $VMHost -Confirm:$false
```

So, what about VMkernel network adapters in a DVPG? While a little more complicated than their VDS cousins, not only can they be used, but they can also be automated using PowerCLL. In Listing 3.19, we are creating a new VDS network adapter adapter that meets the following specifications:

+   - VDS: PROD-VDS02
- DVPG: vMotion, VLAN 853