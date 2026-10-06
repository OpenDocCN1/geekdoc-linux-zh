
```
option = value
```

你有数百个选项和值可供，你在这里看到的是最常用的。要查看完整的选项列表，请参阅 `smb.conf` man 手页。一些最重要的选项是：

- `workgroup = Tardis` — 这是 Windows 计算机网络框标识选项卡中显示的工作组名称。

- `smbpasswd file = /etc/samba/smbpasswd` — 这显示了 Samba 密码文件的位置路径。确保你的 `smb.conf` 文件中包含此选项/值对。

## 连接到微软和 Novell 网络

- `encryptpasswords = yes` — 从 Windows NT service pack 3 及更高版本开始，密码是加密的。如果你正在连接到运行这些版本 Windows 的任何系统，你应该选择加密密码。

- `netbios name = RHL` — 这是 Samba 服务器被 Windows 计算机识别的名称。

- `server string = Samba Server` — 这在网络浏览器的 Windows PC 中作为注释显示。

- `security = user` — 这是应用于服务器访问的安全性级别。其他选项有 `share`、`domain` 和 `server`。`share` 用于方便创建不需要身份验证的匿名名称，当 Windows 计算机的 NetBIOS 名称与 Linux 计算机上的其他名称不同时，它非常有用。`server` 用于在密码文件位于网络中另一台服务器时指定要使用的服务器。如果使用 `smpassword` 将客户端添加到 Windows NT 域，并且登录请求由 Windows NT 主或备用域控制器执行，则使用 `domain`。

- `log file = /var/log/samba/log` — 这是文件可以增长的最大尺寸（单位为 KB）。

- `socket options = TCP_NODELAY SO_RCBUF=8192 SO_SNDBUF=8192` — 这允许对缓冲区进行调优。

- `dns proxy = no` — 表示没有 DNS 名称查找。

### [homes]

`smb.conf` 文件的下一部分 `[homes]` 用于启用主目录。参考 `smb.conf` 文件以获取有关以下内容的更多描述：

- `comment = Home Directories`

- `browseable = yes` — 意味着目录出现在 Windows 浏览器中。

- `writeable = yes` — 意味着用户可以写入目录。

- `create mode = 0664`

- `directory mode = 0775`

- `max connections = 1` — 最大连接数。

### [printers]

此节设置了打印的选项：

- `browseable = yes` — 意味着目录出现在 Windows 浏览器中。

- `printable = yes` — 允许客户端发送打印作业。

- `path = /var/spool/samba` — 打印位置

- `comment = All Printers`

## 创建 Samba 用户

如果你使用的是安全模式并分配了域而不是工作组，则不需要创建 Samba 用户，因为用户将登录到域控制器。但在本例中，我们将创建 Samba 用户。你可以通过运行 `/etc/passwd` 将所有系统用户转换为 Samba 用户：

```
cat /etc/passwd | mksampword.sh > /etc/samba/smpwd
```

此工具只创建用户账户，而不创建密码。你需要使用 `smpassword` 命令和用户名为用户创建密码，如下所示：

```
[root@terry]# smpassword terry
New SMB password:
Retype new password:
Password changed for user terry
Password changed for user terry
```

## 启动 Samba 服务器

最后一步是启动 Samba 守护进程。启动 Samba 的命令是：

```
[root@terry]# /sbin/service smb start
Starting SMB services:      [ OK ]
Starting NMS services:     [ OK ]
```

此时你的系统中应该运行着一个正常的 Samba 服务器。它配置为允许具有系统账户的用户从 Windows PC 访问其主目录。登录用户还可以使用为 Red Hat 配置的打印机。

## 连接到 Samba 客户端

在本节中，你将学习如何将你的系统连接到运行 SMB 协议的其他系统。连接运行 Windows 2000 或 XP 的 PC 将在本章后面的“从 Windows PC 连接到 Samba 服务器”部分中介绍。你可以将系统连接到任何运行 SMB 协议的计算机，无论它是 Windows PC 还是运行 Samba 的 Linux 系统。可以通过命令行通过两种方法进行连接。第一种方法使用名为 `smbclient` 的工具，命令语法为 `smbclient //computer name/sharename`，如下例所示。请确保将示例中的计算机名称替换为你的计算机名称。

### 346 第 14 章

```
[root@terry]# smclient //terrycollings/c
added interface ip=192.168.9.93 bcast=192.168.9.255 nmask=255.255.255.0
got positive name query from 192.168.9.102 (192.168.9.102)
Password:
Domain=[Tardis] OS=[Windows 5.0] Server=[Windows 2000 LAN Manager]
smb: \\
```

上面的示例展示了我如何从我的 Red Hat 系统登录到我的 Windows PC。系统提示我输入密码登录，并提供了有关 Windows 系统的信息以及命令提示符。你可以在命令提示符处输入 `help` 获取可用命令列表。`smb` 提示符下的命令与命令行 FTP 命令非常相似。要退出连接，请输入 `exit`。

让 Samba 客户端上的文件在你的 Red Hat 系统上可访问的另一种方法是将该文件系统挂载到你的文件系统中。你可以使用 `smbount` 命令来实现。该命令的语法为 `smbount //计算机名/目录/system/挂载点`，如下所示：

```
[root@terry]# smbount //terrycollings/c /mnt/windows
Password: 
```

接下来，你可以通过执行以下命令切换到挂载 Windows 系统的目录：

```
[root@terry]# cd /mnt/windows
```

然后，你可以使用 `ls` 命令获取目录列表：

```
[root@Terry windows]# ls
arcclder.exe MSDOS.SYS quicktime
arcsetup.exe Mulsnet Setup QuickInstaller.zip
AUTOEXEC.BAT My Download Files Recycled
boot.ini My Music rhsa
camtasia NalCach W2K.CD
CONFIG.SYS netplus Windows Update Setup Files
Documents and Settings Novell WINNT
Drivers WBTEXT.COM WHERECOME.ID
fgc ntdlr WT61CE.ULS
Hiberfil.sys p2.pdf WT610Z.ULS
IO.SYS datafile.sys WT61UK.ULS
config.aot Program Files WT61US.ULS
Local Mulsnet PUTTTY.RND
```

在这个示例中，我连接到了与上一个示例中相同的 Windows PC。但是，通过使用 `smbount` 命令，我将 Windows 文件系统挂载到了我的 Red Hat 文件系统中。在输入 Windows PC 密码并返回命令提示符后，我切换到刚刚挂载的目录并运行 `ls` 命令来获取 Windows PC 共享目录的列表。现在，可以使用常规文件工具轻松地在两个系统之间移动文件。

可以将 `mount` 命令写入本地启动脚本中，这样在系统启动时就会挂载目录。使用之前所示的命令，并向包含登录用户名和密码的文件添加选项。

```
smbount //terrycoliggins/c /windows -o credentials=/home/terry/.sambacred
```

你需要按照如下代码所示创建一个文件。我创建了一个名为 `.sambacred` 的隐藏文件，并在文件中放置了以下两行：

字体 Username = terry

- password = (password)

请确保在文件路径和用户名处填写与你的系统相关的信息。创建隐藏文件并在 `smbount` 命令中引用它的目的是为了防止他人以明文形式发现文件中的密码。请务必相应修改此文件的权限。

使用这种方法比将挂载信息放在 `/etc/fstab` 文件中更优。虽然可以将挂载信息放在 `/etc/fstab` 文件中，但他人可以通过查看 `/etc/fstab` 文件发现用户名和密码。

要卸载客户端系统文件，输入 `smbumount` 命令以及要卸载的目录路径：

```
# smbount /mnt/windows
```

按下回车键后，文件系统将被卸载。

## 从 Windows PC 连接到 Samba 服务器

现在你就可以在 Windows PC 上测试连接了。对于运行 Windows 2000 或 XP 的系统，不需要配置。在 Windows 上，双击桌面上的“我的网络位置”图标。在网络位置窗口中，你现在将看到 Red Hat 计算机的列表，在本示例中它是 `rhl10`。双击 rhl10 PC 图标，你将看到可用的共享。

### 第 14 章

## 为什么使用 Samba 而不是 NFS？

之前，你设置了网络文件系统（NFS）以实现跨网络的文件共享。那么，为什么不使用 NFS 来共享 Windows 文件呢？嗯，你本这样做，但使用 Samba 与 Windows 计算机通信更有意义。Windows 系统并非原生支持 NFS；服务器消息块（SMB）协议是 Windows 计算机相互通信的方式。它是 Windows 共享文件和打印机的原生协议。通过使用相同的协议，你可以确保文件和打印机共享以最小的难度运行。

当你从 rhl10 PC 双击目录共享（share）时，系统会提示你输入用户名和密码以进入目录。仅此而已。你现在可以在你的 Linux 和 Windows 计算机之间共享文件了。

> **提示**：你可以使用 Windows“映射网络驱动器”命令来设置 Windows 系统，在启动 Windows PC 时始终连接到你的 Samba 共享。

> **交叉引用**：要学习如何设置在 Samba 下使用的打印机，请参阅第 10 章。

## 连接到 Novell 网络

使用 Red Hat Enterprise Linux，你可以轻松地配置系统连接到 Novell 服务器。在本节中，你将学习如何将你的 Red Hat 系统配置为 Novell 客户端。

为了启用 Novell 服务器与你的 Fedora 或 Red Hat Enterprise 系统之间的通信，需要安装两个包。第一个加载包是 `ipxutils`，它是网数据包交换（IPX）——Novell 的网络协议。你需要加载的第二个包是 `ncpfs`——Novell 文件系统包。如果你的系统上没有安装这些包，可以在 Red Hat 安装光盘上找到这些 RPM 包。在继续之前请安装这些包。

安装包后，在配置 Novell 客户端之前，需要加载两个模块。从终端命令提示符，输入以下命令加载模块。

```
# /sbin/modprobe ipx ncpfs
```

### 连接到 Microsoft 和 Novell 网络 347

> **注意**：`ipx` 和 `ncpfs` 模块现已安装。

加载模块后，你需要通过输入以下命令来配置 IPX 连接，启用接口和主站：

```
/sbin/ipx_configure -auto=on -primary=on
```

如果配置正确，可以通过 `slist` 命令检查连接。`slist` 的输出如图 14-1 所示。

| 名称 | 描述 |

| :--- | :--- |

| BART | Novell 服务器 |

![](img/b5eb2d43ffbc348ca020521f962cb_385_0.png)

图 14-1 `slist` 命令输出显示 Novell 服务器。

假设你想登录图 14-1 所示的 BART 服务器，将其文件系统挂载到你系统的 bart 目录下。你需要输入命令：

```
# ncpmount -S BART -terry.mediervices.admin -P password /home/terry/novell/bart
```

登录并挂载 Novell 文件系统后，目录列表将显示服务器的内容。请确保将示例中的信息替换为适用于系统的信息。

通过执行 `ncpmount` 命令并指定挂载点可以卸载 NCP 文件系统。系统关闭期间，NCP 挂载会被干净卸载，因此无需在关闭系统之前卸载文件系统。

如果你不想每次启动系统时都手动配置系统作为 Novell 客户端，你应该将本节中的命令放在你的 `rc.local` 文件中。这样配置会在启动时自动进行。

> **交叉引用**：有关如何配置 Novell 网络打印机的更多信息，请参阅第 10 章。

## 总结

在本章中，你学习了服务器消息块（SMB）协议。该协议用于 Windows 计算机相互通信。你学习了名为 Samba 的 Linux 程序，它模拟 SMB 协议并可用于连接 Linux 网络和 Windows 网络。你在 Red Hat Enterprise Linux 服务器上安装并配置了 Samba，并配置了 Windows 客户端。你还学习了如何使用 NCP 文件系统将你的 Red Hat 系统配置为 Novell 客户端。

# 第 15 章

# 配置数据库服务器

本章内容

- Linux 数据库服务器

- 使用 MySQL

- 使用 PostgreSQL

随着 Linux 继续深入渗透企业领域，它正越来越多地用于存储企业数据。本章描述了在 Fedora Core 和 Red Hat Enterprise（红帽企业版）上对主要的关系型数据库管理系统（RDBMS）进行安装、配置和测试：MySQL 和 PostgreSQL（这两个最流行的开源 RDBMS），以及作为商业 RDBMS 中“巨无霸”的 Oracle。本章的范围仅限于帮助你安装这些数据库系统并验证已安装系统的基本功能。为了让你有合理的预期，在阅读完本章后，你不会成为数据库专家，因为我们没有涵盖 SQL 数据库设计、查询优化或任何其他特定数据库的主题。那些主题值得专门写一本书（每个主题）。

## Linux 数据库服务器

正如 Linux 继续在 Web 服务器和集群计算领域占据主导地位，Linux 正逐渐成为托管企业数据的首选操作系统，其原因与它主导 Web 服务和高性能计算的原因相同：Linux 快速、稳定、可靠、可调优且灵活；源代码可用，并且可以在通用硬件上运行。大多数主流数据库，包括 Oracle、DB/2、Informix、MySQL 和 PostgreSQL，都运行在其之上。因此，系统管理员必须应对运行数据库服务器的事务。

作为系统管理员，你很少对在服务器上运行以及你负责维护的数据库拥有最终决定权或投票权。事实上，比你处于食物链中位置更高的人通常会做出决定。尽管如此，确保服务器运行、可接受且性能良好仍然是你的责任。在大多数机构中，Linux 系统管理员不负责数据库的日常维护和管理，因为这些任务由数据库管理员（DBA）处理。在规模较小的站点，可能没有专职 DBA 的条件，你可能需要承担更多数据库维护的责任，但原则上，你不会编写查询、构建应用程序或为数据库提供技术支持。

尽管如此，熟悉你的系统或多个系统所提供的服务是至关重要的。至少知道如何安装数据库服务器以及如何确保它运行是重要的，因为 DBA 有时可能缺乏管理运行数据库所运行的系统的能力；你的工作是打理数据库，而不是运行它的的硬件和操作系统。

无论使用哪种数据库，启动数据库服务器的基本步骤都是相同的：

1. 安装并配置硬件。

2. 安装并配置操作系统。

3. 安装并配置数据库软件以创建标准安装。

4. 确保基础安装工作正常。

5. 为数据库设置监控和备份作业。

6. 将其交给 DBA（或们）。

本章的目的是解决第 3 步和第 4 步。当然，涉及到安装和配置数据库软件的具体细节。同样，确保默认安装正常需要根据你所使用的数据库采取不同的措施。由于本章的长度不足以涵盖所有流行的数据库包，因此它重点集中在最流行的两个上：MySQL 和 PostgreSQL。MySQL 是自由软件世界中三者中最流行的，在安装量方面无疑超过了 PostgreSQL。我们选择 PostgreSQL 是因为它是 Fedora Core 和 RHEL 的一部分，因为它是红帽数据库（Red Hat Database）底层的数据库技术。总而言之，熟悉这两个数据库包应该能涵盖你必须安装、配置和维护数据库服务器的大多数情况。

# 配置数据库服务器

## 使用 MySQL
