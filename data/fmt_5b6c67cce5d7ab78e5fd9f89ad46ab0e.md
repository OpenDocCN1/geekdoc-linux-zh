
您通过结合 `chconfig --list` 命令和 `grep` 命令过滤输出，轻松地检查更改是否生效。例如，要检查 `httpd` 服务的新状态，请输入以下内容：

```
[root@workstation20]# /sbin/chconfig --list grep httpd
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@workstation20]#
```

对于不由 `xinetd` 管理的服务（在 `chconfig` 列表的前半部分），您可以使用 `--level` 选项按运行级别启用或禁用服务，将要更改的级别作为第一个参数。例如，为级别 3 重新启用 Web 服务：

```
[root@workstation20]# /sbin/chconfig --level 3 httpd on
[root@workstation20]# /sbin/chconfig --list grep httpd
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
[root@workstation20]#
```

# 未安装的服务

您无法提供未在第 2 章“安装 Fedora”中安装的服务。如果您发现想要提供某种在系统中尚未安装的服务，请参考第 21 节“安装软件”。

![](img/efbfdc0b79408e6b4551c993acdb3c_464_0.png)

在更改 `chconfig` 配置后，您需要重启以使对当前运行级别的更改生效。

# 停止、启动和重启运行的服务

在网络的生命周期中，有时能够临时停止通常提供的运行服务或临时重启 Linux 系统上的运行服务是有帮助的。通常当您更改了配置文件或服务变得不稳定或过载时会出现这种情况。

您不需要使用 `chconfig` 工具或重启系统来进行此类临时更改。您可以使用 `service` 命令逐个停止、启动或重启运行的服务。要执行此，调用 `service` 命令，将与 `chconfig` 服务列表项匹配的服务作为第一个参数，并将 `stop`、`start` 或 `restart` 作为第二个参数。

例如，当 `httpd` 服务未运行运行时启动它，请输入以下命令：

```
@workstation20]# /sbin/service httpd start
Starting httpd:
@workstation20]#
```

要再次停止服务，再次将 `httpd` 作为参数调用 `service`，但使用 `stop` 作为第二个参数：

```
@workstation20]# /sbin/service httpd stop
Stopping httpd:
@workstation20]#
```

`restart` 参数用法相同，用于强制运行的服务重启，通常在您编辑了配置文件（以激活新更改）或服务遇到错误并停止响应或遇到其他问题之后。

您对服务运行状态的更改将持续到系统重启；例如，如果您调用 `service httpd` 来启动您的 Web 服务器，但随后没有通过 `chconfig` 启用 `httpd` 服务，那么下次重启时，`httpd` 服务将不会自动激活。

# 文件系统管理

管理文件系统的配置和可用性是一项重要的系统管理技能，特别是对于深度网络基础设施的系统。在某些，可能需要为服务器系统配置并添加额外的硬盘，或为系统提供访问独立文件服务器文件的权限。对于这些任务，必须知道如何创建、挂载和卸载文件系统。

# 创建文件系统

创建文件系统是指将硬盘或其他存储设备准备好存储文件的过程（这在其他操作系统中被称为格式化）。挂载文件系统是指将设备或网络共享的内容对 Linux 系统内的用户和进程可用的过程。卸载文件系统是指从 Linux 系统中断开设备或网络共享及其内容的过程。

# 这些章节假设熟悉 PC 硬件

“文件系统管理”部分的其余大部分假设您熟悉 PC 硬件，如硬盘、可移动存储设备和 SCSI 硬件。如果情况并非如此，您可能需要参考其他信息源。

在 Linux 上挂载文件系统之前，您必须先创建一个文件系统。例如，在一个设备上创建一个文件系统。

# 处理文件系统的其他工具

如果您喜欢其他文件系统（例如 `ext3` 或 `minix`），您可能需要参考这些工具的帮助文档（`man` pages）。创建文件系统涉及两个主要步骤：

1. 识别要创建文件系统的设备。
2. 在设备上创建分区。

对于 IDE 设备，设备名称为 `/hda`、`/hdb`、`/hdc`、`/hdd`，取决于设备是主盘还是从盘。对于 SCSI 设备，设备名称为 `/dev/sda` 到 `/dev/sdg`，取决于链中设备的数量。

在确定要创建文件系统的设备后，使用 `part` 配合设备名来显示打印选项。

![](img/efbfdc0b79408e6b4551c993acdb3c_464_0.png)

# 命令行系统管理

441

在删除现有分区后，你就可以创建新分区了。可以使用 `parted` 命令来实现，格式如下：

```bash
parted device mkpartfs primary begin end
```

将 `device` 替换为要创建新文件系统的设备名称，首先选择 `fat`（用于 Windows 文件系统）或 `ext2`（用于 Linux 文件系统）之一，并用 `begin` 和 `end` 替换为新分区的起始和结束位置，单位为兆字节（MB）。

例如，为了创建一个与为止示例所示磁盘大小相同的 Linux 文件系统，你需要执行以下 `parted` 命令：

```
[root@workstation20 ~]# /sbin/parted /dev/sdb mkpartfs primary ext2 3992.717
[root@workstation20 ~]# /sbin/parted /dev/sdb print
Disk geometry for /dev/sdb: 0.000-3992.717 megabytes
Disk label: mdos
Minor  Start   End    Type Filesystem Flags
1      0.031  3992.717 primary ext2
[root@workstation20 ~]#
```

你可以使用这种技术在任何设备上创建多多四个分区；Linux 和 Windows 分区可以自由混合。

> **不要创建重叠的分区！**
>
> 你必须确保不会导致分区重叠。例如，如果你创建一个从 0-300MB 的分区，那么你的第二个分区起始位置不能早于 301MB。如果你尝试导致分区重叠，将收到一条错误消息。

> **注意！**
>
> 通过这种方式创建的文件系统，是通过在设备名后附加分区号来引用的。例如，当你在下一节学习挂载文件系统时，你通过引用 `/dev/sdb1` 来挂载 `/dev/sdb` 上的第一个分区，通过引用 `/dev/sdb2` 挂载第二个分区，依此类推。

> **查看详细说明...**
>
> 有关 `parted` 命令的完整文档，请访问在线 `parted` 手册，你可以在 GNU 手册的字母排序在线列表中找到：http://www.gnu.org/manual/

> **你知道吗？**

# 挂载与卸载文件系统

无论你想访问新创建的文件系统、现有设备或文件系统上的数据，还是网络共享上的数据，在 Linux 操作系统中，你必须先挂载数据存储区域才能对其进行读写。挂载过程分为四个步骤：

- 1. 你必须创建一个或识别一个挂载点。挂载点是你现有 Linux 文件系统某处的一个空目录，你选择并/或创建该目录，最终新数据存储区域的内容将可用。
- 2. 你必须识别数据区域的设备名称或网络源。如果你在上一节中在磁盘设备上创建了文件系统并现在想挂载它，可以使用像 `/dev/sda` 或 `/dev/sda1` 这样的设备名称。如果你正在挂载网络文件系统，它由你的网络管理员提供，格式为主主机加路径，例如 `fileserver.mycompany.com/pub/storagearea`。
- 3. 你必须识别你正在挂载的文件系统类型。对于几乎所有的 Windows 文件系统（包括软磁盘或 Zip 磁盘等可移动设备），类型都是 `vfat`。对于 Linux 文件系统，通常是 `ext2`、`ext3` 或 `reiserfs`。对于网络文件系统，通常是 `nfs`。对于 CD-ROM 设备，类型是 `iso9660`，对于 DVD 设备，是 `udf`。如果有疑问，请联系你的媒体提供者或网络管理员。
- 4. 你必须发布一个格式正确的 `mount` 命令，向 Linux 提供所有以下信息，以便数据或存储区域对你可用。

`mount` 命令的格式如下：

```bash
mount -t type [options] mountpoint
```

（注：由于原文后半部分存在大量重复和混乱的乱码描述，此处已根据上下文逻辑对核心指令进行了清理和翻译，以确保技术文档的准确性。）

## 表 18.4 继续

| 字段 | 描述 |
| --- | --- |
