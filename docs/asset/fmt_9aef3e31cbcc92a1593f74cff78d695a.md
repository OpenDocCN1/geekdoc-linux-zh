
[printers] 之后的前六行描述了一般访问控制。`browseable` 参数允许客户端浏览打印机列表。包含 `guest` 的行指定用户应仅作为访客打印文件。`path` 指定临时文件的位置（当你发出打印请求时，它会先到此位置，然后再到打印机）。使用 `/tmp` 可以更轻松地调试问题（例如，如果 `lpd` 请求失败并堆积）。无论如何，你应该指定一个你的匿名用户（通常是默认的 `nobody`）可以写入的位置。

上面的示例中的第二组行说明了 SAMBA 如何处理打印命令。这些命令是 `printing = BSD` 设置下的默认值。如果你使用的是 LPRng（我们推荐），请将 BSD 改为 `LPRNG`。LPRng 命令的工作方式与 BSD 命令类似，但 `lpq` 的输出不同（请参阅下面的问题，了解这种情况会发生什么）。

此示例中的打印机列表直接来自 `/etc/printcap`（使用最后一行的 `printcap name` 参数）。这通常是合适的，但你可能希望限制打印机列表。复制现有的 `/etc/printcap` 文件，在副本中删除不需要的打印机，并将 `printcap name` 设置为此新修改的文件。

## PROBLEM 36

症状：打印机队列在 Windows 客户端上没有显示。临时文件以 `lpq` 开头并堆积起来。

问题：SAMBA 无法正确解析 `lpq` 输出。

修复：确保 `lpq` 命令设置为正确的语法，并验证 `printing` 参数值。Linux 有三种主要可能的值：`LPRNG`、`PLP` 和 `BSD`。打印实用程序（`lpr`、`lpd` 等）的手册页应说明你系统上安装了哪种打印 spooler。

## PROBLEM 37

症状：过了一段时间，`/tmp`（或你设置的 `path`）中会出现几个名为 `lpq.*` 的文件。

问题：有时 SAMBA 没有清理好自己。

修复：有时队列检查器可能出现故障并丢弃文件。你应该保留一个 cron 作业来运行 `find` 并删除这些旧文件。例如，如果 `smb.conf` 指定 `path = /tmp`，请将此命令放入系统 crontab 中：

```
find /tmp -name 'lpq.*' -ctime 1 -exec rm '{}' ';' > /dev/null 2>&1
```

## PROBLEM 38

症状：打印作业被破坏或失败。PostScript 源代码作为文本打印。

问题：打印作业开头出现垃圾字符。

修复：某些 Windows 打印驱动程序会在作业前加上 `^D`，试图清除打印机内存。但在 Unix 打印队列的情况下，如果作业的前两个字符不是 `%!`，打印过滤器可能会混淆。首先尝试在 `smb.conf` 文件中添加

```
postscript = yes
```

这并不会去掉 `^D`，而是会在每个作业前发送一个 `%!`。这可能不适合你的打印机——在这种情况下，你需要设计另一个过滤器，在将任何作业发送到打印机之前先查看第一个字符。

### Single Printer Sections

对于 `[printers]` 部分之外的单个打印机，添加如下部分：

```
[myprinter]
guest ok = true
guest only = true
printable = yes
```

```
print command = send_job_command -Pmyprinter %s
lpq command = /usr/bin/lpq -Pmyprinter
lpm command = /usr/bin/lprm -Pmyprinter %j
path = /tmp
```

在这里，无论你将 `send_job_command` 指定为什么，它都会将作业发送到打印机。你可能希望这样做以绕过打印过滤器或添加不同的过滤器。相关手册页：`lpr (1)`、`lpq (1)`、`lprm (1)`、`lpd (8)`

## 文件共享

你可以通过两种方式在 SAMBA 的 `smb.conf` 文件中向 Windows 客户端导出目录。一种是使用常规部分，另一种涉及特殊的 `[homes]` 部分。下面是一个常规部分中非常简单的单路径共享示例：

```
[projects]
path = /stage/projects
valid users = +staff
writeable = yes
```

在这里，我们允许 `staff` 组中的用户对 `/stage/projects` 进行读写访问。若要将 `/stage/projects` 用作 Windows 机器上的网络驱动器，可以在 MS-DOS 命令提示符下输入以下内容：

```
net use g: \\SERVER\PROJECTS /user:username
```

在这里，`SERVER` 是 SAMBA 服务器的 NetBIOS 名称，`username` 是 `staff` 组中的用户。我们还假设 `g:` 当前未被使用。类似地，你可以通过右键单击 Windows 机器上的“我的电脑”图标，然后在菜单上选择“映射网络驱动器”来连接网络驱动器。

## 名称变更

由于 DOS 风格文件名的限制，SAMBA 呈现的文件名与它们在 Unix 文件系统中的实际显示不同。这并非巧合，SAMBA 将这种操作称为名称变形（name mangling）。你会得到像 `XINIT~3L.193` 这样的名称，因为 Windows 无法处理特别长的名称。

有两种方式可从 SAMBA 服务器请求主目录。第一种是显式方式，如以下 DOS 命令所示：

```
net use g: \\SERVER\username1 /user:username2
```

当你发出这个请求时，`SERVER` 上的 SAMBA 服务器首先会查看 `\\SERVER\username1` 中的 `username1` 部分，就像它在 `smb.conf` 中任何其他部分通常所做的那样。如果 `username1` 匹配任何其他部分，则使用该匹配部分。但是，如果不匹配且存在 `[homes]` 部分，SAMBA 会在返回错误之前再尝试一次：它查找 `username1` 的主目录，如果该 `username1` 是 SAMBA 服务器上的用户，则该主目录成为共享。`username2` 是要连接的 Linux 用户（通常与 `username1` 相同）。

另一种请求主目录共享的方式是隐式方式：

```
net use g: \\SERVER\homes /user:username
```

在这里，你直接告诉 SAMBA 你想要你的主目录，并且你的登录名是 `username`。以下是一个相当安全的 `[homes]` 部分示例：

```
[homes]
guest ok = no
browseable = no
```

是否希望用户能够写入这些目录（使用 `writable` 参数）由你决定。文件权限最终由 SAMBA 服务器上底层的 Unix 文件系统决定；SMB 客户端只能写入连接用户有权限写入的文件和目录。

一旦你查看用户的共享，它就会出现在共享列表中。如果你不喜欢 `[homes]` 部分的工作方式，你可以设置一个更简单的，如下所示：

```
[u]
guest ok = no
path = /home/%u
```

对 `\\SERVER\%u` 的任何访问都会解析为用于连接的账户的主目录（此示例假设你的所有主目录都在 `/home` 下）。

## SAMBA 客户端

SAMBA 附带一个名为 `smbclient` 的程序。它适用于偶尔的远程访问用途，以及调试你自己的 SAMBA 服务器的 `smb.conf` 文件。用法如下：

```
$ smbclient '\\SERVER\share'
```

你可以使用 `-U user` 来更改用户（默认是你的登录名）。除非你指定 `-P passwd` 选项，否则它会要求你输入密码。如果你尝试访问访客共享，可以指定空密码，或者只需在密码提示符处按回车。成功后，`smbclient` 会给你一个类似这样的提示符：

```
Domain=[MYWRKGRP] OS=[Unix] Server=[Samba 2.0.6]
smb: \>
```

从那里，你可以使用类似于 ftp 的 `put`、`mput`、`get`、`mget` 等命令。使用 `help` 查看完整列表。

如果你想定期使用 Windows 机器上的共享，应考虑 Linux 内核中可用的 SMB 文件系统。要使用它，首先让你的内核支持 `smbfs`，方法是将其编译进内核，或将其构建并加载为模块（后者更可取——参见第 7 章）。然后在你的 SAMBA 包中查找一个 `smbmount` 程序，它结合了 `smbclient` 和 `mount` 程序：

```
# smbmount '\\SERVER\SHARE' -c 'mount /mnt' -U user -P password
```

相关手册页：`smbclient (1)`、`smbmount (8)`

## 4.3 Netatalk

要让你的 Linux 机器支持 AppleTalk，你需要两样东西：对 AppleTalk 底层协议的内核支持，以及向客户端提供服务（如文件共享和打印）的服务器程序。AppleTalk 有许多底层协议（传输机制），但在本地网络上最常见的是运行在以太网之上的 DDP。在“网络选项”下有对应的内核配置选项；它称为 AppleTalk DDP，你应该按照第 7 章的描述将其配置为模块。
