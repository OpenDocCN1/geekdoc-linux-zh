$pciDevices [$strVendorId].deviceTab[$strDeviceId]

```
}
else{
objDevice.DeviceName = $strDeviceId
}
$hostDevices += $objDevice
}
```

```
# Find associated ESX storage devices
foreach ($hba in $_.ExtensionData.Config.StorageDevice.HostAdapter) {
$hostDevices | Where-Object {$_.Pci -match $hba.Pci} | Foreach-Object {$_.EsDeviceName = "[+${hba.device+"]"}
}
```

```
# Find associated ESX network devices
foreach ($nic in $_.ExtensionData.Config.Network.Pnic) {
$hostDevices | Where-Object {$_.Pci -match $nic.Pci} | Foreach-Object {$_.EsDeviceName = "[+${nic.device+"]"}
}
```

# Clusters

You retrieve cluster information by using the Get-Cluster cmdlet

```
Get-Cluster | FT -AutoSize
```

| Name HAEnabled HAFailoverLevel DrsEnabled DrsAutomationLevel |
|---|---|---|---||
| CL01 True | 1 | False | FullyAutomated |
| CL05 False | 1 | False | FullyAutomated |
| CL02 False | 1 | True | FullyAutomated |
| CL03 False | 1 | False | FullyAutomated |
| CL04 False | 1 | False | FullyAutomated |