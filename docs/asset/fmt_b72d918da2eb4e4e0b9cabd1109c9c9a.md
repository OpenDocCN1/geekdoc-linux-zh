
```powershell
# 对于硬件 v4 根据控制器的 SCSIPort 磁盘的 SCSTargetID 匹配磁盘。
# 不支持混合 scsi 适配器类型。
$DiskMatch = $WinWinds | Where-Object {$_.SCSIPort -eq $PortOffset
eq $VirtualSCSISController.BusNumber -and
$_.SCSTargetID -eq $VirtualDiskDevice.UnitNumber
}\else
{
# 对于硬件 v7+ 根据控制器的 pciSlotNumber 和磁盘的 SCSTargetID 匹配
$DiskMatch = $WinWinds | Where-Object {$_.CtrlPciSlotNumber -eq
($VM.ExtensionData.Config.ExtraConfig | Where-Object {$.key -match
"scsi"($VirtualSCSISController.BusNumber).pcislotnumber")}).value
-and $_.SCSTargetID -eq $VirtualDiskDevice.UnitNumber
}
{
$VirtualDisk.WindowsDisk = "Disk $($DiskMatch.Index)"
$VirtualDisk.WindowsDiskSizeGB = $DiskMatch.Size / 1 GB
}
```

## 第 8 章 • 配置虚拟机硬件

```powershell
else
{
    Write-Warning "No matching Windows disk found for SCSI ID" \
    ($virtualDisk.SCSI_Id)
    $VirtualDisk
}
```

```powershell
else
{
    Write-Error "Error Retrieving Windows disk info from guest"
}
```

在列表 8.4 中 `Get-VMDiskMapping` 函数的输出可以使用 `Format-Table` 命令以表格格式查看，或者更好的方法是是使用 `Out-Grid` 命令。图 8.2 显示了示例输出。

```powershell
$map = Get-VM App0 | Get-VMDiskMapping -guestCredential $guestCred
$map | Out-Grid
```

图 8.2 Get-VMDiskMapping 示例输出

![](img/62596f5acc979040608a4e5111beb7d6_315_0.png)

# 添加、配置和删除虚拟硬件

## 扩展虚拟磁盘

只要时间足够，几乎任何虚拟机（VM）最终都会耗尽磁盘空间。要扩展该磁盘，请使用 `Set-HardDisk` 命令。`-CapacityGB` 参数指定虚拟磁盘的新大小。例如，将虚拟机 VM0001 的虚拟磁盘“Hard disk 2”扩展到 10 GB，请使用以下命令：

```powershell
Get-VM VM0001 | Get-HardDisk -Name "Hard disk 2" \
Set-HardDisk -CapacityGB 10
```

扩展虚拟磁盘非常直观且容易实现。但扩展磁盘只是完成了一半工作。通常扩展磁盘是为了确保客操作系统分区达到容量上限。因此，也有必要扩展客操作系统分区以使用新添加的容量。但不必担心，`Set-HardDisk` 命令也支持客操作系统分区。

要扩展客操作系统分区，`Set-HardDisk` 命令会在后台调用 `Invoke-VMScript` 命令，并使用在指定客户上下文中运行在 VM 内部的脚本来扩展分区。这些脚本位于 PowerCLI 安装目录下的 `Scripts` 文件夹中。要指定特定分区，请使用 `-Partition` 参数。如果未使用此参数指定分区，则将扩展硬盘上的最后一个分区。可以通过指定不带冒号的驱动器号来指定 Windows 分区。这里存在一些限制：

- 在 Windows 中，要扩展多分区磁盘上不是最后一个一个的分区，该磁盘必须是动态磁盘（dynamic disk）。

- 在 Linux 上，当磁盘为多分区结构且不支持逻辑卷管理器（LVM）时，只能扩展最后一个分区。

扩展客操作系统分区目前仅支持 Windows XP SP3 或更高版本，以及 Linux RedHat Enterprise 5 上的 `ext3` 分区。

要将虚拟机 VM0001 上之前扩展的“Hard disk 2”扩展到 100GB 并扩展客操作系统分区，请使用以下命令：

```powershell
Get-VM VM0001 | Get-HardDisk -Name "Hard disk 2" \
Set-HardDisk -CapacityGB 100 \
-HostCredential $hostCredential \
-GuestCredential $guestCredential \
-ResizeGuestPartition -Partition E
```

![](img/62596f5acc979040608a4e5111beb7d6_316_0.png)

当被扩展的分区是系统磁盘时，将适用额外的限制：

- Linux 系统磁盘无法扩展。

- Windows 2003 和 Windows XP 需要一个辅助虚拟机（helper virtual machine）来扩展系统分区。

在 Windows 上，可以使用 `-HelperVM` 参数指定辅助虚拟机。当使用辅助虚拟机时，在扩展磁盘之前，与该磁盘及辅助虚拟机相关的所有 VM 必须关闭。当你使用辅助虚拟机调整磁盘大小时，磁盘将逐一调整大小，这会导致辅助虚拟机为每个磁盘反复开关机。此过程可能会减慢命令的性能。

例如，要扩展 VM001 的系统磁盘（其系统分区属于“Hard disk 1”），并使用 VM002 作为辅助虚拟机，在扩展磁盘之前，VM001 和 VM002 都需要关闭。请注意，列表 8.5 中使用的客户登录凭据是辅助虚拟机的客户登录凭据。

# 列表 8.5 自动化系统分区扩展

```powershell
Get-VM VM001, VM002 | Shutdown-VMGuest -Confirm:$false
```

```powershell
While ((Get-VM VM001).PowerState -eq "PoweredOn") {
  Sleep -Seconds 2
}
While ((Get-VM VM002).PowerState -eq "PoweredOn") {
  Sleep -Seconds 2
}
```

```powershell
Get-VM VM001 | Get-HardDisk -Name "Hard disk 1" | |
  Set-HardDisk -CapacityGB 60 |
  -HostCredential $HostCredential |
  -GuestCredential $guestCredential |
  -HelperVM (Get-VM VM002)
```

```powershell
Get-VM VM001, VM002 | Start-VM -Confirm:$false
```

坐好，放松，并享受这一切吧。这些操作真的酷酷！

> 注意：扩展分区仅支持 Windows。 (img/62596f5acc979040608a4e5111beb7d6_316_0.png)

## 修改其他硬件

...（此处由于原文重复且混乱，已按上述逻辑整合）...

## 使用精简置备优化存储使用率

通过转换虚拟磁盘可以回收未使用的空间。你可以通过 vMotion 或通过在位转换虚拟磁盘来实现这一点。

## 使用 vMotion 转换虚拟磁盘

通过存储 vMotion 将厚置备（thick）虚拟磁盘转换为精简置备（thin）虚拟磁盘（或反之），可以通过将磁盘移动到另一个数据存储来实现。由于 vMotion 会在目标卷上创建硬盘的新副本，因此它是通过 `Move-HardDisk` 命令行程序实现的，并使用 `-Datastore` 参数指定新的数据存储，使用 `-DiskType` 参数指定新的磁盘类型。以下代码使用 vMotion 将虚拟机 VM001 上的所有磁盘移动到数据存储 Datastore02，并在移动过程中将其转换为厚置备磁盘：

```
Get-VM VM001 | Get-HardDisk | Move-HardDisk \
  -Datastore Datastore02 -StorageFormat Thin
```

若要转换虚拟机上的单个硬盘，只需指定 `-Name` 参数即可。以下代码使用存储 vMotion 仅移动虚拟机 VM001 上的“Hard disk 2”，并将其即时转换为精简置备：
