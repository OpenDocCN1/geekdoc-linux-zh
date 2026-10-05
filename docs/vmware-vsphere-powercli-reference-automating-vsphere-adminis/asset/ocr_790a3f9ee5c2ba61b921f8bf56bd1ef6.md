# OPTIMIZE STORAGE USAGE WITH THIN PROVISIONING

Copy-HardDisk -HardDisk $esxHardDisk \
-DestinationPath $thinFile \
-DestinationStorageFormat "thin" | Out-Null
Disconnect-VIServer $esxHost -Confirm:$false

```
$spec = New-Object VObject.Vim.VirtualMachineConfigSpec
$spec.device = New-Object \
VMware.Vim.VirtualDeviceConfigSpec[] (2)
$spec.device[0] = New-Object \
VMware.Vim.VirtualDeviceConfigSpec
$spec.device[0].operation = "remove"
if ($replace) {
$spec.device[0].fileOperation = "destroy"
$spec.device[0].device = $HardDisk.ExtensionData
}
$spec.device[1] = New-Object \
VMware.Vim.VirtualDeviceConfigSpec
$spec.device[1].operation = "add"
$spec.device[1].device = New-Object \
VMware.Vim.VirtualDisk
$spec.device[1].device.key = -100
$spec.device[1].device.backing = New-Object \
VMware.Vim.VirtualDiskFlat2BackingInfo
$spec.device[1].device.backing.fileName = \
$thinFile
$spec.device[1].device.backing.diskMode = \
"persistent"
$spec.device[1].device.backing.thinProvisioned = \
$true
$spec.device[1].device.controllerKey = \
$HardDisk.ExtensionData.ControllerKey
$spec.device[1].device.unitNumber = \
$HardDisk.ExtensionData.UnitNumber
```

![](bbox=[0.898, 0.237, 0.958, 0.372])