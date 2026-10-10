
前三个示例显示了本地打印机（并行、串口和 SCSI）的格式。
其他示例是远程主机。在每情况下，`hostname` 可以是主机名或 IP 地址。端口或路径标识了每个打印机在主机上的位置。

# 使用打印命令

为了与旧版本的 UNIX 和 Linux 打印设施保持后兼容，CUPS 支持许多用于打印操作的旧命令。大多数使用 CUPS 的命令行打印可以通过 `lpr` 命令完成。Linux 下的文字处理应用程序（如 StarOffice、OpenOffice.org 和 AbiWord）可以使用此功能进行打印。

通过打印机配置窗口，你可以为每台打印机定义所需的过滤器，以便文本能够正确格式化。`lpr` 命令的选项可以添加过滤器来正确处理文本。管理打印文档的其他命令包括 `lq`（用于查看队列内容）、`lpm`（用于从队列删除打印作业）和 `lpc`（用于控制打印机）。

> 交叉引用：第 6 章提供了如何在多种格式（包括 troff 和 TeX）中格式化和打印文档的示例。

## 使用 lpr 打印

通过 `lpr` 命令，你可以将文档打印到本地和远程打印机。文档文件可以通过设置 `lpr` 命令行的值，也可以通过管道 (`|`) 使用 `lpr` 命令添加。这里是一个简单的 `lpr` 命令示例：

```
$ lpr doc1.ps
```

当你使用 `lpr` 指定文档文件时，输出将定向到默认打印机。作为普通用户，你可以通过设置 `PRINTER` 变量的值来更改默认打印机。通常，你会将 `PRINTER` 变量添加到其中一个启动文件中，例如 `$HOME/.bashrc`。以下是添加到 `.bashrc` 中的一行，用于将你的默认打印机设置为 Lp3：

```
export PRINTER=lp3
```

为了让新的 `PRINTER` 值立即生效，请源化 `.bashrc` 文件（输入 `source $HOME/.bashrc`）。要覆盖默认打印机，请在 `lpr` 命令行上指定特定的打印机。以下示例使用 `-P` 选项来选择不同的打印机：

```
$ lpr -P canyonps doc1.ps
```

`lpr` 命令具有多种选项，允许 `lpr` 解释和格式化多种类型的文档。这些包括 `-num`（其中 `num` 被替换为要打印的副本数，1 到 100）以及 `-1`（导致文档以原始模式发送文档，假设文档已经格式化）。

# 第四部分：Fedora RHEL 网络和服务器设置

## 使用 lpc 列出状态

CUPS 中的 `lpc` 命令功能有限。你可以使用 `lpc` 来列出打印机的状态。这里是一个示例：

```
$ lpc status

hp:

  printer is on device 'parallel' speed -1

  queuing is enabled

  printing is disabled

  no entries

  daemon present

deskjet 5550:

  printer is on device 'usb' speed -1

  queuing is enabled

  printing is disabled

  no entries

  daemon present
```

此输出显示了两个激活的打印机。第一个 (`hp`) 连接到并行端口。第二个 (`deskjet 5550`) 是一个 USB 打印机（显示为 `usb`）。`hp` 打印机目前已禁用（离线），尽管队列已启用，以便人们可以将作业发送到打印机。

## 使用 lprm 删除作业

用户可以使用 `lprm` 命令从队列中删除他们自己的打印作业。在命令行上单独使用时，`lprm` 会从默认打印机删除该用户的所有打印作业。要删除特定用户的作业，请使用 `-P` 选项，如下：

```
$ lprm -P lp0
```

要删除当前用户的打印作业，请输入以下：

```
$ lprm -a
```

要从队列中删除单个打印作业，请在 `lprm` 命令行上指定该作业的作业号。要查找作业号，请输入 `lpq` 命令。该命令的输出可能：

```
$ lpq

printer is ready and printing

Rank Owner Job Files Total Size Time
```

### 第 17 章：设置打印服务器 751

输出显示了两个激活的作业。要删除作业，请输入以下：

```
$ lprm -j [job_id]
```

## 配置打印服务器

要与网络上的其他计算机共享打印机，有以下几种方法：

- **打开防火墙**：如果你有一个限制性的防火墙，它可能不会允许远程用户访问你的打印机。你必须允许访问端口 513 (UDP) 以及可能的端口 631 以允许在计算机上打印。有关配置防火墙的信息请参阅第 14 章。
- **启用 LPD 风格打印**：某些应用程序可能需要旧的 LPD 风格打印服务来连接打印机。要启用它，启动 `cups-lp` 服务。作为 root 用户，执行 `service cups-lp`。然后重启守护进程。要使用此服务，你可能需要安装 `cups-lp` 包（`yum install cups-lp`）。
- **检查名称和地址**：确保你在另一台计算机上配置时，正确输入了计算机名称和队列。使用 IP 地址而不是主机名（如果是这样，会导致 DNS 问题）。运行类似 Wireshark 的工具可以观察哪里出错。

### 配置共享 Samba 打印机

你的 Linux 打印机可以配置为共享 Samba 打印机。要将你的打印机配置为 Samba (SMB) 打印机，你只需要按照第 18 章所述配置基本的 Samba 服务器设置。默认情况下，你的所有打印机都在本地网络上共享。下一节显示了结果设置的内容以及你可能想要如何修改它们。

## 理解打印的 smb.conf

当你配置 Samba 时（如第 18 章所述），`/etc/samba/smb.conf` 文件将被配置为允许共享所有定义的打印机。以下是 `smb.conf` 文件中 `[global]` 和 `[printers]` 部分中可能与打印机共享相关的几行：

```
[global]

workgroup = MYGROUP

serverstring = Samba Server

security = share
```

### 第 17 章：设置打印服务器 753

```ini
printcap name = /etc/printcap

load printers = yes

printing = cups

encrypt passwords = yes

smb passwd file = /etc/samba/smbpasswd

unix password sync = Yes
```

```ini
[printers]

comment = All Printers

path = /var/spool/samba

guest ok = yes

browse = no

writeable = no

printable = yes
```
