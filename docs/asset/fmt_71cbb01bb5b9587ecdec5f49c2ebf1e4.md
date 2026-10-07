
Samba 是 Fedora 和 Red Hat Linux 系统自带的一个软件包。Samba 允许你通过会话消息块（SMB）协议在网络上共享文件系统和打印机。SMB 是 Windows 操作系统用于共享文件和打印机的协议。虽然你不能总是认为 Windows 客户端安装了 NFS（除非你手动安装它），但 SMB 总是可用的（只需进行少量设置）。

在 Fedora 上，Samba 软件包包含各种守护进程、管理工具、用户工具和配置文件。要进行基础的 Samba 配置，你可以从 Samba 配置窗口开始。该窗口为配置服务器和设置共享目录提供了图形界面。

你最终完成的大部分 Samba 配置位于 `/etc/samba/smb.conf` 文件中。如果你需要访问 Samba 服务器配置窗口无法的功能，可以手动编辑 `/etc/samba/smb.conf`，或使用 SWAT（一个基于 Web 的配置 Samba 的界面）。

守护进程由 `smbd`（SMB 守护进程）和 `nmbd`（NetBIOS 服务器）组成。`smbd` 守护进程使添加到 Linux 系统的文件共享和打印服务对 Windows 客户端可用。该软件包支持的客户端计算机包括：

- Windows 9x
- Windows 2000
- Windows NT
- Windows ME
- Windows XP
- Windows for Workgroups
- MS Client 3.0 for DOS
- OS/2
- Dave for Macintosh Computers
- Samba for Linux

作为 Samba 的管理工具，你有几个 shell 命令可以使用。你可以使用 `testpar` 和 `testprn` 命令检查你的配置文件。`smbstatus` 命令告诉你当前哪些计算机正连接到你的共享资源。使用 `nmblookup` 命令，你可以查询 NetBIOS 节点（在 Samba 中用于标识主机的名称）。

尽管 Samba 使用 NetBIOS 服务与 SMB 客户端共享资源，但底层网络必须配置为 TCP/IP。虽然其他 SMB 主机可以使用 TCP/IP、NetBEUI 和 IPX/SPX 传输数据，但 Samba for Linux 只支持 TCP/IP。消息在主机计算机之间通过 TCP/IP 携带并由 NetBIOS 处理。

## 获取并安装 Samba

要检查 Fedora 系统上是否安装了 Samba，请输入以下：

```bash
# rpm -qa | grep samba
samba-*
system-config-samba
samba-swat-*
samba-common-*
samba-client-*
```

你应该能看到上述五个软件包中的每一个名称，后面跟着版本号（我用星号表示版本号）。虽然 Fedora 的所有安装组都没有包含，但组成 Samba 的软件包分布在 CD #1 和 CD #4 中。要安装 Samba，首先挂载 CD 并运行以下命令：

```bash
## mount /mnt/cdrom
# cd /mnt/cdrom/Fedora/RPMS
# rpm -Uhv samba*
# cd ; umount /mnt/cdrom
```

对另一张 CD 重复此过程。在尝试配置 Samba 之前，请阅读 README 文件（位于 `/usr/share/doc/samba*`）。它提供了关于 SMB 协议和 Samba 的良好概述。

## 配置简单的 Samba 服务器

Samba 服务器配置窗口允许你进行基础的 Samba 配置并识别你想要共享的目录。为了使此过程具有实用意义，我正在设置一种特定的共享环境（如果你有喜好，可以进行修改）。其特征如下：

- 单个局域网：包含多台 Windows 和 Linux 机器。
- 用户安全：任何想要访问的用户必须有密码。
- 加密密码：许多客户端使用加密密码。
- 访客账户：将此字段设置为 guest。

以下步骤描述了如何配置 Samba：

1. 要打开 Samba 配置窗口，点击 File -> Server。
2. 在组框中输入组名，例如 Workgroup。
3. 点击 Security 选项卡。
4. 在 Security 选项卡上填写以下字段：
   - Authentication Mode（身份验证模式）：选择 User 或 Domain。
   - Authentication（身份验证）：此字段仅适用于 User。
   - Encrypt Passwords（加密密码）：选择 Yes 或 No。
5. 要将用户添加为 Samba 用户，选择 Preferences -> Users。
6. 点击 Add User。
7. 为 Create New User 窗口中的字段提供信息：
   - Unix Username（Unix 用户名）：选择 Linux 用户。
   - Windows Username（Windows 用户名）：这是用户提供的用户名。
   - Samba Password（Samba 密码）：输入密码，再次输入。
8. 为每个想要访问共享目录重复上述步骤。
9. 现在你已经为 Samba 服务器配置了默认值，点击 File -> Add Share 添加要共享的目录。
10. 在 Create Samba Share 窗口中填写以下字段：
    - Directory（目录）：输入你想共享的目录名称。
    - Description（描述）：输入你喜欢的描述。
    - Basic Permissions（基本权限）：选择 Read-only（只读）或 Read/Write（读写）。
11. 点击 Access 选项卡，为共享选择以下选项之一：
    - Only access to specific users（仅限特定用户访问）：点击，然后选择哪些用户将允许访问共享目录。

## 第四部分：Fedora 网络与服务器设置

- **允许所有人访问** — 如果你想允许任何人访问此目录，请选择此选项。（所有用户在访问该目录时将拥有分配给该用户的权限。）

点击 OK 后，Samba 将启动且新目录将立即可用。你可以关闭 Samba 服务器配置窗口。

- 13. 尽管 Samba 此时已开始运行，但你可能需要设置 Samba 在每次重启 Linux 时自动启动。要实现此点，请在终端窗口以 root 用户身份输入以下命令：

```bash
chkconfig samba sm
```

你可以对每个想要在网络上开放的目录重复添加 Samba 共享目录的步骤。此时，你可以选择以下任一类操作：

- 详细查看你的 Samba 服务器设置（如在“使用 SWAT 配置 Samba”部分所述），以了解你可能想要如何调整你的 Samba 服务器。
- 尝试从网络上的客户端计算机访问你刚刚创建的共享目录。

如果你无法从局域网（LAN）上的 Windows 计算机或其他 Linux 计算机打开你刚刚配置的共享目录，你可能遇到了以下问题之一：

- 客户端没有提供有效的用户名和密码。
- 客户端没有提供加密密码。

解决这些问题的快速方法是仅使用共享级安全（当然，这会让你从安全性完全抛诸脑后）。另一种解决方案是更新密码，并确保客户端正在使用加密密码（如本章后面“设置 Samba 客户端”部分所述）。

## 使用 SWAT 配置 Samba

Samba Web 管理工具 (SWAT) 是一个用于配置 Samba 的基于 Web 的界面。虽然它不像 Samba 服务器配置窗口那样易用，但它提供了更多调整 Samba 的选项，以及每个选项的帮助描述。

> 警告：SWAT 和 Samba 服务器配置窗口都通过修改 `/etc/samba/sm.conf` 文件来配置 Samba。不同的 GUI 工具可能会覆盖彼此的设置，有时甚至会导致另一个工具无法工作。

通常情况下，在切换 GUI 工具之前，最好为你的文件创建一个备份副本。最终，你应该选择一个工具并坚持使用它。

## 第 18 章：建立文件服务器

### 开启 SWAT 服务

在使用 SWAT 之前，你必须进行一些配置。要设置 SWAT 从浏览器中运行，请遵循以下步骤：

- 1. 要开启 swat 服务，请在终端窗口中以 root 用户身份输入以下命令：
   # `chkconfig swat on`
- 2. 要使 swat 服务的更改生效，请如下所示重启 xinetd 启动脚本：
   # `service xinetd restart`

完成此步骤后，使用下一节介绍的 SWAT 程序来配置 Samba。

### 开始使用 SWAT

你可以通过在本地浏览器中输入以下 URL 来运行 SWAT 程序：

```
http://localhost:901/
```

此时，浏览器将提示你输入用户名和密码。输入 root 用户名和密码。SWAT 窗口将出现，如图 18-5 所示。

![](img/2f5d509ecad466b7feb83ce33450460a_742_0.png)

图 18-5：从浏览器使用 SWAT 管理你的 Samba 配置。

> 提示：与其从本地浏览器运行 SWAT，你可以通过将服务器计算机名称替换 localhost，从网络上的另一台计算机上运行它。（要允许 localhost 外的计算机访问 swat 服务，你必须更改或删除 `/etc/xinetd.d/swat` 文件中的 `only_from = 127.0.0.1` 行并重启 xinetd 服务。）

## 第四部分：Fedora 网络与服务器设置

本节内容描述了如何使用 SWAT 创建你的配置条目（在 `/etc/samba/smb.conf` 中）以及如何处理该配置。

> 警告：每当你使用 GUI 更改纯文本配置文件时（如使用 SWAT 时），你可能会丢失手动输入的一些信息。SWAT 会删除注释行并重新排列其他条目。为了保护你手动进行的更改，在用 SWAT 编辑之前，请为你的 `/etc/samba/smb.conf` 文件创建一个备份副本。

## 在 SWAT 中创建全局 Samba 设置

一组全局设置影响了 Samba 服务器上通常实现文件和打印共享的方式。它们出现在 `/etc/samba/smb.conf` 文件的 `[global]` 标题下。要编辑全局变量，请点击 SWAT 窗口上的 GLOBALS 按钮。

共有七种类型的选项：基础选项、安全选项、日志选项、调整、打印选项、浏览选项和 WINS 选项。查看并修改你的全局 Samba 服务器设置，请点击 GLOBALS 按钮。然后添加以下选项。

> 注意：每个选项都对应 `/etc/samba/sm.conf` 文件中使用的精确参数。你可以参考 smb.conf 手页（输入 `man smb.conf`）来获取关于这些参数的更多信息。

### 基础选项

以下选项与你的 Samba 服务器相关的基本信息有关：

- **workgroup**：与 SMB 主机组关联的工作组名称。默认情况下，该字段的值为 WORKGROUP。
- **realm**：如果你正在使用 kerberos 认证，此值表示要使用的 kerberos 领域（realm）。通常这由提供服务的服务器主机名反映。
- **netbios**: 分配给 Samba 服务器的名称。
- **netbios alias**: 名。
- **server**: 用于标识服务器的字符串。
- **interfaces**: 允许设置多个网络接口。
- **mask**: 掩码的值。

## 第 18 章：建立文件服务器

### 安全选项

在安全选项中，第一个选项（security）是最需要正确设置的。它定义了共享文件的安全类型。以下是你的选项：

- **user**: 文件和打印机最常用的安全类型。它要求用户提供用户名/密码。让其工作的最简单方法是为每个使用服务器的客户端用户提供一个用户账户。
- **share**: 该安全值对于仅打印或提供更公开的文件访问（访客共享）最好。客户端不需要提供有效的用户名和密码即可访问服务器。
- **server**: 从客户端角度来看，这种安全选项与用户安全相同。在服务器安全模式下，用户名/密码将发送到另一个 SMB 服务器进行验证。
- **domain**: 从客户端角度来看，这种安全选项与用户安全相同。此设置仅在 Samba 服务器被添加到 Windows NT 域时有效。

Windows NT 主域控制器或备份域控制器。其实现方式与 Windows NT 服务器执行验证的方式相同。必须仍然设置有效的 Linux 用户账户。

- **encrypted passwords**（加密密码）—— 控制是否可以与客户端协商加密密码。默认为否（no）。为了域安全，此此值必须设置为 Yes（是）。较版本的 Windows NT（4.0 SP3 或更高版本）以及 Windows 98 和 Windows 2000 期望开启加密密码。（有关让客户端使用加密密码的信息，请参见“设置 Samba ”部分。）
- **updated encrypted**（更新加密）—— 允许使用明文密码登录的用户在登录时自动将密码更新为加密密码。通常情况下，此选项是关闭的。当你希望使用明文密码的安装让所有人使用加密密码认证时，可以开启它。这可以避免直接从服务器运行 `smpasswd` 命令的麻烦。在所有人更新完成后，可以关闭此功能。当此选项开启时，encrypted passwords 选项应设置为 no。
- **obey password restrictions**（遵守密码限制）—— 如果你想使用 PAM 进行账户和会话管理，请开启此项（Yes）。即使激活了 PAM，如果加密密码功能开启（encrypted passwords = yes），PAM 也被使用。
- **pam password change**（PAM 密码更改）——指示 Samba 使用 PAM 密码控制标志。如果开启此项（Yes），SMB 客户端将使用 PAM 代替“Password program”中列出的程序来更改 SMB 密码。
- **password program**（密码程序）——指示使用哪个密码程序来更改 Linux 用户密码。默认使用 `/usr/bin/passwd`，并插入当前用户 (%u)。
- **password chat**（密码对话）——设置在 Samba 守护进程 (`smbd`) 和 Linux 程序（默认是 `/usr/bin/passwd`）之间进行的对话，smbd 据此尝试将 SMB 密码与 Linux 用户密码同步。
- **username map**（用户名映射）——这设置用于映射 Samba 名称的文件。默认情况下，这是 `/etc/samba/smusers`。
- **unix password sync**（Unix 密码同步）——开启此项（Yes）后，当更改 SMB 密码时，Samba 会尝试用用户的 SMB 密码更新其 Linux 密码。为了实现这一点，Samba 会以 root 用户身份运行 `passwd` 命令。 默认开启。
- **guest account**（访客账户）——指定访客账户的用户名。当指定服务为 Guest OK 时，将使用此处输入的用户名来访问该服务。该账户通常是 `nobody` 用户。

> **提示**：确保访客账户是一个有效用户。（默认的 nobody 应该已经设置好可以使用。）如果使用无效用户作为访客账户，列出共享资源的 IPC$ 连接将失败。

# 第 18 章：设置文件服务器

- hosts allow（允许主机）——包含允许使用你的计算机 Samba 服务的一个或多个主机列表。默认情况下，任何计算机的用户都可以连接到 Samba 服务器（当然，他们仍然必须提供有效的用户名和密码）。通常，使用此选项允许来自特定计算机（如 10.0.0.1）或计算机网络（如 10.0.0.0）的连接，这些是由 hosts deny 选项排除的。
- hosts deny（拒绝主机）——包含一个或多个不允许用户使用你的计算机 Samba 服务的主机列表。你可以将此选项设置得相当严格，然后添加你想要使用 Samba 服务器的主机和网络。默认情况下不拒绝任何主机。

# 日志选项

以下选项有助于定义如何在你的 Samba 服务器上进行记录：

- log level（日志级别）——设置记录 Samba 活动时的调试级别。将级别从默认值 (0) 提高以记录更多的 Samba 活动。
- log file（日志文件）——定义 Samba 日志文件的位置。默认情况下，Samba 日志文件包含在 `/var/log/samba`（文件名为 nmbd、log.smbd 和 smb.log）。在此选项中，%m 被替换为 sm，以便将 smb 日志文件设置为 `/var/log/samba/smb.log`。
- max log size（最大日志大小）——设置日志文件消耗的最大空间（以 KB 为单位）。默认情况下，该值为 0（无限制）。

# 分配访客账户

Samba 总是将 Linux 系统上有效用户的权限级别分配给使用服务器的客户端。在共享安全的情况下，该用户将分分配一个账户（默认是 *nobody* 账户）。

如果未设置 guest account 值，Samba 将通过一套相当复杂的规则来确定使用哪个用户账户。结果是，很难保证在每情况下将分配哪些用户权限。这就是为什么如果你想为你的 Samba 提供更具体的用户访问，建议使用用户安全。

# 调优选项

Socket Options（套接字选项）允许向 Samba 用于通信的协议传递选项。默认设置了以下选项：TCP_NODELAY、SO_RCBUF=8192 和 SO_SNDBUF=8192。第一个选项禁用了 Nagle 算法，该算法用于管理 TCP/IP 数据包的传输。另外两个选项分别将套字接收缓冲区和发送缓冲区的大小设置为 8192。设置这些选项是为了提高性能（据报道，比不设置这些选项快 10 倍）。通常情况下，你不应该更改这些选项。

# 打印选项

printing 选项用于定义打印机状态呈现的方式。对于 Fedora，其值为 cups。你可以使用其他操作系统，如 sysv、AIX、hpux、Berkeley (bsd)、lprng 和 Samba。这对于提供服务特别有用。

# 浏览选项
