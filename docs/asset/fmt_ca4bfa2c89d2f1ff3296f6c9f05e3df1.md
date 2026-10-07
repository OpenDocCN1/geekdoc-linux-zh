
```
[printers]
comment = Ubuntu
browseable = no
writable = yes
path = /var/spool/samba
```

# 使用 testparam 命令测试 Samba

在你 Ubuntu 上正确配置后，你可以使用 `testparam` 命令来检查它。对于所有配置一样，如果你正在修改现有文件，谨慎的做法是将旧文件复制到另一个位置。然后，使用 `testparam` 检查文件。其语法如下：

```
matthew@semour:-$ testparam /path/to/smb.conf
Load smb config
Processing "[homes]"
Processing "[printers]"
Loaded services OK.
```

此输出显示配置是正确的，只要服务运行正常，Samba 就能工作。现在将旧的 `smb.conf` 文件移动到新位置，将其到位并重启 Samba。

# 启动、停止和重启 smbd 守护进程

在 `smb.conf` 文件配置正确后，你可能需要启动、停止或重启 Samba 守护进程。你可以使用 `/usr/sbin/smbd` 命令来实现（不带任何选项启动 Samba 服务器）。你最经常更改的选项是 `smb.conf` 文件的位置；如果你不想使用默认位置 `/etc/smb.conf`，则更改选项。`-s` 选项允许你更改 Samba 使用的 `smb.conf` 文件位置；这对于测试新的 `smb.conf` 文件是否有效也很有用。另一个有用的选项是 `-l` 选项，它指定 Samba 用于存储信息的日志文件。

要从命令行启动、停止或重启 Samba，使用 `/etc/init.d/samba` 脚本配合正确的关键字，例如：

```
matthew@semour:-$ sudo /etc/init.d/samba start
```

# 使用 smbstatus 命令

`smbstatus` 命令报告 Samba 连接的当前状态。语法如下：

```
/usr/bin/smbstatus [options]
```

表 21.2 显示了一些可用选项。

| 表 21.2 smbstatus 选项 |

| 选项 | 结果 |

| --- | --- |

| -b | 简洁输出 |

| -d | 详细输出 |

| -s /path/to/config | 如果启动时使用的配置文件不是标准文件 |

| -u username | 显示特定用户的连接状态 |

| -p | 列出当前的 smb 进程，在脚本中可能非常有用 |

# 让 Samba 运行起来

## 使用 smclient 命令连接

`smbclient` 允许其他 Linux 主机上的用户访问你的 smb 共享。你无法在宿主机上挂载该共享，但可以使用类似于 FTP 客户端的方式使用它。`smclient` 命令可以配合多个选项使用。最常用的是 `-l`，后面跟你要连接的计算机的 IP 地址。`smclient` 命令不需要 root 权限：

```
matthew@seymour:$ smclient -I 10.10.10.20 -U username&password
```

这将为你提供以下提示符：

`smb:` <共享目录上的当前目录>

从这里开始，命令与标准的 UNIX/Linux FTP 命令几乎相同。请注意，你可以在 `smbclient` 命令行中省略密码，此时系统会提示你输入 Samba 密码。

## 挂载 Samba 共享

有两种方法可以将 Samba 共享挂载到你的 Linux 主机上。挂载与挂载可用介质分区或远程 NFS 目录相同，只是 Samba 共享是通过 SMB 访问的。第一方法使用标准的 Linux `mount` 命令：

```
matthew@seymour:$ sudo mount -t smbfs //10.10.10.20/homes /mount/point -o username=heather,dmask=777,fmask=777
```

> 注意

如果你的名称服务正在运行或主机在你的 `/etc/hosts` 文件中，可以用 IP 地址替换主机名。

上述命令将 `heather` 的 `/home` 目录挂载到你的主机上，并赋予所有用户对挂载点的完全权限。这些权限等同于 `chmod` 命令中的权限。

第二方法使用 `smbmount` 命令产生相同的结果，如下：

```
matthew@seymour:$ sudo smbmount //10.10.10.20/homes /mount/point -o username=heather,dmask=777,fmask=777
```

要卸载共享，请使用以下标准命令：

```
matthew@seymour:$ sudo umount /mount/point
```

# 第21章 共享文件和打印机

你也可以使用这些挂载命令将真正的 Windows 客户端共享挂载到 Ubuntu 主机上。通过 Samba，你可以配置服务器提供 Windows 可以提供的任何服务，而且除了你之外没人会知道。

## 配置 Samba SWAT

Samba 开发者团队通过 Samba Web 管理工具 `SWAT` 使 Samba 的管理变得简单得多。`SWAT` 是一个基于 Web 的配置和主界面，尽可能接近点击式的 Samba 环境。本节提供了一个关于如何使用 `SWAT` 设置 SMB 访问用户的 `/home` 目录以及如何共享目录的简单示例。

> 注意 你需要通过命令 `sudo passwd root` 设置密码来启用 root 账户。不启用 root 账户将阻止你有效使用 `SWAT`。

在启动 `SWAT` 之前，你需要执行几个步骤。首先，确保已安装 Samba 和 `swat` 软件包。然后，通过编辑 `/etc/inetd.conf` 文件并删除以下行中存在的 `#<#>` 注释来启用 `SWAT` 访问系统：

```
#<#> swat stream tcp nowait.400 root/
/usr/sbin/tcpd /usr/sbin/swat
```

保存文件并使用以下命令重启 `openbd-inetd` 守护进程：`matthew@seymour:~$ sudo /etc/inetd/openbd-inetd restart`

接下来，启动 X 会话，运行 Firefox，并访问 `http://localhost:901`。你将看到登录提示。输入 root 用户名和密码并点击 OK 按钮。屏幕清空，你会看到 `SWAT` 主页，如图 21.1 所示。

> 提示 你也可以使用 Ubuntu 的 `shares-admin` 客户端配置 Samba。从 X 终端的命令行启动客户端，或选择“系统 - 管理 - 共享文件夹”菜单。

首先，点击 `SWAT` 主页上的 Globals（全局设置）。你会看到一个与图 21.2 显示类似的页面。窗口中有许多选项，但你可以在 Security Options（安全选项）部分的 Hosts Allow（允许的主机）字段中输入一个或多个 IP 地址或子网地址（例如 `192.168.0.` ——注意结尾的点，它允许所有主机访问；在此示例中为 `192.168.0` 子网），从而快速设置局域网局域网主机的访问。如果你需要关于如何格式条目的帮助，请点击字段左侧的 Help（帮助）链接。将出现一个带有相关信息的网页。

# 让 Samba 运行起来

![](img/71b571561538b2a14c3bd347f4fcb569_482_0.png)

欢迎来到 SWAT！

请使用上述按钮之一选择配置操作

# Samba 文档

- 守护进程 (Daemons)

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 名称服务器

  - `winbind` - windbind 守护进程

- 配置文件 (Configuration Files)

  - `smb.conf` - Samba 主配置文件

  - `hosts` - NetBIOS 主机文件

  - `compound` - Samba 密码文件

- 管理工具 (Administrative Utilities)

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

![](img/71b571561538b2a14c3bd347f4fcb569_482_1.png)

# 全局参数 (Global Parameters)

| 当前视图 | 全局参数 |

| :--- | :--- |

| 全局参数 | 高级 (Advanced) |

| 帮助 (Help) | 重置 (Reset) |

| 帮助 (Help) | netbios |

| 帮助 (Help) | realm |

图 21.1 你可以使用 SWAT 轻松地配置和管理 Samba。

# Samba 文档

- 守护进程

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 名称服务器

  - `winbind` - windbind 守护进程

- 配置文件

  - `smb.conf` - Samba 主配置文件

  - `hosts` - NetBIOS 主机文件

  - `compound` - Samba 密码文件

- 管理工具

欢迎来到 SWAT！

请使用上述按钮之一选择配置操作

# Samba 文档

- 守护进程

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 名称服务器

  - `winbind` - windbind 守护进程

- 配置文件

  - `smb.conf` - Samba 主配置文件

  - `hosts` - NetBIOS 主机文件

  - `compound` - Samba 密码文件

- 管理工具

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

# 全局参数

| 当前视图 | 全局参数 |

| :--- | :--- |

| 全局参数 | 高级 (Advanced) |

| 帮助 (Help) | 重置 (Reset) |

| 帮助 (Help) | netbios |

| 帮助 (Help) | realm |

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

# Samba 文档

- 守护进程

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 名称服务器

  - `winbind` - windbind 守护进程

- 配置文件

  - `smb.conf` - Samba 主配置文件

  - `hosts` - NetBIOS 主机文件

  - `compound` - Samba 密码文件

- 管理工具

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

# 21.2

![](img/71b571561538b2a14c3bd347f4fcb569_482_1.png)

# 21.3

# 第21章 共享文件和打印机

# 21.1 共享文件和打印机

![](img/71b571561538b2a14c3bd347f4fcb569_483_0.png)

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

欢迎来到 SWAT！

请使用上述按钮之一选择配置操作

# Samba 文档

- 守护进程

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 名称服务器

  - `winbind` - windbind 守护进程

- 配置文件

  - `smb.conf` - Samba 主配置文件

  - `hosts` - NetBIOS 主机文件

  - `compound` - Samba 密码文件

- 管理工具

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

# 全局参数

| 当前视图 | 全局参数 |

| :--- | :--- |

| 全局参数 | 高级 (Advanced) |

| 帮助 (Help) | 重置 (Reset) |

| 帮助 (Help) | netbios |

| 帮助 (Help) | realm |

# 21.4

![](img/71b571561538b2a14c3bd347f4fcb569_484_0.png)

# 21.4

# 21.1.1

欢迎来到 SWAT！

请使用上述按钮之一选择配置操作

# Samba 文档

- 守护进程

  - `smbd` - SMB 守护进程

  - `nmbd` - NetBIOS 名称服务器

  - `winbind` - windbind 守护进程

- 配置文件

  - `smb.conf` - Samba 主配置文件

  - `hosts` - NetBIOS 主机文件

  - `compound` - Samba 密码文件

- 管理工具

图 21.1 你可以使用 SWAT 轻松地配置和管理系统上的 Samba。

# 21.1.2

# 21.1.3

# 21.1.4

# 21.1.5

# 21.1.6

# 21.1.7

# 21.1.8

# 21.1.9

# 21.1.10

# 21.1.11

# 21.1.12

# 21.1.13

# 21.1.14

# 21.1.15

# 21.1.16

# 21.1.17

# 21.1.18

# 21.1.19

# 21.1.20

# 21.1.21

# 21.1.22

# 21.1.23

# 21.1.24

# 21.1.25

# 21.1.26

# 21.1.27

# 21.1.28

# 21.1.29

# 21.1.30

# 21.1.31

# 21.1.32

# 21.1.33

# 21.1.34

# 21.1.35

# 21.1.36

# 21.1.37

# 21.1.38

# 21.1.39

# 21.1.40

# 21.1.41

# 21.1.42

# 21.1.43

# 21.1.44

# 21.1.45

# 21.1.46

# 21.1.47

# 21.1.48

# 21.1.49

# 21.1.50

# 454 第 21 章 共享文件和打印机

世界各地的办公室都从打印服务器和共享打印机中受益。这是一件简单的事情，即使是在小规模的环境下，也能带来真正的生产力效益。

## 创建网络打印机

设置远程打印服务涉及配置打印服务器，然后在网络中的一台或多台计算机上创建远程条目。本节介绍了一种从一个 Linux 工作站向局域网内的另一台 Linux 计算机打印的快速方法。你还将学习使用 Samba 及其工具进行 SMB 打印。最后，本节讨论了如何配置网络连接打印机并将其用于单份或多个文档。

## 在局域网上启用网络打印

如果连接打印机的计算机正在运行 Ubuntu 且你想为系统设置打印功能，请使用 `system-config-printer` 创建新打印机，该程序位于“系统 -> 管理 -> 打印”菜单中。

首先，按照第 1 章“安装 Ubuntu 和安装后配置”中所述，将你拥有的任何打印机安装到服务器。（点击“添加”并等待片刻，打印机可能会被检测到；这非常简单，你不需要查阅其他章节中的内容。）

接下来，打开“服务器 -> 设置”，启用“发布连接到此系统的共享打印机”。点击“确定”。右键点击任何打印机图标并选择“共享”。这样完成了。大多数用户将需要本节其余部分的信息，即使是为了通过 Web 界面访问通用 UNIX 打印系统 `CUPS`。

若要启用共享，请编辑你的 `/etc/cups/cupsd.conf` 文件。找到以 `<Location />` 开头的部分并将其修改如下：

```
<Location />
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
Allow From 192.168.0.*
</Location>
```

这告诉 `CUPS` 在网络 `192.168.0.*` 上共享你的打印机（例如）。确保将此更改以匹配你的网络设置。

接下来，你需要在同一个文件中查找以以下内容开头的部分：

`Listen localhost:631`

将其修改为：

```
Listen 631
```

这告诉 `CUPS` 监听端口 631 以接收任何打印机请求。

## 使用 Ubuntu 进行网络和远程打印

### 会话消息块打印

打印到 SMB 打印机需要 Samba 以及它的工具（如 `smclient` 和相关的 `smbprint` 打印过滤器）。你可以使用 Ubuntu 自带的 Samba 软件打印到 Windows 网络上的共享打印机，或将连接到系统的打印机设置为 SMB 打印机。本节描述了如何使用 Samba 创建本地打印机条目以打印到远程打印机。

通常你在 Windows 操作系统下通过控制面板中的“网络设备”配置设置来设置 SMB 或共享打印机。启用打印共享后，重启计算机。在“我的电脑”的“打印机”文件夹中，右键点击你想共享的打印机名称或图标，并在弹出菜单中选择“共享”。设置“共享为”项目，然后输入一个描述性名称（例如 HP2100）和密码。

在运行 Linux 时，你必须输入名称和密码来配置打印机。你还需要知道打印机的组名、IP 地址和打印机名称，并准备好用户名和密码。要找到这些信息，请选择“开始 -> 设置 -> 打印机”，然后在“打印机”窗口中右键点击共享打印机的列表。从弹出窗口中选择“属性”。

你可以通过编辑 `smb.conf` 文件来使用 `CUPS` 配置 Samba 使用你的打印机。在 `[global]` 部分中，如果还没有这些行，请输入以下内容：

```
load printers = yes
printing = cups
printcap name = cups
```

这告诉 Samba 由 `CUPS` 提供打印服务。接下来，你需要在 `smb.conf` 文件的末尾创建一个新部分，如下：
