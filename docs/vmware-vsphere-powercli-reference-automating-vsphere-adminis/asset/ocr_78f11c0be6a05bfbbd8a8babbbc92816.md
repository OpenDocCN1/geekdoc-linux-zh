# CHAPTER 6 • CREATING VIRTUAL MACHINES

]
[VMware.VimAutomationViCore.Impl.V1.Inventory.VMHostImpl]
$VMHost

[int]
$Version
Process

```
$HostSystem = Get-View -VIObject $VMHost -Property Parent
$compResource = Get-View -Id $HostSystem.Parent `
-Property EnvironmentBrowser
$EnvironmentBrowser = Get-View -Id $compResource.EnvironmentBrowser `
$VMConfigOptionDescriptors = =
$EnvironmentBrowser.QueryConfigOptionDescriptor
```

```
if ($Version)
{
Key = $VMConfigOptionDescriptors |
Where-Object {$_.key -match "$($Version)"} |
Select-Object -ExpandProperty Key
```

```
else
{
Key = $VMConfigOptionDescriptors |
Where-Object {$_.DefaultConfigOption} |
Select-Object -ExpandProperty Key
$EnvironmentBrowser.QueryConfigOption($Key,
$HostSystem.MoRef) |
Select-Object -ExpandProperty GuestOSDescriptor |
Select-Object @(
Name='GuestId'
Expression={$_.Id}
@(
Name='GuestFamily'
Expression={$_.Family}
```