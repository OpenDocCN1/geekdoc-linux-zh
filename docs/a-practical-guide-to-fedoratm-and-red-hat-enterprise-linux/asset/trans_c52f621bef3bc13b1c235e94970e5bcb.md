
## 传统 UNIX 打印

在图形用户界面（GUI）和所见即所得（WYSIWYG）（第 1281 页）文字处理软件出现之前，UNIX 用户会使用 *vi* 等编辑器和 *TeX* 或 *nroff/troff* 等排版标记语言来创建文档，使用解释器将生成的文件转换为 PostScript 格式，然后使用 *lpr*（BSD）或 *lp*（System V）将 PostScript 文件发送到打印机。为了兼容性，Linux 实现了 BSD 和 System V 的命令行打印实用程序。然而，这些实用程序现在是 CUPS 中同等功能的封装器，而不再是打印系统的核心组件。相应的实用程序在功能上是等效的；请任选其一使用（表 13-2）。

### 表 13-2：`lpr` BSD 和 System V 命令行打印实用程序

| **BSD/SysV** | **用途** |
| :---------- | :---------- |
| `lpr`/`lp` | 将作业发送到打印机 |
| `lpg`/`lpstat` | 显示打印队列的状态 |
| `lprc`/`cancel` | 从打印队列中移除作业 |

在命令行中，你可以使用 `lp` 打印文本、PostScript 或 PDF 文件：

```bash
$ lp memo.txt
request id is MainPrinter-25 (1 file(s))
```

上述命令将 `memo.txt` 添加到默认打印机的打印队列中，并分配作业编号 25。当该打印机可用时，它将打印该文件。你可以使用 `-d` 选项指定打印机：

```bash
$ lp -d HL2140 graph.ps
request id is HL2140-26 (1 file(s))
```

`lpr -P` 选项与 `lp -d` 选项等效。

如果没有参数，`lp` 和 `lpr` 会将标准输入发送到打印机：

```bash
$ cat memo2.txt | lpr
request id is MainPrinter-27 (1 file(s))
```

`lpg` 和 `lpstat` 命令显示有关打印队列的信息：

```bash
$ lpstat
MainPrinter-25    zach      13312   Sun Feb 23 18:28:38 2014
HL2140-26         zach      75776   Sun Feb 23 18:28:48 2014
MainPrinter-27    zach      8192    Sun Feb 23 18:28:57 2014
```

使用 `cancel` 或 `lprm` 从打印队列中移除作业。默认情况下，只有打印作业的拥有者或具有 `root` 权限的用户才能移除作业。

```bash
$ cancel 27
$ lpstat
MainPrinter-25    zach      13312   Sun Feb 23 18:28:38 2014
HL2140-26         zach      75776   Sun Feb 23 18:28:48 2014
```

在具有 `root` 权限时，输入命令 `cancel -a` 或 `lprm -` 以从打印队列中移除所有作业。

## 从 Windows 打印

本节介绍如何从 Windows 机器使用 Linux CUPS 服务器上的打印机。与使用 Samba 从 Windows 打印相比，管理 CUPS 更容易，并且可以配置得更安全。

### 使用 CUPS 打印

现代版本的 Windows（2000 或更高版本）支持 IPP，因此可以直接与 CUPS 通信。要使用此功能，必须配置 Linux 打印服务器上的 CUPS 以允许远程 IPP 打印；还需要在 Windows 系统上创建一个新的打印机，指向 Linux 打印服务器的 IP 地址。

首先，按照第 572 页“共享 CUPS 打印机”中的说明，设置 *etc/cups/cupsd.conf* 文件以允许客户端进行网络打印。配置 CUPS 以允许从 Windows 机器打印与配置允许从 Linux 客户端系统打印完全相同。如有必要，按照第 557 页的说明打开防火墙。

**Windows XP** 在 Windows XP 中，前往 **控制面板→打印机和传真**，点击 **添加打印机**。在介绍窗口中点击 **下一步**，选择 **网络打印机或连接到另一台计算机的打印机**。点击 **下一步**。选择 **连接到 Internet 或家庭/办公网络上的打印机**。继续按照下文“输入 URL”中的说明操作。

**Windows 7** 在 Windows 7 中，前往 **控制面板→设备和打印机**，点击 **添加打印机**。点击 **添加网络、无线或蓝牙打印机**。假设 Windows 未找到打印机，请点击 **我想要的打印机未列出**。点击标有 **按名称选择共享打印机** 的单选按钮。

**输入 URL** 在文本框中输入以下信息（在 Windows XP 中它标记为 **URL**）：`http://hostname:631/printers/printer-name`

其中 *hostname* 是 Linux CUPS 服务器系统的名称或 IP 地址，*printer-name* 是该系统上打印机的名称。例如，对于 IP 地址为 192.168.0.12 的系统 dog 上名为 dog88 的打印机，你可以输入 http://dog:631/printers/dog88 或 http://192.168.0.12:631/printers/dog88。如果你使用主机名，它必须在 Windows 机器上的 *hosts* 文件中定义。点击 **下一步**。Windows 会要求你指定打印机的制造商和型号，或者提供打印机驱动程序。如果你提供打印机驱动程序，请使用该驱动程序的 Windows 版本。

Windows 复制完某些文件后，打印机将出现在“打印机和传真”/“设备和打印机”窗口中。在 Windows 7 中，你需要再点击两个屏幕。右键单击打印机并选择 **设为默认打印机**，使其成为默认打印机。你可以通过右键单击打印机并选择 **属性或打印机属性** 来指定打印机的注释、位置和其他属性。

### 使用 Samba 打印

本节假设在控制你想从 Windows 使用的打印机的 Linux 系统上已安装并正在运行 Samba（第 827 页）。必须设置 Samba，以便将执行打印的 Windows 用户映射到 Linux 用户（包括将 Windows 来宾用户映射到 Linux 用户 *nobody*）。确保这些用户具有 Samba 密码。请参阅第 829 页的“Samba 用户、用户映射和密码”。

Windows 通过 SMB 支持打印机共享，这允许使用与文件共享相同的机制在 Windows 系统之间透明地共享打印机。

Samba 允许 Windows 用户使用连接到 Linux 系统的打印机，就像使用任何其他共享打印机一样。由于所有 Linux 打印机传统上看起来都是 PostScript 打印机，因此 Linux 打印服务器看起来是共享一个 PostScript 打印机。Windows 不包含通用的 PostScript 打印机驱动程序。相反，Windows 用户必须为 PostScript 打印机选择一个打印机驱动程序。Apple LaserWriter 12/640ps 驱动程序是一个不错的选择。

当你使用 *rpm* 安装 Samba 时，它会创建一个名为 /var/spool/samba 的目录，该目录由 *root* 账户所有，任何人都可以读写。为此目录设置了粘滞位（第 1275 页），允许作为 Linux 用户启动打印作业的 Windows 用户能够删除该作业，但拒绝用户删除其他用户的打印作业。确保该目录存在并具有正确的所有权和权限：

```bash
$ ls -ld /var/spool/samba
  drwxrwxrwt. 2 root root 4096 02-03 15:23 /var/spool/samba
```

取消 /etc/samba/smb.conf 文件 **[global]** 部分中以下两行的注释。

```ini
[global]
    ...
    printing = cups
    printcap name = cups
```

打印机的共享在 *smb.conf* 的 **[printers]** 部分中列出。在以下示例中，*path* 是 Samba 用作暂存目录的路径，而不是普通的共享路径。这些设置允许任何人（包括 *guest*）使用该打印机。默认 *smb.conf* 文件中的 **[printers]** 部分包含以下条目，这些条目适用于大多数设置：

```ini
[printers]
      comment = All Printers
      path = /var/spool/samba
      browseable = no
      guest ok = no
      writable = no
      printable = yes
```

理想情况下，计划打印的每个用户都应拥有一个账户。否则，当多个用户共享同一账户（例如，*nobody* 账户）时，他们可以相互删除对方的打印作业。

## 打印到 Windows

CUPS 查看 Windows 机器上的打印机的方式与其他任何打印机完全相同。唯一的区别是你连接时需要指定的 URI。要配置连接到 Windows 机器的打印机，请点击 CUPS Web 界面中的 **管理** 选项卡并选择 **添加打印机**，就像为本地打印机做的那样。

## CUPS 配置细节

Listen localhost:631
Listen /var/run/cups/cups.sock

在已注释的 Listen 指令的位置，使用访问控制列表来仅允许选定的机器连接到本地打印机。访问控制列表定义在 `<Location>` 容器内部（有关 Apache 的等效项，参见第 948 页）。以下示例仅允许 IP 地址为 192.168.1.101 的系统和本地系统打印到指定的打印机。

```apache
<Location />
 Order Allow,Deny
 # Allow access from the local system and 192.168.1.101
 Allow from localhost
 Allow from 192.168.1.101
 # Uncomment the following to permit access from all local interfaces
 Allow @LOCAL
 </Location>
```

`@LOCAL` 宏是 CUPS 内部的，指定本地系统。该宏接受来自解析为本地系统的任何地址的通信。指定 `Allow @LOCAL` 以在所有本地接口之间共享打印机。

当你更改 cupsd.conf 时，必须重启 cupsd 守护进程（第 557 页）。

*Order Allow,Deny* 指令默认拒绝打印请求，并允许来自指定地址的请求。*Order Deny,Allow* 指令默认允许访问，并且仅拒绝在 Deny 指令中指定的客户端。你可以在 `Allow from` 和 `Deny from` 指令中使用包含通配符的域名以及使用通配符或子网掩码的 IP 范围。这些指令的工作方式与 Apache 中的相同。欲了解更多信息，请参阅第 961 页的“Order”。

在使用 *Order Deny,Allow* 指令时，*Deny from* 指定 CUPS 不接受连接的唯 IP 地址。在使用 *Order Allow,Deny* 指令时，*Allow from* 指定 CUPS 接受连接的唯一 IP 地址。

重启 *cupsd* 后，远程系统可以使用由 *Listen* 指令指定的 IP 地址和端口号在本地系统的打印机上进行打印。如果服务器正在运行防火墙，你需要允许远程系统通过它连接到端口 631；参见第 557 页。根据系统配置，你可能还需要修改 SELinux 策略（第 475 页）。

