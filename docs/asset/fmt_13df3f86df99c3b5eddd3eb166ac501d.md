
- 你可以使用 `root_squash` 选项将客户端上 `root` 用户的 ID 码映射到服务器上的 `nfsnobody` 用户。
- 你可以使用 `all-squash` 选项将客户端上的所有 NFS 用户映射到服务器上的 `nfsnobody`。

`/etc/passwd` 文件显示 `nfsnobody` 的 UID 和 GID 为 65534。你可以使用 `ananuid` 和 `anogid` 选项来覆盖这些值。

## NIS 和 NFS

当你使用 NIS (655) 进行用户授权时，用户在两个系统上将自动具有相同的 UID。如果你在大型网络上使用 NFS，使用 LDAP（第 1040 页）或 NIS 等目录服务进行授权是一个好主意。如果没有此类服务，你必须手动同步所有系统上的 `passwd` 文件。

## `root_squash` (`no_root_squash`)

映射来自远程系统 `root` 的请求，使其看起来像是来自本地系统上 `nfsnobody`（非特权用户）的 UID，或者由 `ananuid` 指定。该选项不影响敏感的 UID（如 `asin`）。`no_root_squash` 选项关闭此映射，使得来自 `root` 的请求看起来像是来自 `root`。

## `no_all_squash` (`all_squash`)

不改变向 NFS 服务器发送请求的用户映射。`all-squash` 选项将来自远程系统所有用户（而非 `root`）的请求映射为看起来像是来自本地系统上 `nfsnobody`（非特权用户）的 UID，或者由 `ananuid` 指定。此选项常用于控制对导出的公共 FTP、新闻和其他目录的访问。

`ananuid=un` 和 `anogid=gn` 分别将匿名账户的 UID 或 GID 设置为 `un` 或 `gn`。当在来自 `root_squash` 或 `all_squash` 的指令下，如果 NFS 无法识别传入的 UID 或 GID，它将使用这些账户。

## `showmount`: 显示 NFS 状态信息

在不带任何选项的情况下，`showmount` 工具显示允许挂载本地目录的系统列表。要显示远程系统的信息，请将远程系统的名称作为参数。你通常使用 `showmount` 显示服务器正在导出的目录层次列表。然而，`showmount` 提供的信息可能并不完整，因为它取决于 `mount` 并信任远程服务器报告的准确性。

在以下示例中，`bravo` 和 `grape` 可以挂载本地目录，但你不知道是哪些：

```
# /usr/sbin/showmount
localhost 的主机:
bravo.tcorp.com
grape.tcorp.com
```

如果 `showmount` 显示类似 `RPC: Program not registered` 的错误，说明服务器上没有运行 NFS。请使用 `nfs` init 脚本启动 NFS（第 682 页）。

`-a` 选项告知哪些目录被哪些远程系统挂载。这些信息存储在 `/etc/exports` 中。

```
# /usr/sbin/showmount -a
localhost 上的挂载点:
bravo.tcorp.com/home
grape.tcorp.com/home
```

`-e` 选项显示导出的目录列表。

```
# /usr/sbin/showmount -e
localhost 的导出列表:
/home bravo.tcorp.com,grape.tcorp.com
```

## `exportfs`: 维护导出目录层次列表

`exportfs` 工具维护内核的导出目录层次列表。在不更改 `/etc/exports` 的情况下，`exportfs` 可以向导出目录层次列表添加或删除条目。`exportfs` 命令具有以下格式：

```
/usr/bin/exportfs [options] dir ..
```

其中 `options` 是该目录导出的系统的一个或多个选项名称，`dir` 是正在导出的目录层次的根路径。

如果该命令位于 init 脚本中，系统会在启动时执行它。此命令执行 `/etc/exports` 中的条目，并从 `/var/lib/nfs/stab`（第 684 页）中移除无效条目，`/var/lib/nfs/stab` 会与 `/etc/exports` 同步：

### `exportfs -r`

将 `r` 替换为 `a` 以导出 `/etc/exports` 中的条目。使用 `u` 选项删除导出的目录层次；使用 `ua` 选项删除所有导出的目录层次。

### 选项

- `a`: (all) 导出 `/etc/exports` 中指定的目录层次。此选项不会导出你从 exports 中移除的条目（即它不会从 `/var/lib/nfs/stab` 中移除无效条目）；请使用 `r` 执行此任务。
- `i`: (ignore) 忽略 `/etc/exports`；仅使用命令行指定的内容。
- `o`: (options) 指定选项。你可以按照在 `exports` 文件中相同的方式指定选项。例如，在本地系统执行 `exportfs -i -o ro /home/sam`。
- `r`: (reexport) 重新导出 `/etc/exports` 中的条目，并从 `/var/lib/nfs/stab` 中移除无效条目，以便 `/var/lib/nfs/stab` 与 `/etc/exports` 同步。
- `u`: (unexport) 使导出的层次不再导出。如果在取消时目录层次已挂载，当你尝试从远程系统访问该目录层次时，将看到 `Stale file handle`（失效的文件句柄）消息。
- `v`: (verbose) 详细模式：在导出目录时提供更多信息。

映射文件的第一列包含相对 autofs 挂载点 `sam` 和 `auto`。此挂载点将附加到 `auto.master` 第一列中对应的 autofs 挂载点，从而创建绝对的 autofs 挂载点。在本示例中，`sam`（来自 `auto.misc`）被附加到 `/free1`（来自 `auto.master`），生成 `/free1/sam`。第二列包含选项，第三列显示要挂载的服务器和目录层次结构。此示例显示的是本地驱动器；对于 NFS 挂载设备，远程系统的主机名将出现在冒号之前（例如 `grape:/home/sam`）。

在进行下一步设置工作之前，你必须为挂载点的父目录创建目录（上例中的 `/free1` 和 `/free2`），并使用 `autofs` init 脚本启动（或重启）自动挂载守护进程。以下命令显示已配置和激活的 autofs 挂载点的信息。

```
# /sbin/service autofs status
```

![](img/0f75ae90508d45878c00a5b098fe29d4_941_0.png)

![](img/0f75ae90508d45878c00a5b098fe29d4_941_1.png)

# 章总结

NFS 允许服务器在异构网络上与客户端系统共享本地目录层次结构，减少存储需求和管理开销。NFS 定义了客户端/服务器关系，服务器提供客户端可以挂载的目录层次结构。

在服务器上，`/etc/exports` 文件列出了系统导出的目录层次结构。`exports` 中的每行列出了允许挂载该层次结构的系统，并指定了每个层次结构的选项（`readonly`、`read-write` 等）。向 NFS 执行 `exportfs -r` 命令以重新读取此文件。

从客户端来看，你可以使用 `mount` 命令来挂载导出的 NFS 目录层次结构。或者你可以在 `/etc/fstab` 中添加条目，以便系统在启动时自动挂载该目录层次结构。

自动挂载的目录层次结构有助于一致地管理具有许多服务器和文件系统的大型系统组，并有助于消除服务器与服务器之间的依赖。自动挂载守护进程会自动挂载所需的 autofs 目录层次结构，并在不再需要时将其卸载。

# 练习题

1. 列出使用 NFS 的三个理由。
2. 你会用哪个命令在本地系统挂载位于名为 `bravo` 的文件服务器上的 `/home` 目录层次结构？假设挂载的层次结构在本地系统中显示为 `/bravo.home`。如果该层次结构位于 IP 为 192.168.1.1 的文件服务器，你将如何挂载相同的层次结构？你如何卸载 `/home`？
3. 你如何列出本地系统 `grape` 可以挂载的远程系统 `bravo` 挂载点？
4. 哪个命令行列出当前挂载的 NFS 目录层次结构？
5. `/etc/fstab` 文件的作用是什么？
6. 从服务器如何允许 `example.com` 中的任何系统对 `/opt` 进行只读访问？

# 高级练习题

7. 何时禁用属性缓存是一个好主意？
8. 描述 `/etc/exports` 中 `root_squash` 和 `all_squash` 选项的区别。
9. 为什么 `/etc/exports` 中的 `secure` 选项并没有真正提供任何安全性？
10. 某些无盘工作站使用 NFS 作为交换空间。为什么这很有用？缺点是什么？
11. NFS 将客户端用户映射到服务器上的用户。解释为什么这种映射存在安全风险。
12. `mount nosuid` 选项起什么作用？你为什么想这么做？

# 23. Samba：集成 Linux 和 Windows

| 本章内容 | 页码 |
|---|---|
| 关于 Samba | 697 |
| 快速上手：使用 `system-config-samba` 配置 Samba 服务器 | 699 |
| `swat`：配置 Samba 服务器 | 701 |
| 手动配置 Samba 服务器 | 705 |
| 从 Windows 访问 Linux 共享 | 711 |
| 从 Linux 访问 Windows 共享 | 712 |
| 故障排除 | 714 |

Samba 是一组免费程序，使类 Unix 操作系统（包括 Linux、Solaris、FreeBSD 和 Mac OS X）能够作为服务器和客户端与其他操作系统（如 OS/2 和 Windows）协作。

作为服务器，Samba 与 Windows 系统共享 Linux 文件和打印机。作为客户端，Samba 让 Linux 用户能够访问 Windows 系统上的文件。它跨操作系统共享文件的能力使 Samba 成为异构计算环境中的理想工具。

请参考第 520 页的“与 Windows 集成”获取有关使用 Samba 进行打印的信息。

# 引言

本章首先提供了 Samba 工具列表，随后是一些基础信息。“快速上手”部分讨论了如何使用 `system-config-samba`（一个极简 GUI）设置 Samba 服务器。下一节涵盖了如何手动使用 Samba 服务器，使用文本编辑器手动编辑控制 Samba 的文件。接下来的两节“从 Windows 访问 Linux 共享”（711）和“从 Linux 访问 Windows 共享”（712）解释了如何处理 Linux 和 Windows 文件。本章的最后一节“故障排除”（714）提供了在设置或使用 Samba 遇到问题时的处理建议。

表 23-1 列出了组成 Samba 套件的实用和守护进程。

| 表 23-1. Samba 工具和守护进程 |
|---|---|
| 工具或守护进程 | 功能 |
| `net` | 语法与 DOS 命令相同。 |
| `nmbd` | 默认作为守护进程运行的 NetBIOS 程序。提供命名服务。 |
| `nmblookup` | 执行 NetBIOS 查询。 |
| `smbclient` | 显示 Windows 共享。 |
| `smbd` | 提供 Samba 文件和打印服务。 |
| `smbpasswd` | 修改 Samba 密码。 |
| `smbstatus` | 显示当前 `smbd` 连接的信息。 |
| `smbtree` | 显示可用共享的层次结构。 |
| `swat` | Samba 管理工具。 |
| `testparm` | 检查 `smb.conf`。 |
| `testprns` | 检查打印机。 |

# 关于 Samba

本文介绍了你需要安装的包、关于 Samba 的信息来源以及 Samba 下的用户和密码。

# 前提条件

安装软件包：

- `samba`
- `samba-client`
- `samba-common`
- `system-config-samba`（可选）
- `samba-swat`（可选，但建议安装）

运行 `chconfig` 使系统在进入多用户模式时启动 `smb`：

```
# chconfig smb on
```

启动 `smb`：

```
# /sbin/service smb start
```

如果你想使用 `swat`，请修改 `/etc/xinetd.d/swat`（见 701 页“swat：配置 Samba 服务器”），并重启 `xinetd`：

```
# /sbin/service xinetd restart
```

## 更多信息

# 共享

在 Samba 中，导出的目录层次结构被称为共享（share）。

Samba 名称来源于 SMB，它是 Windows 原生的文件和打印共享协议。

# Samba 用户、用户映射和密码

Windows 用户访问 Samba 服务需要提供 Windows 用户名和 Samba 密码。在某些情况下，Windows 会为你提供用户名和密码。也可以使用其他方法进行验证。例如，Samba 可以使用 LDAP 或 PAM 代替默认密码文件。身份验证方法参考 Samba 文档。

## 用户名

提供的用户名必须与 Linux 用户相同或映射到 Linux 用户。Samba 在 `/etc/samba/smbusers` 中维护用户名。Linux 和 Samba 中用户名相同的用户不需要出现在此文件中，但他们仍然需要 Samba 密码。

当你安装 Samba 时，`smbusers` 有两个条目：

```
$ cat /etc/samba/smbusers
# Unix_name = SMB_name1 SMB_name2 ...
root = guest administrator admin
nobody = guest pocuest smguest
```

Samba 使用密码而非登录密码来身份验证用户。默认情况下，Samba 将密码存储在 `/etc/samba/smbpasswd` 中。在安装 Samba 后，`root` 或 `nobody` 的身份验证将失败，因为安装 Samba 时并没有设置密码：此时 `smbpasswd` 文件不存在。

本节中描述的每种身份验证配置技术都允许你将用户添加到 `smbusers` 或 `smbpasswd` 中。你可以像本节后面讨论的那样，随时使用 `smbpasswd` 来添加和更改 `smbpasswd` 中的密码。

## 注意

当你尝试从 Windows 连接到 Samba 服务器时，Windows 会将你的 Windows 用户名和密码提交给 Samba。如果你的 Windows 用户名与 Linux 用户名相同或匹配，且你的 Windows 和 Samba 密码相同，则你无需输入用户名或密码即可连接到 Samba 服务器。

## 示例

你可以将以下行添加到 `smbusers`，将 Windows 用户名 `sam` 映射到 Linux 用户名 `sls`：

```
sls = sam
```

可以使用以下命令为 `sls` 在 `smbpasswd` 中添加密码：

```bash
# smbpasswd -a sls
New SMB password:
Retype new SMB password:
Added user sls.
```

现在，当 Sam 使用用户名 `sam` 登录 Samba 服务器时，Samba 将 `sam` 映射到 `sls` 并在 `smbpasswd` 中查找 `sls`。假设 Sam 提供了正确的密码，他以 `sls` 的身份登录 Samba 服务器。

## 快速上手：使用 `system-config-samba` 配置 Samba 服务器

`system-config-samba` 工具只能设置 Samba 服务器的基本功能。然而，如果你不熟悉 Samba 并且想要快速一个简单的 Samba 服务器，它是最好的工具。`system-config-samba` 工具执行三个基本职能：配置服务器、配置用户以及设置导出到 Windows 机器的共享（目录层次结构）。

### 提示：备份 `smb.conf`

默认安装时，`/etc/samba/smb.conf` 包含大量内容（第 705 页）。`system-config-samba` 工具会覆盖此文件。在第一次运行该工具之前，请制作 `smb.conf` 的副本以防万一。

要显示 Samba 服务器配置窗口（图 23-1），请在命令行输入 `system-config-samba`。在 KDE 中选择 **Main menu: System > Samba**，或在 Gnome 中选择 **System: Administration > Server Settings > Samba**。

### 图 23-1. Samba 服务器配置窗口

![](img/0f75ae90508d45878c00a5b098fe29d4_952_0.png)

选择 **Menu > Server Settings** 显示服务器设置窗口。基本选项卡如图 23-2 所示。将工作组（workgroup）更改为你 Windows 机器上使用的组。可以根据需要更改服务器描述。点击 **Security** 选项卡并确保身份验证模式（Authentication Mode）设置为 **User**；你不需要指定身份验证服务器或 Kerberos 域（Realm）。如果你正在使用 Samba 用户...

### 图 23-2. 服务器设置窗口，基本选项卡

![](img/0f75ae90508d45878c00a5b098fe29d4_953_0.png)

Samba 用户
