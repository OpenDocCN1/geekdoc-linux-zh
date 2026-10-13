
| switchto | vmx 文件的别名或路径 | 切换到指定的虚拟机。 |
|---|---|---|
| listvms |  | 列出虚拟机 |
| query |  | 检查虚拟机的状态。 |
| exit |  | 停止所有使用 vmware-fullscreen 命令启动的虚拟机。 |

- 在配置文件中添加以下参数（在线文档中已解释）：FullScreenSwitch.cycleKey、FullScreenSwitch.hostDirectKey 和 FullScreenSwitch.cycleHost。

vmware-fullscreen 实用程序的日志文件信息会写入运行该应用程序的用户临时目录中的日志文件。默认情况下，这将是：c:\documents and settings\<username>\local settings\temp。

可以通过在通用 VMware Workstation 配置文件（C:\Documents and Settings\All Users\Application Data\VMware\VMware Workstation\config.ini.）中添加以下条目来更改路径：

```
fullScreenSwitch.log.filename="<path>"
```

## 6.3 VMware 文件参考

虚拟机由一组文件组成。配置、BIOS 和虚拟硬盘的内容都进入主机 PC 文件系统上的文件。表 6.4 概述了用于虚拟机和一般 VMware 目的的文件。这些文件列表并不完整，因为并非所有文件都有文档记录。该概述是通过分析 VMware Workstation 及其创建的文件得出的。

表 6.4：虚拟机文件参考。

| 文件或文件类型 | 描述 |
|---|---|
| .vmx | 一个包含虚拟机配置的文本文件。参数通过 VMware 应用程序配置。如果需要，可以通过文本编辑器修改参数。手动编辑前请关闭 VMware 应用程序。VMware Workstation 会验证此文件是否存在缺失引号、重复条目等。 |
| .vmxf | 这是存储虚拟机作为团队成员时团队特定信息的附加配置文件。 |
| .vmtm | 虚拟机团队的配置文件。 |
| .vmdk | 所有虚拟磁盘文件的扩展名。 |
| diskname-###.vmdk | 创建快照后，所有对原始磁盘文件的更改都存储在此 REDO 文件中。 |
| <vmxconfig name>.nvram 或只是 .nvram | 包含 BIOS 的非易失性随机存取存储器文件。 |
| .vmsd | 此文件包含有关快照的元数据。 |
| .vmsn | 这是实际的快照文件，其中存储虚拟机的运行状态。 |
| .vmss | 虚拟机挂起状态文件。它包含挂起虚拟机时的内存转储。 |
| .vmem | 虚拟机的内存交换文件。 |
| .lck | 为配置和磁盘文件创建的锁定文件。 |
| .log | 虚拟机所有活动的日志文件。可以通过在 .vmx 配置文件中添加 logging = FALSE 来关闭日志记录。日志文件的名称和位置可以用此参数修改：log.filename = "c:\patch\name.log"。注意：没有日志记录，VMware 将很难分析您可能遇到的任何问题。 |
| vmware-core | 在某种致命错误情况下创建的转储文件。 |
| C:\Documents and Settings\All Users\Application Data\VMware\VMware Workstation |  |
| config.ini | 通用配置文件。 |
| C:\Documents and Settings\All Users\Application Data\VMware |  |
| vmnetdhcp.conf | VMware 主机专用 DHCP 服务器配置文件。 |
| vmnetdhcp.leases | 包含 DHCP 分配的 IP 地址的文件。 |
| vmnetnat.conf | VMware NAT 服务配置文件。 |

## 6.4 VMware 产品世代

如果您使用 VMware 产品已有几年，您可能知道虚拟机并不总是能在虚拟机产品之间或同一产品的不同版本之间兼容。在本节中，我将讨论如何处理不同产品世代以及如何确定虚拟机属于哪个世代。

注意：本节中的信息摘自官方 VMware 虚拟机迁移规划指南，可在以下网址获取：www.vmware.com/pdf/mobility_guide.pdf。

表 6.5 列出了四个当前的 VMware 产品世代。在大多数情况下，在同一世代的 VMware 产品之间转换虚拟机很简单。在某些特殊情况下，例如从 VMware Workstation 迁移到 VMware ESX Server，需要执行一些额外步骤。

表 6.5：VMware 产品及其世代。

| 世代级别 | 属于此世代的产品 |
|---|---|
| 第 2 代 | GSX Server 1, ESX Server 1.0 and 1.1 |
| 第 3 代 | Workstation 3, GSX Server 2, ESX Server 1.5 |
| 第 4 代 | Workstation 4, GSX Server 3, ESX Server 2 |
| 第 5 代 | Workstation 5 |

提示：当产品不属于同一世代时，您当然可以遵循官方指南并升级虚拟机。但是，有时使用本书第 3 部分所述的物理到虚拟转换方法来执行虚拟到虚拟迁移会更容易。

如果您不确定虚拟机的世代，想对其进行一些研究，以下提示很有用：

```
config.version = "2"    VMware Workstation 2
config.version = "6"    VMware Workstation version 3 / GSX Server 2.x
config.version = "7"    VMware Workstation version 4/ GSX Server 3.x
config.version = "8"    VMware Workstation version 5 and 5.5.
```

还有一个标识符用于硬件世代。以下是多年来我在虚拟机中发现的内容列表：

```
virtualHW.version = "2"      VMware Workstation 3 / GSX Server 2.x
virtualHW.version = "3"      VMware Workstation 4 / GSX Server 3.x
virtualHW.version = "4"      VMware Workstation 5 and 5.5
```

VMware Workstation 版本 2 虚拟机可以通过其虚拟磁盘的 .dsk 扩展名轻松识别。.vmdk 扩展名是在 VMware Workstation 版本 3 中引入的。

如果您只有虚拟硬盘的副本（.VMDK），并且不知道它属于哪个硬件世代，则可以搜索文件中的适当字符串。硬件标识存储在虚拟硬盘集的第一个 .VMDK 文件中。

使用 Windows 的 find 命令或 Linux 的 grep 命令在文件中查找虚拟磁盘世代标识符：

Windows

```
find "virtualHWVersion" <path to .vmdk file>
```

Linux

```
grep 'virtualHWVersion' <path to .vmdk file>
```

这将导致一个字符串，例如以下显示版本 4，属于 VMware Workstation 5 的字符串：

```
ddb.virtualHWVersion = "4"
```

注意：对于较旧版本的 VMware Workstation，我没有在配置文件中找到此字符串。它存在于 VMware Workstation 4 和 5 中。因此，由于版本 2 使用 .DSK 文件，未找到此字符串的剩余 .VMDK 文件可能来自 Workstation 版本 3 或 GSX Server 2。

## 6.5 VMware Windows 服务概述

VMware Workstation 在您的 Windows 中添加了三个服务。如果您安装 VMware DiskMount 实用程序，将添加第四个服务。下图显示了“管理工具”中的“服务”应用程序中的服务概述。

![](img/25fe75b93b97a021effaba85db112a52_101_0.png)

DHCP 和 NAT 服务负责主机 PC 上相应的 VMware 功能。它们在第 11 章“网络配置”中进行了说明。虚拟挂载服务属于 VMware DiskMount 实用程序，讨论见第 7.4 节“使用 DiskMount 实用程序”。

### VMware 授权服务

此服务需要澄清。授权服务负责在启动应用程序的用户不是管理员用户时运行 VMware。此服务检测到用户不是管理员用户并以本地系统帐户启动 VMware。图 6.2 显示了 Sysinternals Process Explorer 的屏幕截图

![](img/25fe75b93b97a021effaba85db112a52_102_0.png)

图 6.2：Sysinternals Process Explorer。

vmware-vmx.exe 作为服务下的 vmware-authd.exe 的子进程启动。可以通过在通用 VMware 配置文件中启用日志记录来跟踪服务的运行。此文件名为 config.ini，位于 C:\Documents and Settings\All Users\Application Data\VMware\VMware Workstation。要启用日志记录，请将以下行添加到此文本文件中：

