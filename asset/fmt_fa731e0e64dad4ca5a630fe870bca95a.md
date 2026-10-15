
### 在 Fedora 系统上，设置 autofofs 服务在每次启动系统时自动重启：

```
# chkconfig autofofs on
```

# 设置 Linux 服务器

信不信由，这就是你所需要做的一切。如果你到想要共享目录的 NFS 服务器有网络连接，请尝试访问共享的 NFS 目录。例如，如果你知道网络上名为 `shuttle` 的计算机正在共享 `/usr/local/share` 目录，你可以执行以下操作：

```
$ cd /net/shuttle
```

如果该目录下有任何供你访问的共享目录，你就可以成功切换到该目录。

你也可以输入以下内容：

```
$ ls
$ usr
```

你应该能看到 `usr` 目录是共享目录路径的一部分。如果来自其他顶层目录（如 `/var` 或 `/tmp`）的共享目录，你也会看到它们。当然，是否能看到其中任何目录取决于服务器上的安全设置。

也请尝试进入挂载的共享目录。例如：

```
$ cd /net/shuttle/usr/local/share
$ ls
info man music television
```

此时，`ls` 命令应该会显示名为 `shuttle` 的计算机上 `/usr/local/share` 目录的内容。你对这些内容的操作取决于服务器为共享进行的配置。

在你实际尝试使用它们（例如切换到网络挂载的目录）之前，看不到任何文件或目录，这可能会让你感到有些困惑。例如，`ls` 命令在目录挂载之前不会在网络挂载的目录下显示任何内容，这可能导致有时“它在那里，有时又没印象”的感觉。只需切换到网络挂载的目录，或访问此类目录上的文件，其余部分就会处理好。

# 卸载 NFS 文件系统

在 NFS 文件系统挂载后，卸载它非常简单。你使用 `umount` 命令，并配合本地挂载点或远程系统名称。例如，这里是从本地目录 `/mnt/map` 挂载 `maple:/tmp` 的两种方法：

```
$ mount maple:/tmp
$ umount /mnt/map
```

这两种形式均有效。如果 `maple:/tmp` 是自动挂载的（来自 `/etc/fstab` 中的列表条目），则该目录将在下次启动 Linux 时被重新挂载。如果它是临时挂载（或在 `/etc/fstab` 中列为 `noauto`），则它在启动时不会重新挂载。

# 运行文件服务器

## 提示

命令是 `umount`，而不是 `unmount`。这很容易记错。

当你尝试卸载文件系统时收到“device is busy”（设备忙）的消息，意味着卸载失败，因为该文件系统正在被访问。最可能的是 NFS 文件系统中的某个目录是你 shell 的当前目录（或你系统中其他人的 shell）。另一种可能性是某个命令打开了 NFS 文件系统中的文件（例如文本编辑器）。检查你的终端窗口和其他 shell，如果是的话，请 `cd` 出该目录。

# 使用 NFS 的其他操作

命令是 `umount`，而不是 `unmount`。这很容易记错。

最可能的是 NFS 文件系统中的某个目录是你的 shell 的当前目录（或你系统中其他人的 shell）。另一种可能性是某个命令打开了 NFS 文件系统中的文件（例如文本编辑器）。检查你的终端窗口和其他 shell，如果是的话，请 `cd` 出该目录。

如果文件系统未挂载，你无法访问它。如果已挂载，你就可以正常访问。

# 设置 Linux 服务器

如果你仅与 Linux 和其他 Unix 系统工作，NFS 可能是你共享文件的最佳选择。你可以在 Windows 上挂载 NFS 共享，但前提是有 NFS 客户端软件，Windows 默认并不提供。如果你的网络主要由微软计算机组成或是系统的组合，你可能希望考虑 Samba 进行文件共享。

# 设置 Samba 文件服务器

Samba 是一个随 Ubuntu、Fedora 和红帽 Linux 系统以及许多其他 Linux 系统提供的软件包。（如果你的发行版未包含，你可以从 `samba.org` 获取 Samba 包。）Samba 允许你在使用服务器消息块 (`SMB`) 或通用文件系统 (`CIFS`) 协议的网络计算机上共享文件和打印机。`SMB` 是 Windows 操作系统交付的用于文件和打印机的协议。`CIFS` 是一种基于 `SMB` 的开放跨平台协议。

> 在 Windows 文件和打印机共享中，`SMB` 有时被称为 `CIFS`（通用文件系统），它是基于 `SMB` 的 Internet 标准网络系统定义，或者是 `NetBIOS`（它是原始的 `SMB` 协议）。

Samba 软件包包含各种守护进程、管理工具、用户工具和配置文件。要进行基础 Samba 配置，请从 Samba 服务器配置窗口开始，它提供了一个图形化界面来配置服务器并设置共享目录。

## 运行文件服务器

- OS/2
- 适用于 Macintosh 电脑的
- Mac OS X
- 适用于 Linux 的 Samba

> Mac OS X Server 自带 Samba，因此可以使用 Macintosh 系统作为服务器。然而，本章将讨论如何使用 Linux 作为服务器。你可以拥有 Macintosh、Windows 或 Linux 客户端计算机。此外，Mac OS X 同时配备了用于 Samba 的客户端和服务器软件。

作为 Samba 的管理工具，你有几个 shell 命令可以使用：`testparm` 和 `testprns`，你可以用它们来检查配置文件；`mbstatus`，它可以告诉你哪些计算机当前连接到你的共享资源；以及 `nmblookup` 命令，可以用它查询计算机。

Samba 使用 NetBIOS 服务与 SMB 客户端共享资源，底层网络必须配置为 TCP/IP。其他 SMB 主机使用 TCP/IP、NetBEUI 和 IPX/SPX 传输数据，Linux 版 Samba 仅支持 TCP/IP。消息在主机之间通过 TCP/IP 传输，然后由 NetBIOS 处理。

### 获取和安装 Samba

你可以根据你的 Linux 发行版通过不同的方式获取 Samba 软件。以下是几个示例：

- Ubuntu 和 Debian —— 在 Ubuntu 或 Debian 中使用 Samba，必须使用 `apt-get` 安装 `samba` 和 `smbclient` 包。然后运行 `/etc/init.d` 目录下的相应脚本来启动 Samba 服务，如下：

```
# apt-get install samba-common smbclient
# /etc/init.d/samba start
```

- Gentoo —— 使用 Gentoo，你必须在内核中配置 `net-fs` 支持以使用 Samba 功能。安装 `net-fs` 包 (`emerge net-fs`) 应该可以获得所需的包。要启动服务，运行 `rc-update` 并立即启动服务：

```
# emerge samba
# rc update add samba default
# /etc/init.d/samba start
```

- Fedora 和 Red Hat Linux 系统 —— 你需要安装 `samba`、`samba-client`、`samba-common` 以及可选的 `system-config-samba` 和 `samba-swat` 包在 Fedora 中使用 Samba。然后你可以使用 `service` 和 `chkconfig` 命令启动 Samba —— 如下：

```
# service sm start
# chkconfig sm on
```

## 第四部分 设置 Linux 服务器

在大多数使用 Samba 的 Linux 系统上，命令和配置文件是相同的。Samba 项目本身带有一个基于 Web 的界面，用于管理 Samba 的 Samba Web 管理工具 (`SWAT`)。对于第一次设置 Samba 的人来说，`SWAT` 是让其运行起来的好方法。

> 注意：如果你的 Linux 安装中没有可用的 Samba 文档，请查阅 Samba 项目主页（`www.samba.org`）上的文档。此外，检查包含 SWAT 的详尽帮助信息。

### 使用 SWAT 配置 Samba

除了提供丰富的 Samba 接口外，`SWAT` 还带有一个出色的帮助功能。如果你需要从另一台计算机管理 Samba，可以配置 `SWAT` 远程访问，并通过管理员登录和密码进行安全保护。

#### 开启 SWAT 服务

在使用 `SWAT` 之前，你必须进行一些配置。要做的第一件事是开启 `SWAT` 服务，不同的 Linux 发行版操作方法不同。

以下是在 Fedora 和 Red Hat Linux 系统中设置 `SWAT` 的方法：

1. 在终端窗口中以 root 用户身份输入以下内容开启 `SWAT` 服务：

```
# chkconfig swat on
```

2. 通过如下方式重启 `inetd` 启动脚本来应用服务更改：

```
# service inetd restart
```

Debian、Slackware 和 Gentoo 等 Linux 发行版通过 `inetd` 超守护进程开启 `SWAT` 服务。安装 `SWAT` 后，只需删除 `/etc/inetd.conf` 文件中行前的注释字符（以 root 用户身份使用任何文本编辑器）并重启守护进程。以下是 Ubuntu 和 Debian 中该行的示例：

```
swat stream tcp nowait.4 root /usr/sbin/tcpd /usr/sbin/swat
```

当 `SWAT` 服务准备好激活后，重启 `inetd` 守护进程使其重新加载 `inetd.conf` 文件。在 Debian 中，输入 root 用户：

```
# /etc/init.d/inetd restart
```

`init.d` 脚本和 `inetd` 是 Linux 中启动 `SWAT` 服务的两种方式。如果你使用的是 Fedora 或 Debian 以外的 Linux 发行版，请查看 `/etc/inetd.conf` 文件或 `/etc/inetd.d` 目录（Fedora 自动使用），查找 `SWAT` 服务的位置。

完成此步骤后，一个守护进程将在你的网络接口上监听连接到你 `SWAT` 服务的请求。你现在可以使用下一节描述的 `SWAT` 程序来配置 Samba。

#### 开始使用 SWAT

你可以通过在本地浏览器输入以下 URL 来运行 `SWAT` 程序：

```
http://localhost:901/
```

当浏览器提示时，输入 root 用户名和密码。出现 `SWAT` 窗口（如图 16-2）。

图 16-2

从你的浏览器中使用 `SWAT` 管理你的 Samba 配置。

欢迎使用 `SWAT`！

请使用上方按钮之一选择一个配置操作

Samba 文档

- `smbd` - SMB 守护进程
- `nmbd` - NetBIOS 名称服务器
- `winbind` - winbind 守护进程
- 配置文件
  - `smb.conf` - 主配置
  - `lmhosts` - NetBIOS 

### 设置 Linux 服务器

你不需要从本地浏览器运行 `SWAT`，可以通过将 `localhost` 替换为服务器名称，从另一台计算机上运行它。（要允许 localhost 以外的计算机访问 Fedora 服务，必须在 inetd 文件中更改 `only_from = 127.0.0.1`。）这在 Ubuntu 系统中不需要。

后续章节将解释如何使用 `SWAT` 配置你的条目。每当你手动进行更改时，在编辑前请备份你的 `/etc/samba/smb.conf`。

#### 在 SWAT 中创建全局设置

一组全局设置影响服务器的文件和打印共享。这些设置出现在 `/etc/samba/smb.conf` 文件的 `[global]` 头部。要查看和编辑全局变量，点击 `SWAT` 窗口上的 `GLOBALS` 按钮。

有多种类型可用：基础、安全、日志、调整、打印和 WINS。

每个选项对应 `/etc/samba/smb.conf` 文件中的精确参数。你可以参考 `smb.conf` 手页（输入 `man smb.conf`）获取更多信息。

##### 基础选项

以下选项与你的 Samba 服务器的基本信息相关：

- **Workgroup**：与 SMB主机关联的工作组。此字段的值为 `WORKGROUP`。
- **Realm**：如果你使用 kerberos 认证，此值指示使用的 kerberos 领域。通常由提供服务的的主机名反映。
- **NetBIOS**：分配给此 Samba 服务器的名称。可以使用与 DNS 主机名相同的名称，也可以留空，以防 DNS 主机名自动生成。默认会填充你的主机名。
- **NetBIOS alias**：允许设置一个与 TCP/IP DNS 名称不同的主机计算机引用方式（别名）。
- **Server string**：标识服务器的字符串。此名称出现在打印注释等位置。默认情况下，它显示 Samba 和版本号。
- **Interfaces**：允许设置另外一个网络接口并让 Samba 浏览多个不同的子网。此字段的形式可以是 IP/子网掩码。或者，你可以识别网络接口（例如代表电脑上第一块以太卡的 `eth0`）。例如，一个 C 类网络地址可能显示为：

```
192.168.24.11/255.255.255.0
```

## 运行服务器

### 安全选项

在所有安全选项设置中，第一个（Security，安全）是最重要的。它定义了向客户端计算机访问共享文件系统和打印机时使用的安全类型。（要查看此处描述的某些字段，您需要点击“高级”视图。）

- Security — 设置密码和用户信息如何从客户端计算机传输到 Samba 服务器。如前文所述，正确设置此值至关重要。Samba 2.0 及更高版本的安全默认值（`security=user`）与 Samba 较旧版本的默认值（`security=share`）不同。如果您无法访问服务器，这是一个很好的切入点。以下是您的可选选项：
  - `user` — 用于向 Windows 95/98/2000/NT/XP 客户端共享文件和打印机的常用安全类型。它是当前发布版本 Samba 的默认值。如果用户正在进行大量共享（与主要用打印服务器的 Samba 相比），则此设置是合适的。它要求您在使用服务器之前先提供用户名/密码。获取此方法最简单的方法是为每个使用 Samba 服务器的客户端用户提供一个 Linux 用户账户，通过 Samba 服务器为该用户账户提供的文件权限，与其直接登录 Linux 时提供的基本相同。
  - `guest` — 该安全值最适用于仅共享或提供更具公共性的访问（访客共享）。客户端不需要向服务器提供用户名和密码。然而，用户通常只有访问和更改文件的访客层级权限。本章中的“分配访客账户”侧边栏提供了更多信息。
  - `account` — 从客户端的角度来看，这与 security 相同，因为客户端仍然必须提供用户名/密码组合才能使用 Samba 服务器。区别在于服务器端。使用 `security` 时，用户名/密码会被发送到另一个 SMB 服务器进行验证。如果验证失败，Samba 会尝试使用 `security` 验证客户端。
  - `account` — 从客户端的角度来看，这与 user 账户相同。此设置仅在 Samba 服务器已添加到 Windows 域中（使用 `smbpasswd` 命令）时有效。当客户端在此模式下连接到 Samba 服务器时，其用户名和密码将发送到 Windows NT 主控制器或备份控制器。其实现方式与 Windows 服务器执行验证的方式相同。必须设置 Linux 用户账户。
  - `domain` — 此安全选项允许 Samba 作为 AD 域中的域成员运行。使用此选项必须在 Samba 机器上安装 Kerberos。Samba 还必须加入 AD 域（使用 `net` 工具）。
  - `auth methods` — 设置 Samba 服务器 (`smbd`) 使用的认证方法。大多数情况下的默认值。您可以选择的认证方法包括匿名访问（guest）、通过 winbind 进行中继认证（winbind）、pre-winbind winbind 认证（ntdomain）、基于 netbios 或域名的本地查找（sam），或对信任用户进行远程认证（trustdomain）。

### 设置 Linux 服务器

- **Encrypted passwords** — 控制是否可以与客户端协商加密密码。此项默认开启（Yes）。对于域服务，此值必须为 Yes。较新版本的 Windows NT（4.0 SP3 或更高版本）以及 Windows 98 和 Windows 2000 期望加密密码为开启状态。
- **client channel** — 如果客户端不需要登录通道（yes）、提供通道但不强制执行（auto）或甚至不提供通道（no），请选择此项。
- **server channel** — 如果服务器要求客户端登录通道（yes）、提供通道但不强制执行（auto）或甚至不提供通道（no），请选择此项。如果您将其设置为 no，则必须应用来自 Samba 项目的 Windows XP WinXSP_OrSignReal补丁。
- **map to guest** — 允许您在定义情况下将哪些映射到访客账户（最小权限）。例如，您可以映射无效的用户名（Bad User）、使用错误密码的用户（Bad Password）或具有无效用户 ID（Bad UID）。或者您可以选择不将这些用户映射到访客。
- **Obey PAM restrictions** — 如果您想使用 PAM 进行账户和会话管理，请开启（Yes）。如果激活了加密密码功能（`encrypt passwords = yes`），则不使用 PAM。PAM 代表可插拔认证模块（Pluggable Authentication Modules），用于验证主机计算机和用户。
