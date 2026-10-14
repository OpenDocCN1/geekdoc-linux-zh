

## 21.

现在你需要重新编译内核以使这些更改生效。为此，依次输入以下命令：

```
#make dep
#make clean
#make bzImage
#make modules
#make modules_install
```

## 22.

执行这些命令中的每一个都需要一些时间，并且会有大量文本滚动而过——不用担心，这是正常的。当所有命令都执行完毕后，重新启动系统。

重新启动系统以使更改生效。你可以通过输入以下第一个命令（适用于 Plus 版本）或下一个命令（适用于旧版本）来测试你的 Zip 驱动器：

```
#modprobe imm
#modprobe ppa
```

在执行此操作之前，请确保你的驱动器已连接到并行端口，已打开电源，并且其中已放入磁盘。如果命令成功，你的 Zip 驱动器的活动灯应短暂亮起。如果你查看 /var/log/messages 文件的末尾，你应该会看到类似以下内容（适用于 imm 模块）：

```
scsi1 : Iomega VP12 (imm) interface
scsi : 2 hosts.
Vendor: IOMEGA   Model: ZIP 100          Rev: J.67
Type:   Direct-Access                     ANSI SCSI revision: 02
```

你的 Zip 驱动器被分配为 SCSI 设备 /dev/sda4。你可以通过输入以下命令将其挂载：

```
# mount /dev/sda4 /mnt/ -t vfat
```

请注意你将其挂载为 /dev/sda4，这是因为磁盘默认就是这样分区。你可以通过以下方式运行 fdisk 命令来更改此行为：

```
#fdisk /dev/sda
```

只需按你想要的任何方式对其进行分区即可。你现在可以在 /mnt 上挂载所有常见的文件和目录命令。Zip 驱动器在驱动器挂载时锁定弹出按钮。要解锁它，请按如下方式卸载驱动器：

```
#umount /mnt
```

这将解锁弹出按钮。

## ATAPI/IDE Zip Drives

这种型号的 Zip 驱动器是内部的；它适合你的 3.5 或 5.25 英寸驱动器槽，并通过电缆连接到 IDE 控制器。这些型号比并行端口快得多。这些驱动器的两种型号是旧的基于 IDE 的型号和更新的基于 ATAPI EIDE 的型号。每种型号的配置方式略有不同。

旧的 IDE 型号只需要你在内核中内置 IDE 支持。Linux 然后会像对待普通硬盘一样对待此驱动器，无需额外配置。ATAPI EIDE 驱动器要求你的内核中支持 ATAPI 软盘驱动器。要配置其中任何一种驱动器，只需按照以下步骤操作：

- 1. 以 root 身份登录。
- 2. 将目录更改为 Linux 内核源代码目录：
  `#cd /usr/src/linux`
- 3. 通过输入以下命令启动内核的配置模块：
  `#make menuconfig`
- 4. 内核配置模块将启动；导航到 Block Devices 并按 Enter。
- 5. 突出显示 Include IDE/ATA-2 DISK Support 并按 Y 将其包含在内核中。
  这是针对基于 IDE 的型号，而不是 ATAPI。如果你有 IDE 硬盘，你可能已经设置了此项。
- 6. 突出显示 Include IDE/ATAPI FLOPPY Support 并按 Y 将其包含在内核中。
  这是针对基于 ATAPI 的 Zip 驱动器。
- 7. 按两次 Esc 退出此模块。
- 8. 再按两次 Esc 退出内核配置模块。它会询问你是否要保存新的内核配置；选择 Yes。
- 9. 现在你需要重新编译内核以使这些更改生效。为此，依次输入以下命令：
  `#make dep`
  `#make clean`
  `#make bzImage`
  `#make modules`
  `#make modules_install`
- 10. 执行这些命令中的每一个都需要一些时间，并且会有大量文本滚动而过——不用担心，这是正常的。当所有命令都执行完毕后，重新启动系统。

重新启动系统以使更改生效。请密切注意内核启动时显示的消息。你应该能看到你的 Zip 驱动器作为 IDE 设备被初始化。它将被分配一个形式为 /dev/hd? 的设备文件。

## SCSI Zip and Jaz Drives

这些型号是内部的（Zip 和 Jaz）和外部的（Jaz），适合你的 3.5 或 5.25 英寸驱动器槽。它们通过电缆连接到 SCSI 控制器。Linux 会像对待普通硬盘一样对待这些驱动器。你必须配置内核以支持 SCSI 磁盘和你的驱动器所连接的 SCSI 控制器。为此，只需按照以下步骤操作：

- 1. 以 root 身份登录。
- 2. 将目录更改为 Linux 内核源代码目录：
  `#cd /usr/src/linux`
- 3. 通过输入以下命令启动内核的配置模块：
  `#make menuconfig`
- 4. 内核配置模块将启动；导航到 SCSI Support 并按 Enter。
- 5. 突出显示 SCSI Support 并按 Y 将其包含在你的内核中。
- 6. 突出显示 SCSI Disk Support 并按 Y 将其包含在你的内核中。
- 7. 导航到 SCSI Low-Level Drivers 并按 Enter。
- 8. 在列表中，找到你系统中的 SCSI 控制器类型并按 Y 将其包含在你的内核中。如果你有 Zip Zoom，请选择 AHA152x 驱动程序。
- 9. 按两次 Esc 退出 SCSI Low-Level Drivers 菜单。
- 10. 按两次 Esc 退出 SCSI Support 菜单。
- 11. 按两次 Esc 退出内核配置模块。它会询问你是否要保存新的内核配置；选择 Yes。
- 12. 现在你需要重新编译内核以使这些更改生效。为此，依次输入以下命令：
  `#make dep`
  `#make clean`
  `#make bzImage`
  `#make modules`
  `#make modules_install`
- 13. 执行这些命令中的每一个都需要一些时间，并且会有大量文本滚动而过——不用担心，这是正常的。当所有命令都执行完毕后，重新启动系统。

重新启动系统以使更改生效。请密切注意内核启动时显示的消息。你应该能看到你的 Zip/Jaz 驱动器作为 SCSI 设备被初始化。它将被分配一个形式为 /dev/sd? 的设备文件。请注意，你应该阅读位于 /usr/doc/howto 下的 SCSI How-to 文件中有关你的 SCSI 适配器的文档。它将包含特定于你的适配器的额外信息。

## Crash Course in Zip/Jaz Tools

Linux 附带了一套可用于控制你的 Zip 和 Jaz 驱动器的实用程序。这些实用程序使你能够通过软件对磁盘进行写保护和取消写保护。

## Package requirements:

## Series ap:

ziptool

此软件包安装了两个命令行程序，ziptool 和 jaztool。两个命令的格式完全相同：

```
usage: ziptool -e <dev> eject disk
ziptool -s <dev> report protection status
ziptool -ro <dev> make disk read only
ziptool -rp <dev> make disk read only with password
ziptool -rw <dev> make disk full accessible
```

让我们看一些示例。要通过软件弹出磁盘，请输入以下内容：

```
#ziptool -e /dev/sda
```

要使磁盘只读，请输入以下内容：

```
#ziptool -ro /dev/sda
```

要使用密码使磁盘只读，请输入以下命令：

```
#ziptool -rp /dev/sda
```

程序会提示你输入用于写保护磁盘的密码。小心！如果你忘记了它，唯一能写入磁盘的方法就是格式化它。

要报告磁盘的保护状态，请输入以下内容：

```
#ziptool -s /dev/sda
```

最后，要移除写保护，请输入此命令：
```
#ziptool -rw /dev/sda
```
如果磁盘受密码保护，你将被提示输入密码。
所有这些命令都可以用 Jaz 驱动器使用，只需将 ziptool 替换为 jaztool 即可。

## Joysticks and Gamepads

尽管 Linux 不像其他平台那样拥有大量游戏，但对游戏杆的支持并未被忽视。Linux 支持大多数常用的游戏杆和游戏手柄。不过你必须重新编译内核才能使用它们。

要在 Linux 下配置你的游戏杆/游戏手柄，只需按照以下步骤操作。（请注意，如果你的游戏杆连接到你的声卡，这是通常的情况，你应该先让声卡正常工作。有关此主题的更多帮助，请参阅第 10 章“Sound Card Configuration”。）现在从以下步骤开始：

