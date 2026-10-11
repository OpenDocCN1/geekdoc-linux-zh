
![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_520_0.png)

OAK PINE / apps/ oak/ bin/ apps/ file1 file2 file3

在这个示例中，一台名为 oak 的计算机通过向 `/etc/exports` 文件中添加条目，使其网络上的客户端（pine、maple 和 spruce）可以使用其 `/apps/bin` 目录。客户端计算机（pine）看到该资源可用，并将其挂载在自己本地文件系统的 `/oak/apps` 挂载点上，之后来自 oak 上的 `/apps/bin` 的任何文件、目录或子目录供 pine 上的用户可用（在权限适当的情况下）。

尽管 Linux 经常被用作文件服务器（或其他类型的服务器），但它是一个通用操作系统，因此任何 Linux 系统都 reality作为服务器共享文件系统（导出），或作为客户端使用另一台计算机的文件系统（挂载）。将此与专用的文件服务器（如 NetWare）相比，NetWare 只能与客户端计算机（如 Windows 工作站）共享文件，而永远不会作为客户端。

### 注意

文件系统通常是存在于单一设备（如硬盘）上的文件和目录结构。一个文件系统可以表示到单一设备（如硬盘分区或光盘）。 NFS 共享目录可以从根目录（/）开始挂载到另一台计算机的文件系统。

# 第四部分：设置 Linux 服务器

## 获取 NFS

虽然大多数 Linux 系统都支持 NFS 客户端和服务器功能，但 NFS 并不是默认安装的。你需要根据不同的 Linux 系统安装不同的包。
以下是一些示例：

- Fedora 和红帽企业 Linux——你需要安装 `nfs-utils` 包将 Fedora 作为 NFS 服务器。还有一个图形化的 NFS 配置工具，需要安装 `system-config` 包。NFS 客户端功能位于基础系统中。要启用 NFS 服务，输入：

```
# service nfs start
# chconfig nfs
```

- Ubuntu 和 Debian——作为 NFS 客户端需要 `nfs-common` 和 `portmap` 包；作为服务器（如果你连接了互联网）会安装它们。遵循 `apt-get` 命令行（如后文所述向 `/etc/exports` 文件导出文件系统），可以使用 `nfs-common` 和 `nfs-kernel-server` 脚本，如下：

```
# apt-get install nfs-common portmap nfs-kernel-server
# /etc/init.d/nfs-kernel-server start
# /etc/init.d/nfs-common start
```

- Gentoo——在 Gentoo 中，必须为内核配置 NFS 文件系统和 NFS 服务器支持。安装 `nfs-utils` 包（`emerge nfs-utils`）可以获得所需的包。要启动服务，运行 `rc-update` 立即启动：

```
# emerge nfs-utils
# rc-update add portmap default
# rc-update add nfs default
# /etc/init.d/nfs start
```

在我遇到的每个 Linux 系统中，通过 `mount`、`exportfs` 等命令从 `/etc/exports`、`/etc/fstab` 实际配置 NFS 的方法都是相同的。在安装并运行 NFS 后，只需按照本章的说明操作。

## 共享 NFS 文件系统

要从你的 Linux 系统共享 NFS 文件系统，你需要将其导出到服务器系统。在 Linux 中通过向 `/etc/exports` 文件添加条目来实现导出。每个条目标识了本地文件系统中你想与其他计算机共享的目录。该条目标识了可以共享资源的其他计算机（或向所有计算机开放），并包含了与目录权限相关的其他选项。

# 第 16 章：运行文件服务器

请记住，当你共享一个目录时，你也共享了该目录下的所有文件和子目录（默认情况下）。因此，你需要确定想要共享该目录结构中的所有内容。仍然有方法限制该目录结构内的访问；这些内容将在本章稍后的部分进行讨论。

## 配置 /etc/exports 文件

要让你的 Linux 系统中的目录对其他系统可用，你需要导出该目录。导出通过向 `/etc/exports` 文件中添加有关导出目录的信息来实现持久化。

`/etc/exports` 文件的格式如下：

| 目录 | 主机(选项) | # 注释 |
| :--- | :--- | :--- |

*Directory* 是你想要共享的目录名称，*Host* 表示限制共享该目录的主机计算机。*Options* 可以包含多种选项，用于定义为该主机的共享目录附加的安全措施。（你可以重复 Host/Option 对）。*Comments* 是你想要添加的任何可选注释（紧跟在 # 符号之后）。

作为 root 用户，你可以使用任何编辑器配置 `/etc/exports` 以修改共享目录条目或添加新条目。以下是 `/etc/exports` 文件的示例：

```
/cal      *.linuxos.net(rw)               # Comment events
/pub      ro,insecure,all_squash)         # Public dir
/home     maple(rw,squash uids=0-99) spruce(rw,squash uids=0-99)
```

`/cal` 条目表示包含与公司事件相关的信息的目录。它可能允许所有与计算机名称（`*linuxos.net`）匹配账户的用户访问。用户可以写入该目录，也可以读取它们（由 `rw` 选项指示）。注释（ Comment events）仅用于提醒你该目录包含的内容。

`/pub` 条目表示一个公共目录。它允许任何用户和读者读取该目录中的文件（由 `ro` 选项指示），但不能写入文件。`insecure` 选项允许任何不使用 NFS 端口的人访问该目录。`all_squash` 选项允许所有 UID（用户 ID）和 GID（组）映射到用户 ID 65534（在 Fedora 中是 nobody 用户，在 Ubuntu 中也是 nobody 用户），从而获得文件的最小权限。

`/home` 条目表示一组用户在不同的计算机上具有相同的 `/home` 目录。例如，假设你正在从一台名为 oak 的计算机共享 `/home`。名为 maple 和 spruce 的计算机可以将该目录挂载到它们自己的 `/home` 目录上。如果所有用户在所有机器上使用相同的用户名/UIDs，那么每个用户都可以拥有相同的 `/home/user` 目录，无论他们登录到哪台计算机。`uids=` 用于防止来自另一台计算机的管理员登录更改共享目录中的任何文件。

这些仅仅是示例；你可以共享你选择的目录，包括整个文件系统（/）。当然，共享整个文件系统或其敏感部分（如 `/etc`）存在安全影响。你可以在 `/etc/exports` 文件中添加的安全选项将在随后的章节中进行描述。

## /etc/exports 中的主机名

你可以在 `/etc/exports` 文件中指定哪些主机可以访问你的共享目录。如果你想将多个主机名或 IP 地址与特定的共享目录关联，请确保在每个主机名之前有一个空格。然而，主机与其选项之间不要有空格。例如：

```
/usr/local maple(rw) spruce(ro,root_squash)
```

注意 `(rw)` 之后有一个空格，但在 `maple` 之后没有。你可以通过几种方式识别主机：

- 单个主机——输入一个或多个 TCP/IP 主机名或 IP 地址。如果主机在你的本地域中，你可以指定主机名。否则，使用全 host.domain 格式。这些是指示单个计算机的有效方式：

```
maple
maple.handsonhistory.com
10.0.0.11
```

- IP 网络——通过指定网络号及其子网掩码（用斜杠 (`/`) 分隔），允许从特定网络地址的所有主机访问。以下是设计网络数的有效方式：
`10.0.0.0/255.0.0.0`
`172.16.0.0/255.255.0.0`
`192.168.18.0/255.255.255.0`
`192.168.18.0/24`

- TCP/IP 域——使用通配符，你可以包含特定域层级的全部或部分主机。以下是星号和问号通配符的一些有效方式：

```
*.handsonhistory.com
*craft.handsonhistory.com
???.handsonhistory.com
```
