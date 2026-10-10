

如果您修改了 `cupsd.conf` 文件中的任何设置，必须重新加载 CUPS 服务才能使更改生效。作为 root 用户，输入 `service cups reload`。（`reload` 选项会读取新的配置，而无需重启守护进程。）

## 配置 CUPS 打印机选项

当从打印机配置窗口创建新打印机时，该打印机将定义在 `/etc/cups/printers.conf` 文件中。以下是 `printers.conf` 中打印机定义的一个示例：

```
<DefaultPrinter hp2100>  
    Info HP LaserJet 2100M  
    Location HP LaserJet 2100M in hall closet  
    DeviceURI hp:/par/HP_LaserJet_2100_Series?device=ide0/devparport0  
    State Idle  
    Accepting Yes  
    Shared Yes  
    JobSheets none none  
    QuotaPeriod 0  
    PageLimit 0  
    KLimit 0  
    OpPolicy default  
    ErrorPolicy stop-printer  
  </Printer>
```

这是一个本地打印机的示例，它作为本地系统的默认打印机。最有趣的信息与 `DeviceURI` 有关，它显示打印机连接在并行端口 `/dev/parport0` 上。`State` 为 `Idle`（准备接受打印作业），而 `Accepting` 值为 `Yes`（打印机默认接受打印作业）。

`DeviceURI` 有几种方式来标识打印机的设备名称，反映了打印机的连接位置。以下是列在 `printers.conf` 文件中的几个示例：

```
DeviceURI parallel:/dev/plp
DeviceURI serial:/dev/tty1?baud=38400&size=8&parity=none&flow=soft
DeviceURI scsi:/dev/scsi/sclc0
DeviceURI socket://hostname:port
DeviceURI http://hostname/path
DeviceURI http://hostname/path
DeviceURI http://hostname:port)/path
DeviceURI ipp://hostname/path
DeviceURI smb://hostname/printer
```

前三个示例展示了本地打印机的形式（`parallel`、`serial` 和 `scsi`）。其他示例用于远程主机。在每种情况下，`hostname` 可以是主机名或 IP 地址。端口号或路径标识每台主机上每个打印机的位置。

> **提示：** 如果您发现由于某个特定打印机驱动程序不受 CUPS 支持而无法打印，您可以设置打印机以接受原始模式（raw mode）下的作业。

如果您从安装了正确打印驱动程序的 Windows 客户端进行打印，这可能效果很好。要在 CUPS 中允许原始打印，请取消注释 Linux 中 /etc/cups/mime.types 文件中的以下行：

```
application/octet-stream
```

并取消注释 /etc/cups/mime.convs 文件中的以下行：

```
application/octet-stream
```

之后，您可以将文件作为原始数据打印到您的打印机中，而无需在打印命令中使用 `raw` 选项。作为替代方案，您也可以在通过打印机配置窗口首次配置打印时选择 Raw Print Queue 驱动程序。

## 使用打印命令

为了保持与旧版 UNIX 和 Linux 打印功能向后兼容，CUPS 支持许多用于处理打印的旧命令。使用 CUPS 的大多数命令行打印都可以通过 lpr 命令完成。Linux 的 word processing 应用程序，例如 StarOffice、OpenOffice.org 和 AbiWord，都设置为使用此功能进行打印。

通过打印机配置窗口，您可以为每个打印机定义所需的过滤器，以便正确格式化文本。lpr 命令的选项可以添加过滤器以正确处理文本。用于管理打印文档的其他命令包括 lpq（用于查看打印队列内容）、lpnm（用于从队列中移除打印作业）和 lpc（用于控制打印机）。

> 交叉引用 第 6 章提供了如何格式化并以几种不同格式打印文档的示例，包括 troff 和 TeX。

### 使用 lpr 进行打印

使用 lpr 命令，您可以将文档打印到本地和远程打印机。文档文件可以添加到 lpr 命令行的末尾，或者通过管道（|）传递给 lpr 命令。以下是一个简单的 lpr 命令示例：

```
$ lpr doc1.ps
```

当您仅使用 lpr 指定文档文件时，输出将发送到默认打印机。作为个人用户，您可以通过设置 PRINTER 变量的值来更改默认打印机。通常，您会将 PRINTER 变量添加到您的启动文件之一，例如 $HOME/.bashrc。以下是添加到您的 .bashrc 文件中的一行，将您的默认打印机设置为 lp3：

```
export PRINTER=lp3
```

要使新的 **PRINTER** 值立即生效，请 source .bashrc 文件（输入 source $HOME/.bashrc）。要覆盖默认打印机，请在 `lpr` 命令行上指定特定打印机。以下示例使用 -P 选项选择另一个打印机：

```
$ lpr -P canyons doc1.ps
```

`lpr` 命令有多种选项，使 `lpr` 能够解释和格式化几种不同类型的文档。这些选项包括 -# num（其中 num 替换为要打印的份数，从 1 到 100）和 -1（这会导致文档以原始模式发送，假定文档已经过格式化）。

## 使用 `lpc` 列出状态

CUPS 中的 `lpc` 命令功能有限。您可以使用 `lpc` 列出打印机的状态。以下是一个示例：

```
$ lpc status
hp:
  printer is on device 'parallel'  speed -1
  queuing is enabled
  printing is disabled
  no entries
  daemon present
deskjet_5550:
  printer is on device 'usb'  speed -1
  queuing is enabled
  printing is disabled
  no entries
  daemon present
```

此输出显示了两个打印机。第一个（hp）连接到并行端口。第二个（deskjet_5550）是 USB 打印机（显示为 usb）。HP 打印机当前处于禁用状态（离线），尽管队列已启用，人们仍可继续向打印机发送作业。

## 使用 `lprm` 删除打印作业

用户可以使用 `lprm` 命令从队列中删除自己的打印作业。单独在命令行上使用 `lprm` 时，它会从默认打印机中删除用户的所有打印作业。要从特定打印机中删除作业，请使用 -P 选项，如下所示：

```
$ lprm -P lp0
```

要删除当前用户的所有打印作业，请输入以下内容：

```
$ lprm -
```

要从队列中删除单个打印作业，请在 `lprm` 命令行上指明该打印作业的编号。要查找作业编号，请输入 `lpq` 命令。以下是该命令输出的可能样子：

```
$ lpq

printer is ready and printing

Rank  Owner    Job Files                Total Size Time
active root      133 /home/jake/prl       467
2    root      197 /home/jake/mydoc     23948
```

输出显示有两个等待在队列中的可打印作业。在 Job 列下，您可以看到与每个文档关联的作业编号。要删除第一个打印作业，请输入以下内容：

```
# lprm 133
```

## 配置打印服务器

您已配置好打印机，以便您和计算机上的其他用户可以向其打印。现在，您希望将该打印机与家庭、学校或办公室中的其他人共享。基本上，这意味着将您的计算机配置为打印服务器。

在您的 Linux 系统上配置的打印机可以以不同的方式与网络上的其他计算机共享。您的计算机不仅可以作为 Linux 打印服务器使用，还可以像 SMB 打印服务器一样向客户端计算机呈现。换句话说，Windows 客户端只会看到您的打印机就像来自另一台 Windows 机器的打印机。

在本地打印机连接到您的 Linux 系统且您的计算机连接到您的本地网络后，您可以使用本节的程序通过 Linux (UNIX) 或 SMB 接口与其他客户端计算机共享该打印机。

### 配置共享的 CUPS 打印机

在将本地打印机添加到您的 Linux 计算机后，使其可供网络上其他计算机使用相当简单。如果在共享打印机的计算机之间存在 TCP/IP 网络连接，您可以简单地授予来自远程主机的个别主机或用户访问您的计算机打印服务的权限。设置本地打印机的程序在本章前面部分已讨论。

要将本地打印机作为打印服务器与其他计算机共享，请执行以下操作：

- 1. 从桌面面板选择 系统 > 管理 > 打印。将出现打印机配置窗口。
- 2. 右键单击您要共享的打印机的图标。（如果打印机尚未配置，请参见本章前面部分的“设置打印机”章节。）
- 3. 选择菜单中的共享复选框，使复选框中出现对勾。

