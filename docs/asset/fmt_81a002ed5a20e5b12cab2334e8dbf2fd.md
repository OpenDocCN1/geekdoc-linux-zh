
在这个示例中，名为 `oak` 的计算机通过向 `/etc/exports` 文件添加条目，向网络上的客户端（`pine`、`maple` 和 `spruce`）开放了其 `/apps/bin` 目录。客户端计算机（`pine`）看到该资源可用，并将其挂载到其本地文件系统的挂载点 `/oak/apps` 上，之后，`oak` 上的 `/apps/bin` 中的任何文件、目录或子目录都对用户（在具有适当权限的情况下）可用了。

尽管 Linux 通常被用作文件服务器（或其他类型的服务器），但它是一个通用操作系统，任何 Linux 系统都可以作为服务器共享文件系统（导出/`export`），或作为客户端共享其他计算机的文件系统（挂载/`mount`）。与这些专用文件服务器（如 NetWare）相比，后者仅能与客户端计算机（如 Windows 工作站）共享文件，而不能作为客户端。

> 文件系统通常是存在于单个设备（如硬盘分区或光光盘）上的文件和目录的结构。Linux 文件系统指的是整个目录结构（`/`），它可能包括来自几块磁盘的文件系统（或 NFS 资源），从单台计算机上的根目录（`/`）开始。NFS 中的共享目录可能代表计算机文件系统的全部或部分，它可以连接（从共享目录向下延伸到目录树）到另一台计算机的文件系统上。

# 获取 NFS

虽然每个 Linux 系统都支持 NFS 客户端和服务器功能，但 NFS 并不总是默认安装的。你需要根据不同的 Linux 系统安装不同的包来安装 NFS。有一些示例：

- Fedora 和其他 Red Hat Linux 系统 — 你需要安装 `nfs-utils` 包来将 Fedora 作为 NFS 服务器。还有一个图形化的 NFS 配置工具，它需要你安装 `system-config-nfs` 包。NFS 客户端功能包含在基础操作系统。要运行 nfs 服务，输入以下命令：
```bash
service nfs start
chkconfig nfs on
```
- Debian — 要作为 NFS 客户端，需要 `nfs-common` 和 `portmap` 包；作为 NFS 服务器，必须添加 `nfs-kernel-server` 包。下面的 `apt-get` 命令行（如果你连接了互联网）会安装所有这些包。然后，在你将文件系统导出到 `/etc/exports` 文件后（如后文所述），你可以启动 `nfs-common` 和 `nfs-kernel-server` 脚本，如下所示：
```bash
apt-get install nfs-common portmap nfs-kernel-server
/etc/init.d/nfs-kernel-server start
/etc/init.d/nfs-common start
```
- Gentoo — 使用 Gent 时，NFS 文件和服务器支持必须配置到内核中才能使用 NFS 服务器功能。安装 `nfs-utils` 包（`emer nfs-utils`）应该可以获取所需的包。要启动服务，运行 `rc-update` 并立即启动服务：
```bash
emer nfs-utils
rc-update add portmap default
rc-update add nfs default
/etc/init.d/nfs start
```

实际配置 NFS 的命令（`mount`、`exports` 等）和文件（`/etc/exports`、`/etc/fstab` 等）在我遇到的每个 Linux 系统上都是相同的。一旦你安装并运行了 NFS，只需按照本章中的指令开始使用 NFS。

# 共享 NFS 文件系统

要从你的 Linux 系统共享 NFS 文件系统，你需要从服务器系统将其导出。导出是通过向 `/etc/exports` 文件中添加条目来完成的。每个条目识别了你本地文件系统中你想与其他计算机共享的目录。该条目还识别了可以共享该资源的其他计算机（或向所有计算机开放），并包含了反映与目录相关权限的其它选项。

记住，当你共享一个目录时，默认情况下你也共享了该目录下的所有文件和子目录。因此，你需要确定你想要共享该目录结构中的所有内容。仍然有限制该目录结构内访问的方法，这些将在本章稍后部分讨论。

# 配置 /etc/exports 文件

要让你 Linux 系统中的目录对其他系统可用，你需要导出该目录。导出通过向 `/etc/exports` 文件添加有关导出目录的信息来实现永久性导出。

`/etc/exports` 文件的格式为：

`Directory Host(options) # comment`

其中 `Directory` 是你想共享的目录名称，`Host` 表示限制对此目录共享的主机计算机。`Options` 可以包括多种选项，用于定义附加到该主机的共享目录的安全措施。（你可以重复 `Host/Option` 节点）。注释是你任何想要添加的可选注释（跟在 `#` 符号之后）。

作为 root 用户，你可以使用任何文本编辑器配置 `/etc/exports` 以修改共享目录或添加新文件。这里是 `/etc/exports` 文件的一个示例：

```
/cal *linuxux.net(rw) # Company events
pub (root,Insecure,all_squash)
home (root,Insecure,all_squash)
```

等一下，让我重新检查示例块的 OCR 文本。根据标准的 NFS 导出重建可能的示例：

```
/cal *linuxux.net(rw) # Company events
pub (root,Insecure,all_squash)
home (root,Insecure,all_squash)
```

（注：此处根据原文提供的内容进行了格式对齐）

## /etc/exports 中的主机名

你可以在 `/etc/exports` 文件中指定哪些主机计算机可以访问共享目录。每个主机名之前有一个空格。识别主机的方法有：

- **单个主机** 输入一个或多个 TCP/IP 主机名或 IP 地址。如果主机位于本地域，你可以直接指定主机名。否则，使用全主机.域名格式。以下是识别单个计算机的有效方法：
```
maple
maple.handsonhistory.com
10.0.0.1
```
- **IP 网络** 通过指示网络数及其子掩码（用 `/` 分隔），允许来自特定网络的所有主机访问。以下是设计网络数的有效方法：
```
10.0.0.0/255.255.0.0
172.16.0.0/255.255.0.0
192.168.18.0/255.255.255.0
```
- **TCP/IP 域名** 使用通配符，你可以包含特定域名的所有或部分主机计算机。以下是星号和问号通配符的一些有效用法：
```
*.handsonhistory.com
*craft.handsonhistory.com
???handsonhistory.com
```
