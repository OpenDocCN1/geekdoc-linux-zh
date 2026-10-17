
在 Samba 近期开发阶段出现的一个问题是支持数百台打印机的驱动下载需求。对于这项任务，使用 Windows NT APW（添加打印机向导）有点笨拙（至少可以这么说）。如果你不想仅通过疯狂点击打印机安装就患上 RSS（重复性劳损）疼痛，你需要考虑一个非交互式脚本。如果多台打印机使用相同的驱动程序，则可以使用 `rpclient setdriver` 命令来设置与已安装队列关联的驱动程序。如果驱动程序已上传到 `/print/$` 并注册到打印 TDB 中，它可以被多个打印队列使用。在这种情况下，你只需要对每个队列重复 `rpclient` 的 `setprinter` 子命令（无需反复执行 `adddriver`）。以下是如何实现此操作的示例：

```bash
root# rpclient SAMBA-CUPS -U root%secret -c 'enumdrivers'
cmd = enumdrivers

[Windows NT x86]
Printer Driver Info 1:
  Driver Name: [infotec   IS 2075 PCL 6]

Printer Driver Info 1:
  Driver Name: [DANKA InfoStream]

Printer Driver Info 1:
  Driver Name: [Heidelberg Digimaster 9110 (PS)]

Printer Driver Info 1:
  Driver Name: [dm9110]

Printer Driver Info 1:
  Driver Name: [mydrivername]

[....]
```

```bash
root# rpclient SAMBA-CUPS -U root%secret -c 'enumprinters'
cmd = enumprinters
  flags: [0x800000]
  name: [\\SAMBA-CUPS\\dm9110]
  description: [\\SAMBA-CUPS\\dm9110,,110ppm HiVolume DANKA Stuttgart]
  comment: [110 ppm HiVolume DANKA Stuttgart]
[....]
```

```bash
root# rpclient SAMBA-CUPS -U root%secret -c 'setdriver dm9110 "Heidelberg Digimaster 9110 (PS)"'
cmd = setdriver dm9110 Heidelberg Digimaster 9110 (PPD)
Successfully set dm9110 to driver Heidelberg Digimaster 9110 (PS).
```

```bash
root# rpcclient SAMBA-CUPS -U root%secret -c 'enumprinters'
cmd = enumprinters
flags: [0x800000]
name: [\\SAMBA-CUPS\dm9110]
description: [\\SAMBA-CUPS\dm9110,Heidelberg Digimaster 9110 (PS),\
110ppm HiVolume DANKA Stuttgart]
comment: [110ppm HiVolume DANKA Stuttgart]
[...]
```

```bash
root# rpcclient SAMBA-CUPS -U root%secret -c 'setdriver dm9110 mydrivername'
cmd = setdriver dm9110 mydrivername
Successfully set dm9110 to mydrivername.
```

```bash
root# rpcclient SAMBA-CUPS -U root%secret -c 'enumprinters'
cmd = enumprinters
flags: [0x800000]
name: [\\SAMBA-CUPS\dm9110]
description: [\\SAMBA-CUPS\dm9110,mydrivername,\
110ppm HiVolume DANKA Stuttgart]
comment: [110ppm HiVolume DANKA Stuttgart]
[...]
```

可能不容易识别出第一次调用 `enumprinters` 时显示的“dm9110”打印机在应该列出驱动程序的位置（描述字段中的两个逗号之间）是一个空字符串。在 `setdriver` 命令成功后，一切正常。

### 20.8.3 使用 Windows NT APW 添加新打印机

默认情况下，Samba 在 `Printers`（打印机）文件夹中显示 `smb.conf` 中定义的所有打印机共享。该文件夹中还包含 Windows NT 添加打印机向导图标。仅在以下情况下才会显示 APW：

- 连接的用户能够以管理员权限（即 `root` 或 `printer admin`）成功执行 `OpenPrinterEx(\\server)`。

> **提示**
>
> 尝试从 Windows 2000/XP DOS 框命令提示符执行此操作：
>
> runas /netonly /user:root rundll32 printui.dll,PrintUIEntry /p /t0 /n \\SAMBA-SERVER\\printersharename
>
> 点击 `Printing Preferences`（打印首选项）。

- ... 包含设置 show add printer wizard = yes（默认值）。

APW 可以执行以下操作：

- 将新驱动程序上传到 Samba `[print$]` 共享。
- 将上传的驱动程序与现有的（但尚无驱动程序的）打印队列关联。
- 用之前上传的驱动程序交换现有打印队列当前使用的驱动程序。
- 向 Samba 主机添加一个全新的打印机（仅在与可用的添加打印机命令结合使用。也可以提供相应的删除打印机命令，用于从打印机文件夹中删除条目）。

最后一个（添加新打印机）比前面的操作需要更多的努力。要使用 APW 成功向 Samba 服务器添加打印机，添加打印机命令必须有一个定义好的值。程序钩子必须成功将打印机添加到 UNIX 打印系统（即 `/etc/printcap`、`/etc/cups/printers.conf` 或其他适当文件），必要时也要添加到 `smb.conf`。

当从客户端使用 APW 时，如果命名的打印机共享不存在，`smbd` 将执行添加打印机命令并拒绝尝试定位新的打印机共享。如果该共享仍未定义，则向客户端返回“拒绝访问”错误。添加打印机命令在连接用户的上下文中执行，不一定是 `root` 账户。`map to guest = bad user` 可能无意中让你以错误的权限连接。你应该使用 `smbstatus` 命令进行检查。

### 20.8.4 错误消息：“无法使用不同的名称连接”

一旦你使用错误的凭据连接，除了关闭所有资源管理器窗口，甚至重启外，没有其他办法扭转局面。

- `net use \\SAMBA-SERVER\\sharename /user:root` 会给出一个错误消息：“不允许同一用户使用多个用户名多次连接到服务器或共享资源。断开与该服务器（特别是共享资源）的所有先前连接，然后重试。”
- 任何试图将“网络驱动器”连接到 `\\SAMBASERVER\\print$` 为 z: 的尝试都会遇到顽固的消息：“当前此网络文件夹在凭据（用户名和密码）不同的情况下连接。首先断开到此网络共享的任何现有连接，以便使用不同的用户名和密码重新连接”。

所以你关闭所有连接。再试一次。你得到相同的消息。你从 Samba 端使用 `smbstatus` 检查。是的，有更多的连接。你终止它们所有。客户端仍然给出相同的错误消息。你在高调试级别监视 `smb.log` 文件并尝试重新连接。相同的错误消息，但日志中没有一行记录。你开始怀疑是否有任何连接尝试。你在尝试连接时运行 `ethered` 和 `tcpdump`。结果：没有单字节数据包。Windows 仍然给出错误消息。你关闭所有资源管理器窗口并重新开始。你尝试连接——这次成功了！Windows 似乎在某个地方缓存连接信息，并且不会将其保持最新（如果你不幸运，可能需要重启才能消除错误消息）。

从客户端到服务器强制终止所有连接的最简单方法是执行：

```
C:\>  net use * /delete
```

这将断开所有映射的驱动器，并允许你根据需要创建新的连接。

### 20.8.5 组装驱动程序文件时要小心
