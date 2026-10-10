
如果你更改了 `cupsd.conf` 中的任何设置，必须重载 CUPS 服务才能生效。作为 root 用户，输入 `service cups reload`。（`reload` 选项在不重启守护进程的情况下读取新配置。）

`cupsd.conf` 文件是 CUPS 的主配置文件。打印机仅允许本地主机（`127.0.0.1`）访问。若要向任何可以访问它的远程机器共享此打印机，可以在 `</Location>` 行之前添加 `Allow All`。

`printers.conf` 文件用于定义打印机本身。对于每个打印机，你可以设置它的名称、位置和描述。你还可以设置使用的驱动程序和它连接的端口。

以下是 `printers.conf` 中打印机定义的示例：

```
<Printer hp2100>

Info HP LaserJet 2100M

Location HP LaserJet 2100M in hall closet

DeviceURI hp:/var/par/HP_LaserJet_2100_Series?device=/dev/port0

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

`DeviceURI` 有多种方式来识别打印机的设备名称，反映打印机的连接位置。以下是 `printers.conf` 文件列出的一些示例：

```
DeviceURI parallel:/dev/lp1

DeviceURI serial:/dev/ttyUSB0?baud=38400+size=8+parity=none+flow=none

DeviceURI scsi:/dev/scsi/scld0/0

DeviceURI socket://hostname:port

DeviceURI tftp://hostname/path

DeviceURI ftp://hostname/path
```

## 第 17 章：设置打印服务器 749

```
DeviceURI http://hostname[:port]/path

DeviceURI ipp://hostname/path

DeviceURI smb://hostname/printer
```

前三个示例显示了本地打印机（并行、串行和 SCSI）的格式。其他示例用于远程主机。在每种情况下，`hostname` 可以主机名或 IP 地址。端口号或路径标识了每个打印机在主机上的位置。

> 提示：如果你发现由于 CUPS 不特定的打印机驱动无法打印，可以将打印机设置为接受原始模式（`raw mode`）作业。如果你是从已安装正确打印机驱动程序的 Windows 客户端打印，这种方法是有效的。若要在 CUPS 中允许原始打印，请在 Linux 中取消 `/etc/cups/mime.types` 文件中以下行的注释：

`application/octet-stream`

取消 `/etc/cups/mime.convs` 文件中以下行的注释：

`application/octet-stream`

此之后，你就可以作为原始数据将文件打印到打印机，而无需在打印命令中使用 `-raw` 选项。作为替代方案，你可以在第一次通过打印机配置窗口配置打印时，选择原始打印队列（Raw Print Queue）驱动。

## 使用打印命令

为了与旧的 UNIX 和 Linux 保持后兼容，CUPS 支持许多用于打印的旧命令。大多数使用 CUPS 的命令行打印都可以通过 `lpr` 命令完成。Linux 的文字处理应用程序（如 StarOffice、OpenOffice.org 和 AbiWord）均配置为使用此设施进行打印。

通过打印机配置窗口，你可以为每个打印机定义所需的过滤器，以便文本能够格式化正确。`lpr` 命令的选项可以添加过滤器来正确处理文本。管理打印文档的其他命令包括 `lpq`（查看打印队列内容）、`lrm`（从队列中删除打印作业）和 `lpc`（用于控制打印机）。

> 交叉引用：第 6 章提供了如何在几种不同格式格式化并打印的示例，包括 `troff` 和 `Tex`。

## 使用 lpr 打印

使用 `lpr` 命令，你可以将文档打印到本地和远程打印机。文档文件可以添加到 `lpr` 命令的末尾，或者通过管道（`|`）重定向到 `lpr` 命令。这里是一个简单的 `lpr` 命令示例：

```
$ lpr doc.ps
```

## 第四部分：Fedora RHEL 网络和服务器设置

当你仅用 `lpr` 指定文档文件时，输出将重定向到默认打印机。作为个人用户，你可以通过设置 `PRINTER` 变量的值更改默认打印机。通常，你会将 `PRINTER` 变量添加到其中一个启动文件，，例如 `~/.bashrc`。以下是添加到 `.bashrc` 文件中的行代码，用于将你的默认打印机设置为 `lp3`：

```
export PRINTER=lp3
```

要让新的 `PRINTER` 值立即生效，请源化 `.bashrc` 文件（输入 `$HOME/.bashrc`）。要覆盖默认打印机，请在 `lpr` 命令行上选择特定的打印机。以下示例使用 `-P` 选项来选择不同的打印机：`lpr` 命令具有多种选项，允许 `lpr` 解释和格式化多种不同类型的文档。这些包括 `-n num`，其中 *num* 被替换为要打印的副本数（从 1 到 100），以及 `-1`（这将导致以原始模式发送文档，假设该文档已经过格式化）。

## 使用 lpc 列出状态

CUPS 中的 `lpc` 命令功能有限。你可以使用 `lpc` 列出打印机的状态。这里是一个示例：

```
lpc status

hp:

    printer is on device 'parallel' speed -1

    queuing is enabled

    printing is disabled

    no entries

    daemon present

desket_5550:

    printer is on device 'usb' speed -1

    queuing is enabled

    printing is disabled

    no entries

    daemon present
```

此输出显示了两个激活的打印机。第一个 (`hp`) 连接到并行端口。第二个 (`desket_5550`) 是 USB 打印机（显示为 `usb`）。`hp` 打印机目前已禁用（离线），尽管队列已启用，人们可以继续向打印机发送作业。

## 使用 lprm 删除打印作业

用户可以使用 `lprm` 命令从队列中删除他们的打印作业。在命令行上单独使用 `lprm` 时，它会从默认打印机删除该用户的所有打印作业。要从特定打印机删除作业，请使用 `-P` 选项，如下：

```
lprm -P lp0
```

## 第 17 章：设置打印服务器 751

要删除当前用户的所有打印作业，请输入以下内容：

```
$ lprm
```

要从队列中删除单个打印作业，请在 `lprm` 命令行上指定该作业的作业号。找到作业号，输入 `lpq` 命令。该命令的输出可能如下：

```
$ lpq

printer is ready and printing

Rank Owner Job Files Total Size Time

active root 133 /home/jake/prl 467

2 root 197 /home/jake/mydoc 23948
```

输出显示队列中有两个待打印的作业。（在这种情况下，它们没有在打印，因为打印机已关闭。）在 Job 列下，你可以看到与每个文档关联的作业号。要删除第一个打印作业，请输入以下内容：

```
$ lprm 133
```
