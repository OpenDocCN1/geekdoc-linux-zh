
## `automount`：按需挂载目录层次结构

在分布式计算环境中，当您登录网络上的任何系统时，您的所有文件——包括启动脚本——都可以访问。所有系统通常也能够挂载所有服务器上的所有目录层次结构：无论您登录哪个系统，您的主目录都在等待您。

例如，假设 `/home/zach` 是一个按需挂载的远程目录层次结构。当 Zach 登录或当您发出命令 `ls /home/zach` 时，`autofs` 开始工作：它在 `/etc/auto.misc` 映射中查找，发现 `/home/zach` 是一个键，表示要挂载 `plum:/home/zach`，然后挂载远程目录层次结构。一旦目录层次结构被挂载，`ls` 就会显示该目录中的文件列表。

`automount` 映射可以存储在 NFS 和 LDAP 服务器上，也可以存储在本地文件系统中。除非您更改 `/etc/nsswitch.conf` 文件中的 `automount` 条目（第 495 页），否则 `automount` 守护程序将把映射视为本地系统上的文件进行查找。

### 先决条件

安装以下软件包：

- `autofs`

运行 `systemctl` 使 `autofs` 服务（`automount` 守护程序）在系统每次进入多用户模式时启动，然后启动 `autofs` 服务。使用 `systemctl status` 命令确保服务正在运行。

```
# systemctl enable autofs.service
# systemctl start autofs.service
```

修改 `autofs` 配置文件后，再次给出第二个命令，将 `start` 替换为 `restart` 以使 `autofs` 重新读取这些文件。

## `autofs`：自动挂载的目录层次结构

`autofs` 目录层次结构与其他目录层次结构类似，但在需要之前保持未挂载状态，届时系统会自动挂载它（*按需挂载*）。当不再需要 `autofs` 目录层次结构时，系统会将其卸载——默认情况下，在五分钟不活动之后。自动挂载的目录层次结构是以一致方式管理大量系统的重要组成部分。`automount` 守护程序在安装包含大量服务器或大量目录层次结构时特别有用。它还有助于消除服务器之间的依赖关系（下文）。

当启动使用传统基于 fstab 挂载且 NFS 服务器宕机的系统时，由于等待服务器超时，系统可能需要很长时间才能启动。同样，当有两个服务器，每个都从另一个挂载目录层次结构，并且两个系统都宕机时，在启动过程中，当每个系统都试图从另一个系统挂载目录层次结构时，两个系统都可能挂起。这种情况称为 *服务器间依赖*。`automount` 功能通过仅在进程尝试访问目录层次结构时才从另一个系统挂载它，从而避免了这些问题。

- **服务器间依赖**

当进程尝试访问未挂载的 `autofs` 目录层次结构内的文件之一时，内核通知 `automount` 守护程序，该守护程序随后挂载目录层次结构。您必须给出一个访问 `autofs` 挂载点（在这种情况下为 `/home/zach`）的命令，例如 `cd /home/zach`，以创建促使 `automount` 挂载 `autofs` 目录层次结构的请求；只有在那时，系统才能显示或使用 `autofs` 目录层次结构。在您发出此 `cd` 命令之前，zach 不会出现在 `/home` 中。

控制 `automount` 行为的主要文件是 `/etc/auto.master`。此文件中的每一行描述一个挂载点，并引用指定要挂载在挂载点上的目录的 `autofs` 映射。一个简单的例子如下：

```
$ cat /etc/auto.master
/-      /etc/auto.misc --timeout=60
/plum   /etc/auto.plum
```

- **挂载点**

`auto.master` 文件有三列。第一列指定 `autofs` 挂载点的父目录——即要挂载 `autofs` 目录层次结构的位置。第一列中的 `/-` 表示挂载点是根目录。

- **映射文件**

第二列指定称为 *映射文件* 的文件，该文件存储补充配置信息。可选的第三列保存 `autofs` 映射条目的选项。在上面的例子中，第一行将超时时间（目录未使用时保持挂载的时间长度）设置为 60 秒；默认超时时间是 600 秒。您可以在 `/etc/sysconfig/autofs` 中更改 `autofs` 的默认值。

虽然映射文件可以有任何名称，但其中一个传统上命名为 `auto.misc`。以下是前一个 `auto.master` 文件中指定的两个映射文件：

```
$ cat /etc/auto.misc
/music        -fstype=ext4     :/dev/mapper/fedora-music
/home/zach    -fstype=nfs4    plum:/home/zach

$ cat /etc/auto.plum
public        -fstype=nfs4    plum:/home/public
```

| 类型 | 描述 |
| :--- | :--- |
| 相对挂载点 | 映射文件的第一列保存绝对或相对 autofs 挂载点。出现在 auto.master 第一列中除 / 以外的路径名指定了相对 autofs 挂载点。相对挂载点将附加到 auto.master 第一列中对应的 autofs 挂载点。在此例中，public（来自 auto.plum）附加到 /plum（来自 auto.master）形成 /plum/public。 |
| 绝对挂载点 | 出现在 auto.master 第一列中的 / 指定了绝对 autofs 挂载点。在此例中，auto.master 为 auto.misc 映射文件指定了 / 作为挂载点，因此该映射文件中指定的挂载点是绝对的，并完全在 auto.misc 映射文件中指定。auto.misc 文件指定了 autofs 挂载点 /music 和 /home/zach。 |

第二列保存 autofs 选项，第三列显示要挂载的服务器和目录层次结构。

`auto.misc` 文件指定了本地文件系统（`/dev/mapper/vg_guava-music`；一个 LV（第 44 页））和远程 NFS 目录（`plum:/home/zach`）。您可以通过冒号前没有系统名称以及通常的 ext4 文件系统类型来识别本地目录层次结构。远程目录层次结构文件系统的冒号前出现系统名称，且文件系统类型始终为 nfs4。

在新的设置能够工作之前，您必须重启 `autofs` 服务（第 821 页）。此过程会在必要时创建保存挂载点的目录。

以下示例从 `automount` 守护程序（`autofs` 服务）未运行开始。第一个 `ls` 命令显示 `/music` 和 `/plum` 目录是空的。下一条命令以 root 权限运行，启动 `autofs` 服务。现在当您列出 `/music` 时，`autofs` 会挂载它，`ls` 显示其内容。`/plum` 的列表显示为空：它不是一个 `autofs` 挂载点。

```bash
$ ls /music /plum
/music:
/plum:

$ su -c 'systemctl start autofs.service'

$ ls /music /plum
/music:
lost+found mp3 ogg
/plum:

$ ls /plum/public
memos personal
$ ls /plum
public
```

当您给出 `ls` 命令并指定挂载点（`/plum/public`）时，`automount` 会挂载它，`ls` 显示其内容。一旦 public 挂载在 `/plum` 上，`ls /plum` 显示 public 目录已就位。

# 章节总结

NFS 允许服务器在异构网络上与客户端系统共享选定的本地目录层次结构，从而减少存储需求和管理开销。NFS 定义了一种客户端/服务器关系，其中服务器提供目录层次结构，客户端可以挂载这些目录层次结构。

在服务器上，`/etc/exports` 文件列出了系统导出的目录层次结构。`exports` 文件中的每一行都指定了一个目录层次结构以及允许挂载它的客户端系统，并包含针对每个客户端的选项（如只读、读写等）。执行 `exports -r` 命令会促使 NFS 重新读取此文件。

从客户端来看，`mount` 命令用于挂载已导出的 NFS 目录层次结构。或者，你可以将条目放入 `/etc/fstab`，以便系统在挂载本地文件系统时自动挂载该目录层次结构。

自动挂载的目录层次结构有助于以一致的方式管理包含许多服务器和目录层次结构的大型系统组，并有助于消除服务器之间的依赖关系。`automount` 守护进程会在需要时自动挂载 `autofs` 目录层次结构，并在不再需要时将其卸载。

## 练习

- 1. 使用 NFS 的三个理由是什么？

- 2. 你会给出什么命令来在本地系统上挂载位于名为 `plum` 的文件服务器上的 `/home` 目录层次结构？假设该已挂载的目录层次结构在本地系统上显示为 `plum:/home`。如果该目录层次结构位于 IP 地址为 192.168.1.1 的文件服务器上，你会如何挂载它？你如何卸载 `/home`？

- 3. 你会如何列出本地客户端 `guava` 可以挂载的远程服务器 `plum` 上的挂载点？

- 4. 哪条命令行可以列出当前已挂载的 NFS 目录层次结构？

- 5. `/etc/fstab` 文件的作用是什么？

- 6. 从服务器端来看，你如何允许 example.com 中的任何系统对 `/opt` 目录进行只读访问？

## 高级练习

- 7. 什么时候禁用属性缓存是个好主意？

- 8. 描述 `/etc/exports` 中 `root_squash` 和 `all_squash` 选项之间的区别。

- 9. 为什么 `/etc/exports` 中的 `secure` 选项实际上不提供任何安全性？

- 10. 一些无盘工作站使用 NFS 作为交换空间。这种方法为什么有用？缺点是什么？

- 11. NFS 将客户端上的用户映射到服务器上的用户。解释为什么这种映射是一种安全风险。

- 12. `mount nosuid` 选项的作用是什么？为什么你希望使用此选项？

# 23 SAMBA：Linux 和 Windows 的文件和打印机共享

- **在本章中**

  - Samba 简介 . . . . . . . . . . . . . . . . 828

  - `smbpasswd` 和 `pdbedit`：处理 Samba 用户和密码 . . . . . . . . . . . . 831

  - 运行 Samba 客户端 . . . . . . . . . . . . 832

  - 设置 Samba 服务器 . . . . . . . . . . . 836

  - JumpStart：使用 `system-config-samba` 配置 Samba 服务器（Fedora） . . . 837

  - `smb.conf`：手动配置 Samba 服务器 . . . . . . . . . . . . 839

  - 故障排除 . . . . . . . . . . . . . . . . . 846

### 学习目标

阅读完本章后，你应该能够：

- ▶ 描述 Samba 的用途、历史及组件

- ▶ 列出 Samba 服务器的功能

- ▶ 使用各种 Samba 客户端工具

- ▶ 描述 Samba 认证方法

- ▶ 为本地账户配置 Samba 共享

- ▶ 排除 Samba 连接的故障

Samba 是一套程序，使类 UNIX 操作系统（包括 Linux、Solaris、FreeBSD 和 Mac OS X）能够作为服务器和客户端与其他操作系统（如 OS/2 和 Windows）共享文件和打印机。

作为服务器，Samba 将 Linux 文件和打印机与 Windows 系统共享。作为客户端，Samba 使 Linux 用户能够访问 Windows 系统上的文件和打印机。其在不同操作系统间共享文件的能力使 Samba 成为异构计算环境中的理想工具。

有关使用 CUPS 和 Samba 在 Windows 机器上进行打印的信息，请参阅第 574 页和第 576 页。

# Samba 简介

本章首先列出 Samba 工具，然后提供一些关于 Samba 的基本信息。关于 Samba 客户端的部分解释了如何使用 Samba 处理远程系统上的文件和打印机。下一部分描述了配置 Samba 服务器的三种方式。首先，JumpStart 部分解释了如何使用 `system-config-samba` GUI（仅限 Fedora）设置 Samba 服务器。接下来的部分涉及使用文本编辑器编辑 Samba 配置文件。最后一部分“故障排除”（第 846 页）提供了一些建议，当 Samba 无法正常工作时应怎么做。

表 23-1 列出了组成 Samba 程序套件的某些实用程序和守护进程。完整列表请参见 `samba` 手册页。

**表 23-1** Samba 实用程序和守护进程

| 实用程序或守护进程 | 功能 |
| :--- | :--- |
| `net` | 此实用程序的语法与 DOS 的 `net` 命令相同，随着时间推移，最终将取代 `smbpasswd` 等其他 Samba 实用程序。 |
| `nmbd` | `NetBIOS`（第 1262 页）名称服务器程序，默认以守护进程方式运行。为 Samba 客户端提供 NetBIOS over IP 命名服务。还为远程系统上的 Samba 共享提供浏览支持。 |
| `nmblookup` | 查询 `NetBIOS`（第 1262 页）名称；参见第 847 页。 |
| `pdbedit` | 维护 Samba 用户数据库（第 831 页）。 |
| `smbclient` | 显示 Samba 服务器（如 Windows 机器）上的共享；使用类似 ftp 的命令（第 833 页）。 |
| `smbd` | Samba 程序，默认以守护进程方式运行。为 Samba 和 Windows 客户端提供文件和打印服务。 |
| `smbpasswd` | 更改 Samba 和 Windows NT 服务器上的 Windows NT 密码哈希值（第 831 页）。 |
| `smbstatus` | 显示当前 `smbd` 连接的信息。 |
| `smtar` | 从 Samba 服务器备份和恢复数据；类似于 tar。 |
| `smbtree` | 显示可用共享的层次结构图（第 832 页）。 |
| `testparm` | 检查 `smb.conf` 文件的语法（第 846 页）。 |

## 更多信息

- **Web** Samba: www.samba.org（邮件列表、文档、下载等）

- **HOWTO** 非官方 Samba HOWTO: www.oregontechsupport.com/samba.

# 注释

- **客户端防火墙** Samba *客户端*通常使用 UDP 端口 137 和 138。如果客户端正在运行防火墙或位于防火墙之后，你需要打开这些端口。输入以下命令以在每次系统启动时（永久性！）和运行中的系统上打开端口；有关 `firewall-cmd` 的信息，请参见第 906 页。

```bash
# firewall-cmd --add-port=137/udp
# firewall-cmd --permanent --add-port=137/udp
# firewall-cmd --add-port=138/udp
# firewall-cmd --permanent --add-port=138/udp
```

- **共享** 在 Samba 和 Windows 中，导出的目录层次结构被称为 *share*（共享）。

- **映射共享** Samba/Windows 术语 *mapping a share*（映射共享）等同于 Linux 术语 *mounting a directory hierarchy*（挂载目录层次结构）。

- **Samba** *Samba* 的名称源自 *SMB*（第 1273 页），这是 Windows 本地文件和打印机共享协议。另见 *CIFS*（下文）。

- **CIFS** *CIFS*（第 1242 页）是基于 *SMB*（上文）的互联网文件系统协议。术语 *SMB* 和 *CIFS* 可以互换使用。

- **打印** 使用 CUPS 在连接到 Linux 系统的打印机上打印比使用 Samba 从 Windows 打印更容易，且可以更加安全。有关更多信息，请参见第 574 页的“从 Windows 打印”。

- **故障排除** 如果服务器无法正常工作，请参见第 846 页的“故障排除”。

# Samba 用户、用户映射和密码

- **认证** 为了让 Windows 用户访问 Linux 系统上的 Samba 服务，该用户必须提供 Windows 用户名和一个 Samba 密码。在某些情况下，Windows 会为你提供用户名和密码。或者，你可以以 *guest*（来宾；匿名用户；见下一页）用户身份登录。也可以使用其他方法进行认证。例如，Samba 可以使用 *LDAP*（第 1257 页）或 *PAM*（第 476 页）代替默认的密码文件。有关认证方法的更多信息，请参见 Samba 文档。

## Samba 用户、用户映射和密码

Windows 提供的用户名必须与 Linux 用户名相同，或者必须映射到一个 Linux 用户名（见下文“用户映射”）。

Samba 用户必须具有与 Linux 用户相同的名称（用户名必须出现在 `/etc/passwd` 中）。你可以使用 `pdbedit`（第 841 页）来显示 Samba 用户。

默认情况下，在 Fedora/RHEL 系统中，Samba 使用 Samba 密码对用户进行身份验证。在安装后，不存在任何 Samba 密码。你可以使用 `smbpasswd`（第 831 页）来管理 Samba 密码。除了 `nobody` 之外的每个 Samba 用户都必须有一个 Samba 密码。更多信息请参阅下一页。
