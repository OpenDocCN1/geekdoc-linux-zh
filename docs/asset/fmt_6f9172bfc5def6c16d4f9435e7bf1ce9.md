
本附录描述了 Red Hat Linux/SPARC 与 Red Hat Linux/Intel 安装之间的差异。虽然它提供了这些差异的良好概述，但并未完整记录安装过程。对于这一点，您需要顺序阅读第 2、3 和 6 章。这些章节将引导您参考本文的相应部分。

此外，在 `http://www.redhat.com/support` 上有大量关于 `sun4c` 的信息。

# C.1 支持的硬件

Red Hat Linux/SPARC 支持基于机器架构的硬件。最新的支持硬件列表可以在 `http://www.redhat.com/` 查看。

# C.2 安装概述

在 SPARC 系统上安装 Red Hat Linux 比安装 Red Hat Linux/Intel 稍微复杂，主要是由于机器架构的差异。通常，成功安装的主要步骤为：

- 1. 确定您的 SPARC 系统支持哪些控制台命令。
- 2. 确定是否有足够的内存使用基于内存盘的安装。
- 3. 确定您将如何启动安装程序。
- 4. 确定您将使用何种安装方法。
- 5. 确定是否将从串口终端安装 Red Hat Linux/SPARC。
- 6. 加载并运行 Red Hat Linux 安装程序。

让我们详细查看这些每个步骤。

# C.3 控制台命令

SPARC 系统有两种不同类型的启动命令可用，取决于系统控制台 PROM 的版本。PROM 低于 2.0 的系统使用所谓的“旧”式启动命令，而 PROM 版本为 2.0 或更高版本的系统可以使用旧式或新式的启动命令。如果您的 SPARC 系统的控制台提示符为 `ok`，则说明您的系统处于新命令模式，可以使用新式启动命令。

# C 关于 Red Hat Linux/SPARC 的特定信息

以下列表目前不支持：

- `sun4e` 机器，内核尚未移植到该架构。

以下类型的 CD-ROM 不支持（有关 CD-ROM 兼容性的更多信息，请访问 `http://saturn.tlug.org/suncdfaq`）：

- 所有 NEC 型
- 部分 Toshiba XM-4101B
- Toshiba XM-3201B
- 旧版 SPARC PROM AppleCD 300 Plus
- Apple CD600i

## 关于 Red Hat Linux/SPARC 的特定信息

要进一步了解您的硬件配置。关于旧版 Sun 硬件的优秀参考资料（特别是旧式的启动命令），可以参考 James W. Bardsall 写的 *The Sun Hardware Reference*。该文件可以在 `ftp://ftp.picarey.com/pub/Sun-Hardware-Ref/parts/` 找到。文件 `part2` 包含了对旧版 Sun 系统中存在的“ROM 监控器”的详细描述。

通常情况下，新式的启动命令是 `boot`，后跟一个描述性的设备名称（例如 `floppy`、`cdrom` 或 `net`）。

旧式的启动命令是 `b`，后跟一个如下格式的设备指定符：

```
xx(a,b,c)
```

`xx` 用于指定设备类型（例如用于 SCSI 磁盘的 `sd`），`a` 是控制器编号，`b` 是设备的单元号，`c` 是分区号。如果您拥有旧版 SPARC 系统，并需要关于其启动命令语法的额外信息，请参阅 *The Sun Hardware Reference*。

## C.4 基于 ramdisk 的安装标准

当 Red Hat Linux/SPARC 安装开始时，通常会将一个 ramdisk 加载到内存中。该 ramdisk 包含安装所需的数据和程序，大小约为 4 MB。由于 ramdisk 内存独立 Red Hat Linux/SPARC 安装程序，您的 SPARC 系统必须至少拥有 12 MB 内存才能成功使用基于 ramdisk 的安装。对于内存少于 12 MB 的 SPARC 系统，还有另一种方法。它被称为 NFS 挂载根目录（NFS-mounted root）。顾名思，不是使用 ramdisk 来存放 Red Hat Linux/SPARC 安装程序的一部分，而是使用 NFS 服务器将必要文件导出到 SPARC 系统。虽然这种方法内存内存少，但设置起来较为复杂。

注意：也可以通过 Red Hat Linux/SPARC CD-ROM 启动来安装 Red Hat Linux/SPARC。这种方法既不用 ramdisk 也不用 NFS 挂载根，因为必要文件已经存在 Red Hat Linux/SPARC CD-ROM 上。我们将在第 202 页的 C.5.2 节讨论从 CD-ROM 启动。

## C.5 选择启动方法

### C.4.1 准备使用 NFS 挂载根

如果您将使用 NFS 挂载根运行安装程序，您需要为您的 SPARC 系统提供网络连接、一个能够导出 Red Hat Linux/SPARC CD-ROM（或等文件）的 NFS 服务器，以及能够响应 `rarp` 请求的能力，以便您的 SPARC 系统获取其 IP 地址。`rarp` 的必要命令为：

```
rarp -s ip.address.of:sparc hw:address:sparc
```

如您所料，请将 `ip.address.of:sparc` 替换为您的 SPARC 系统的 IP 地址，并将 `hw:address:sparc` 替换为您的 SPARC 系统网络适配器的 MAC 地址。IP 地址由网络管理员分配，MAC 地址在 SPARC 系统上电时显示在控制台上。

要在安装期间使用 NFS 挂载根，请在您的启动命令中添加以下参数：

```
linux fsroot=nfs.server.ip.address:/path/to/RH/image
```

单词 `linux` 应该始终包含在位于第一个参数之前的启动命令中。将 `nfs.server.ip.address` 替换为 NFS 服务器的 IP 地址，并将 `/path/to/RH/image` 替换为包含相应 Red Hat Linux/SPARC 文件的导出目录路径。

## C.5 选择启动方法

本节描述了如何启动（或引导）安装程序。一旦安装程序运行，您将能够从几种安装方法中进行选择。您可以从以下安装方法中：CD-ROM、NFS、硬盘和 FTP。（注意，如果直接从 CD-ROM 启动安装程序，安装将自动从 CD-ROM 进行。）

Red Hat Linux/SPARC 安装有三种不同的启动方式：

- 从磁盘软片启动 `Boot From Diskette` - 从磁盘片读取安装程序。
- 从 CD-ROM 启动 `Boot From CD-ROM` - 直接从 Red Hat Linux/SPARC CD-ROM 读取安装程序。
- 从网络启动 `Boot From the Network` - 从 TFTP 服务器读取安装程序。

### C.5.1 从磁盘片启动

如果您的 SPARC 系统有磁盘片驱动器，您可以从磁盘片启动 Red Hat Linux/SPARC 安装程序。启动磁盘片镜像（称为 `boot.img`）位于 Red Hat Linux/SPARC CD-ROM 的 `images/` 目录下。请参阅第 193 页的附录 B 了解将镜像写入磁盘片的说明。确保您使用的是名为“Boot Diskette”的磁盘片。

对于 PROM 版本为 2.0 或更高版本的 SPARC 系统，正确的启动命令（在新命令模式下）是：

```
boot floppy
```

另一方面，PROM 版本小于 2.0 的 SPARC 系统应在 `> ` 提示符下使用以下命令：

```
b fd()
```

注意：有报告显示某些带有非 2.0 PROM 的系统无法从磁盘片启动 Red Hat Linux/SPARC 安装程序。如果发现您的 SPARC 系统出现这种情况，您将需要使用另一种启动方法。

### C.5.2 从 CD-ROM 启动

如果您的 SPARC 系统有 CD-ROM 驱动器，您可以直接从 Red Hat Linux/SPARC CD-ROM 启动。对于 PROM 版本为 2.0 或更好的 SPARC 系统，在新命令模式下使用以下命令：

```
boot cdrom
```

PROM 版本小于 2.0 的 SPARC 系统应在 `> ` 提示符下使用以下命令：

```
b cdrom(0)
```

注意：如果您对本手册有任何问题，请发送邮件至 `docs@redhat.com`。

### C.5.3 从网络启动

虽然从网络启动 SPARC 系统相当简单，但有几个要求：

- 您的 SPARC 系统必须有网络连接。
- 您的网络必须通过 `rarp` 为您的 SPARC 系统分配 IP 地址。
- 您必须有一个 TFTP 服务器，可以将 Red Hat Linux/SPARC 内核和安装程序下载到您的 SPARC 系统。

网络启动有两种类型：

- 使用 NFS 挂载根的网络启动。内存少于 12 MB 的 SPARC 系统需要此方法。
- 使用网络加载 ramdisk 的网络启动。内存至少 12 MB 的系统可以使用此方法。

设置 RARP：如果您将使用 `rarp`，请参阅第 201 页的 C.4.1 节。
