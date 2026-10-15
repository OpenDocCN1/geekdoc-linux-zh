

## 检查驱动器分配

Linux 在启动时如果光驱通过正确的线缆连接到计算机主板，并且在 IDE 通道上被分配为主盘或从盘，则会识别 CD 和 DVD 驱动器。查看内核启动信息中的驱动器设备分配，例如以下内容：

```
sr: DVDROM 10X, ATAPI CD/DVD-ROM drive
```

如果您拥有 DVD 兼容驱动器，通常还应有一个名为 /dev/dvd 的符号链接以及 /media 下的条目指向您的驱动器设备，因为许多 DVD 客户端，如 xine 或 vlc，默认会查找 /dev/dvd。

第一个 CD-RW 驱动器被分配到设备 /dev/scd0（尽管在启动时可能仍被最初识别为 IDE 设备），后续驱动器分配到 /dev/scd1，以此类推。要初始化驱动器以供使用，应加载以下模块：

| Module | Size | Used by | Not tainted |
|---|---|---|---|
| sg | 30244 | 0 | (autoclean) |
| sr_mod | 15192 | 0 | (autoclean) |
| cdrom | 27872 | 0 | (autoclean) [sr_mod] |
| ide-scsi | 8128 | 0 |  |
| scsi_mod | 96572 | 2 | [sr_mod ide-scsi] |

查找有关设备的内核消息输出，例如：

```
Attached scsi CD-ROM sr0 at scsi0, channel 0, id 0, lun 0
sr0: scsi3-mmc drive: 0x/32x writer cd/rw xa/form2 cdda tray
Uniform CD-ROM driver Revision: 3.12
```

您的基于 ATAPI 的 CD-RW 驱动器随后将作为 SCSI 设备在仿真下工作，并且符号链接 /dev/cdrom 应指向 /dev/scd0。您也可以使用 cdrecord 命令（包含在 Ubuntu 的多媒体软件包中）来获取有关驱动器的 SCSI 设备信息以便在刻录操作期间后续使用，如下所示：

```
# cdrecord -scanbus
```

```
scsibus1:

1,0,0 0) 'HL-DT-ST' 'RW/DVD GCC-4120B' '2.01' Removable CD-ROM
1,1,0 1) *
1,2,0 2) *
1,3,0 3) *
1,4,0 4) *
1,5,0 5) *
1,6,0 6) *
1,7,0 7) *
```

相关信息——示例中的 1,0,0（SCSI 总线、设备 ID 和逻辑单元号，或 LUN）——然后可以在刻录操作中像这样使用：

```
# cdrecord -v speed=8 dev=1,0,0 -data file name.img
```

在此示例中，名为 file_name.img 的 CD-ROM 数据映像将以 8 的速度创建在 CD-R 或 CD-RW 介质上，并且在写入操作完成后新磁盘将被弹出。

> **NOTE**
> 
> Ubuntu 还包含 dvdrecord、dvd+rw-format 和 growisofs 命令，可与 DVD-R 和 DVD-RW 驱动器一起使用。

## 配置无线网络

无线网络过去对 Linux 来说配置起来很麻烦，需要很多复杂步骤才能连接到无线网络。然而，Ubuntu 包含一个名为 Network Manager 的出色实用程序，使连接和管理无线网络变得极其简单。得益于 Ubuntu Linux 内核中包含的多个无线芯片组驱动程序，现在可以轻松连接到 WEP 和 WPA 加密的无线网络。

当您登录到 Ubuntu 时，您应该会在顶部面板中看到 Network Manager 小程序出现（参见图 2.17）。这是处理和监控网络连接的小程序。

![](img/8f9e74e2b343ff525bebfb720a3d8441_77_0.png)

**FIGURE 2.17**  Network Manager 通知小程序，在此已连接到无线网络。

单击工具栏中的小程序图标以连接到无线网络。如果您的无线接入点广播其 SSID，它应该出现在无线网络列表下（类似于图 2.17）。只需单击所需网络，Network Manager 就会检测正在使用的加密类型（如果有）并要求您输入密码。输入后，Network Manager 将启动无线连接。密码随后存储在默认密钥环中，这是一个专属于您登录的安全区域。从现在开始，每当您登录到 Ubuntu 时，Network Manager 连接将自动启动。

如果由于某种原因您的无线网络未出现（您可能隐藏了 SSID），您必须使用“连接到其他无线网络”选项，这将显示图 2.18 所示的屏幕。

