# $VMHost = Get-Cluster Test | Get-VMHost -State Connected |
Get-Random
#Clone SQL01 to SQL01_Clone
$VM = New-VM -Name SQL01_Clone -VM $SourceVM -VMHost

That's as basic a clone operation can get; it is good and bad. An optimist pessimist would say that they have an exact copy of SQL01. The message here is to be extra careful with this virtual machine. Simply powering on SQL01 virtual machine. This can be overcome by cloning the machine with an OSCustomization task.

Let's just with the SQL virtual machine we created. SQL01 houses a critical database, and we want to be able to work on an upgradeにつき. To accomplish this, let's start cloning SQL01, this time applying an OSCustomization specification named SQL_TEST. Doing so will prepare the virtual machine with Sysprep and change the hostname and IP information in one shot. To be successful, the virtual machines network also needs to be changed to Dynamic Host Configuration Protocol (DHCP).

```
# Get source VM Object
$SourceVM = Get-VM -Name 'SQL01'
#Get a host within the Test cluster
$VMHost = Get-Cluster 'Test' | Get-VMHost -State Connected |
Get-Random
# Get the OS CustomizationSpec
$OSCustomizationSpec = Get-OSCustomizationSpec -Name 'SQL_TEST'
# Clone SQL01 to SQL01_clone
$VM = New-VM -Name 'SQL01_Clone' \
-VM $SourceVM \
-VMHost $VMHost \
-OSCustomizationSpec $OSCustomizationSpec
# Change the Network
Get-NetworkAdapter -VM $VM \
-Set-NetworkAdapter -Portgroup (Get-VDPortgroup -Name VLAN100) \
-Confirm:$false
# PowerOn once, triggering the CustomizationSpec
Start-VM -VM $VM
```

![](bbox=[0.905, 0.215, 0.965, 0.335])