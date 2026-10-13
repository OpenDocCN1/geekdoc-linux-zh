
![](img/25fe75b93b97a021effaba85db112a52_328_0.png)

如果你使用过其他 VMware 产品，你会注意到一个不同之处：你无法将虚拟机文件存储在目录层次结构中。你只能从 ESX 服务器选择可用的存储空间并为其指定名称。文件仅存储在分区的根目录中。另一点是，硬盘空间始终预分配给虚拟磁盘文件。动态增长方案不适用于 ESX Server。

图 40.2：向新虚拟机添加磁盘。

## 40.2 使用 ESX Server 远程控制台

对 ESX Server 上虚拟机的控制台访问由 Remote Console 实用程序提供。获取此软件最简单的方法是点击管理界面网页底部的下载链接。

### Windows 安装

在 Windows 计算机上安装客户端应用程序，只需运行下载的可执行文件即可。在撰写本书时，该文件为 VMware-console-2.5.1-13057.exe。安装后，您只需从“开始 → 程序 → VMware”中选择 VMware 虚拟机控制台快捷方式即可启动应用程序。

### Linux 安装

在 Linux 计算机上安装客户端应用程序最简单的方法是下载 RPM 包（VMware-console-2.5.1-13057.i386.rpm）并让包管理器自动安装。

许多最近的 Linux 发行版都附带 RedCarpet 客户端。当您从浏览器下载 RPM 时，您可以选择使用 RedCarpet 打开文件。如果这样做，剩下的唯一额外步骤是在图 40.4 所示的摘要窗口中点击“继续”。

![](img/25fe75b93b97a021effaba85db112a52_329_0.png)

图 40.4：使用 RedCarpet 是安装 Linux 版本最简单的方法。

您也可以使用以下命令手动安装 RPM 版本：

```
rpm -Uhv VMware-console-2.5.1-13057.i386.rpm
```

如果您使用的是较新版本的软件，此示例中的版本号当然可能不同。

如果您没有 RedCarpet 或出于其他原因不想从 RPM 安装应用程序，您可以下载 tar 版本（VMware-console-2.5.1-13057.tar.gz）。

如果您的系统上有 tar 归档文件，您需要对其进行解压缩和提取。您可以使用 z 和 x 参数同时完成此操作：

```
tar -zxf VMware-console-2.5.1-13057.tar.gz
```

归档文件将被提取到名为 vmware-console-distrib 的子目录中。使用 cd 命令进入该目录并从那里开始安装：

```
cd vmware-console-distrib
```

```
./vmware-install.pl
```

这将启动 VMware 虚拟机控制台安装脚本。我在此列出了问题和默认答案供您参考。在大多数情况下，您可以保留默认值。首先，您需要阅读并接受最终用户许可协议。

- 1. 您希望将二进制文件安装到哪个目录？
- `/usr/bin`
- 2. 您希望将库文件安装到哪个目录？
- `/usr/lib/vmware-console`
- 3. 您希望将手册文件安装到哪个目录？
- `/usr/share/man`
- 4. 您希望将文档文件安装到哪个目录？
- `/usr/share/doc/vmware-console`

安装完成后，您将被提示运行配置脚本。您可以回答“是”。或者，您也可以稍后使用以下命令运行脚本：

/usr/bin/vmware-config-console.pl

配置脚本中唯一会询问您的问题是：您希望远程控制台使用哪个端口连接到服务器？默认答案是：902。

## 41 使用 VMware ESX Server 的一些额外提示

一旦开始使用 VMware ESX Server，您需要的许多功能都是自解释的。或者，您也可以查看 VMware 在线文档。以下是一些实用提示，可帮助您更轻松地管理 ESX 服务器。

### 41.1 远程访问 ESX Server 的文件系统

开始使用 VMware ESX Server 时，您肯定需要熟悉 Linux。该产品基于 Linux，并使用 Linux 环境中常见的所有命令、实用程序和配置。您需要习惯的一项具体内容是在许多情况下从 Windows 主机访问 ESX 服务器的文件系统。

执行此操作的一个非常简单且安全的协议是 SSH。它默认在所有 Linux 主机上可用，并且 Windows 环境中也有许多工具可用。任何 SSH 相关软件的良好起点是 www.openssh.com。要使用安全 shell 会话连接到主机，您可以使用 PuTTY，其可从 www.openssh.com/windows.html 获取。

对于文件传输，基于安全复制命令（SCP）的 WinSCP 实用程序非常有用。您可以从 winscp.net 下载此工具。

### 41.2 创建 ISO 仓库

当您开始安装操作系统时，您可能希望使用 ISO 镜像。如果您只有一个 ESX Server 或 GSX Server，那么很简单：只需将文件复制到该服务器即可。但大多数管理员拥有多台服务器，您可能已经有一台存储 ISO 文件集合的 Windows 或 Linux 服务器。

无论哪种情况，将 ESX Server 指向该中央位置都是一个好主意。如果是 Windows 服务器，您可以使用 Samba 协议，如果是 Linux 主机，则可以使用 NFS。

注意：由于它将成为单点故障，使用中央 ISO 存储位置时需要牢记以下几点。确保仅在安装期间将 ISO 连接到虚拟机。机器完全安装后将其断开。如果您将其保持连接状态而 ISO 不可用，将导致错误消息，虚拟机可能无法启动。

### Samba

要创建 Samba 共享，请使用 mount 命令，语法如下：

```
mount -t smbfs -o username=<user>,password=<pw>
    //<ip | host>/sharename <mount point>
```

要将共享挂载到 /mnt/iso 作为具有只读权限的特殊用户：

```
mount -t smbfs -o username=iso,password=secret
    //isosrv/isshare /mnt/iso
```

另外，如果您希望在 ESX Server 启动时自动加载此设置，您需要在 /etc/fstab 文件中添加以下内容。作为前一个命令行示例：

//isosrv/isshare  /mnt/iso  smbfs
    ip=isosrv,username=iso,password=secret,noauto 0 0

### NFS

当您的文件位于另一台 Linux 主机或 ESX Server 上时，您可以设置 NFS 导出，让 ESX Server 指向它。在文件所在的主机上，使用以下命令手动创建导出：

```
exportfs <host>:/path
```

要与名为 esx2 的主机共享 /iso 目录：

```
exportfs esx2:/iso
```

要永久将此 NFS 导出添加到主机，请以以下常用格式将其添加到 /etc/exports 文件中：

/iso/  esx1(ro,root_squash,sync)

在您想要配置文件访问的服务器上，首先必须确保加载了两个必要的守护进程。您可以使用以下命令手动执行此操作：

/etc/init.d/netfs start
/etc/init.d/portmap start

守护进程加载后，使用以下命令手动将 NFS 位置挂载到目录：

```
mount -t nfs <ip | host>:/path <mount point>
```

要访问主机 esx1 上之前导出的共享：

```
mount -t nfs esx1:/iso /mnt/iso
```

要永久将此 NFS 挂载添加到服务器，使其在每次启动时激活，请根据示例将以下行添加到 /etc/fstab 文件中：

```
esx1:/iso /mnt/iso nfs ro,rsize=1024,wsize=1024,noauto 0 0
```

### 41.3 维护和故障排除模式

ESX Server 启动时，它使用 LILO 启动加载程序启动操作系统。在启动加载程序屏幕中，您可以选择启动 ESX（默认）或 Linux。

![](img/25fe75b93b97a021effaba85db112a52_333_0.png)

根据需要使用 Linux 部分对 ESX 服务器进行配置和故障排除。在此模式下，虚拟机不会启动。因此，如果启动过程中出现任何问题，请使用此模式进行调查和故障排除。

图 41.1：LILO 启动加载程序允许您仅启动 Linux 部分。

提示：您可以检查第二终端（Alt-F2）顶部的消息来检查服务器启动的模式。在 ESX vmkernel 模式下启动时，它会显示：VMware ESX Server 2.5.1（或其他版本号）。在 Linux 下启动时，第一行将仅显示：Linux。
