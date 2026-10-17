
#### Suspending virtual machines

脚本可用于的实际场景之一是，当你关闭主机时希望挂起虚拟机而不是让它们关闭；在主机重新启动后需要再次启动整个客户机操作系统。以下是一个简单的脚本，它会挂起虚拟机然后重启机器：

```
#script to reboot the server
#first suspends the virtual machines and then reboots
vmware-cmd /data1/vmware/nw65/nw65.vmx suspend
vmware-cmd /data1/vmware/suse10/suse10.vmx suspend
vmware-cmd /data1/vmware/sles9/sles9.vmx suspend
#maybe do some other stuff;-)
reboot
```

此示例脚本演示了该实用程序的语法。`vmware-cmd`命令后面跟着配置文件路径和名称，并以要执行的操作结尾。

#### Preparing for a backup

在第 35.5 节中，我解释了备份正在运行虚拟机的 VMware GSX Server 主机是个坏主意。此外，我建议停止虚拟机，并在备份后重新启动它们。以下脚本扩展了我为重启主机而创建的脚本。在此脚本中，我不会手动列出虚拟机，而是使用`vmware-cmd -l`命令列出所有已列出的虚拟机：

```
for vm in $(vmware-cmd -l); do
  vmware-cmd $vm suspend
done
```

如果你运行此脚本并且虚拟机已处于挂起状态或电源关闭状态，实用程序将生成错误消息，说明机器处于错误状态。因此，如果你有空闲时间和脚本技能，你可以使用`vmware-cmd getstate`命令检查虚拟机状态来扩展它。

#### Command reference

在本节末尾，我想为你提供`vmware-cmd`实用程序可用的完整选项集。要处理虚拟机操作，请使用以下语法：

```
vmware-cmd <options> <vm-cfg-path> <vm-action> <arguments>
```

要处理基于服务器的操作，请在命令中添加`-s`参数。

```
vmware-cmd -s <options> <server-action> <arguments>
```

表 37.1：`vmware-cmd`命令的选项。

| 选项 | 描述 |
|---|---|
| `-H <host>` | 指定替代主机（如果设置，则必须同时设置 -U 和 -P） |
| `-O <port>` | 指定替代端口 |
| `-U <username>` | 指定用户 |
| `-P <password>` | 指定密码 |
| `-h` | 更详细的帮助 |
| `-q` | 安静 - 最小输出 |
| `-v` | 详细 |

表 37.2：`vmware-cmd`实用程序的服务器操作。

| 选项 | 描述 |
|---|---|
| `-l` | 列出已注册的 VM |
| `-s register <config file path>` | 注册 VM |
| `-s unregister <config file path>` | 注销 VM |
| `-s getresource <variable>` | 检索服务器资源 |
| `-s setresource <variable> <value>` | 设置服务器资源 |

#### 表 36.3：`vmware-cmd`实用程序的工作站操作。

| 选项* | 描述 |
|---|---|
| Getconnectedusers | 列出连接到 VM 的用户及其 IP 地址 |
| getstate | 获取 VM 的执行状态 |
| start <powerop_mode> | 启动或恢复 VM |
| stop <powerop_mode> | 停止 VM |
| reset <powerop_mode> | 重置 VM |
| suspend <powerop_mode> | 挂起 VM |
| setconfig <variable> <value> | 设置配置变量 |
| getconfig <variable> | 检索配置变量的值 |
| setguestinfo <variable> <value> | 设置来宾信息变量 |
| getguestinfo <variable> | 检索来宾信息变量的值 |
| getid | 检索 VM ID |
| getpid | 检索正在运行的 VM 的进程 ID |
| getproductinfo <prodinfo> | 获取各种产品信息 |
| connectdevice <device_name> | 将虚拟设备连接到 VM |
| disconnectdevice <device_name> | 从 VM 断开虚拟设备连接 |
| getconfigfile | 检索配置文件路径 |
| getheartbeat | 检索来宾操作系统的心跳值 |
| getuptime | 检索来宾操作系统的运行时间 |
| getremoteconnections | 检索到 VM 的远程连接数 |
| gettoolslastactive | 检索自工具上次通知以来的秒数 |
| getresource <variable> | 检索 VM 资源 |
| setresource <variable> <value> | 设置 VM 资源 |
| setrunasuser <username> <password> | 设置 VM 以其运行的用户 |
| getrunasuser | 检索 VM 以其运行的用户 |
| getcapabilities | 检索当前用户对 VM 的访问权限 |
| addredo <disk_device_name> | 向虚拟磁盘添加重做日志 |
| commit <disk_device_name> <level> <freeze> <wait> | 提交虚拟磁盘的重做日志 |
| answer | 回答请求输入的 VM 的问题 |

*工作站选项必须始终包含虚拟机配置文件的完整路径。

## 第 6 部分

### VMware 简介

ESX Server 和 VirtualCenter

![](img/25fe75b93b97a021effaba85db112a52_312_0.png)

> 猜猜看：你通过把它们全部放在一个机架上来“整合服务器”，但你把冷却单元拆出来了，因为你需要多一点空间。

> 所以我想 ESX 并不是指极端堆叠盒子？

## 38 VMware ESX Server 简介

如果你使用过 VMware Workstation 或 VMware GSX Server，那么你就了解虚拟机的概念。你知道多个虚拟机可以在一台硬件主机上运行并共享内存、CPU 和硬盘等资源。对于 VMware ESX Server 来说也是如此，但比较也到此为止：它是一台运行虚拟机的硬件主机。你创建它们的方式看起来相同，但存在重要差异。此外，VMware ESX Server 的配置和管理与 VMware Workstation 完全不同，而且比 VMware GSX Server 更先进。

本章作为 VMware ESX Server 的介绍。如果你已经使用过该产品，这里应该没有新内容。我假设你熟悉 VMware 的托管产品，如 Workstation 或 GSX Server，因此我将从这些产品与 VMware ESX Server 之间的相似性和差异概述开始。之后，我将详细介绍运行服务器所需的硬件和软件以及如何执行简单安装。

### 托管与原生操作系统

最大的区别在于 VMware ESX Server 不是所谓的“托管产品”。你不会在用于服务器的硬件主机上安装 Windows 或 Linux。相反，安装程序会安装一个由 VMware 修改的 Linux 版本，专门用于运行虚拟机。你可以登录 Linux 环境以执行维护或配置任务，但 VMware 的本意并不是让你在 ESX Server 上安装自己的额外 Linux 软件。运行专用的 Linux 版本似乎会给你的环境带来限制，因为你无法安装可能有用的驱动程序或软件。但从积极的一面来看，这正是 VMware ESX Server 如此强大的原因。所有受支持硬件的驱动程序都包含在内，并且使用 VMware 批准的驱动程序和软件，你可以为虚拟机获得一个超稳定的运行环境。

### 固定大小的虚拟磁盘

创建虚拟机看起来与 VMware Workstation 或 VMware GSX Server 相同，如果你第一次看到的话，但存在一些显著差异。首先，你必须在创建虚拟机时分配所有所需的磁盘空间。没有动态增长的虚拟磁盘之说。这些虚拟磁盘文件存储在专用的 VMFS 文件系统上，该文件系统针对这些大文件进行了优化。此外，你虚拟机中的虚拟磁盘始终使用 SCSI 磁盘，并且也需要存储在物理 SCSI 磁盘上。这是因为它是 VMFS 文件系统支持的唯一磁盘类型。

### 仅远程管理
