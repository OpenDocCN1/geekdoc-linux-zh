
完成 `wu-ftptpd` 安装后，没有任何需要配置的。在默认的 `wu-ftptpd` 安装下，任何用户都可以使用其用户名和密码进行身份验证，获取其主目录的 FTP 访问（另有规定）。`wu-ftptpd` 设置了三个配置文件。这三个文件分别是 `/etc/ftaccess`、`/etc/fhosts` 和 `/etc/ftpusers`。

## /etc/ftaccess 文件

`/etc/ftaccess` 是主 ftp 配置文件。在 `/etc/ftaccess` 文件中，有许多可以配置和自定义的选项。你可以使用 `loginfails` 选项指定成功登录 FTP 服务器的尝试次数。（默认值为 `logins=5`，允许在 FTP 服务器拒绝连接之前尝试五次）。你也可以允许或拒绝特定类型连接（如 `all`、`guest` 和 `anonymous`）访问特定工具（如 `compress`、`tar` 和 `chmod`）。关于 `/etc/ftaccess` 选项的更多信息，请阅读 ftaccess 页 (`man 5 ftaccess`)。

## /etc/fhosts 文件

`/etc/fhosts` 文件用于允许或拒绝对特定账户的访问。`/etc/fhosts` 文件中有两种条目。第一种是 `allow`，第二种是 `deny`。语法为 `allow username host` 或 `deny username host`。Standard Networking Services 245

例如，`allow kara 192.168.0.*` 只允许用户“kara”从 192.168.0.* 登录。条目 `deny anonymous 192.168.0.*` 将拒绝任何用户从 192.168.0.* 访问。

## /etc/ftpusers 文件

`/etc/ftpusers` 文件用于指定哪些系统账户可以通过 ftp 登录。默认情况下，`root`、`bin`、`daemon`、`adm`、`lp`、`sync`、`shutdown`、`halt`、`mail`、`news`、`uucp`、`operator`、`games` 和 `nobody` 都被加入。如果你创建了任何想要拒绝 FTP 访问的用户，也将他们加入。

## 设置匿名 FTP

匿名 FTP 服务器不需要特定的用户 ID 或密码即可访问服务器。这意味着可以使用匿名 FTP 客户端（如 Netscape）并简单地传递通用用户名（如“anonymous”和“ftp”）以及电子邮件地址作为密码。

要将你的 FTP 服务器配置为匿名 FTP 服务器，你可以安装 `anftpd` RPM，然后 ftpd 服务器将自动配置。该 RPM 可以在你的 Red Linux 6.0 光盘上的 `/RedHat/RPMS/anftpd-2.8.1.i386.rpm` 找到。

## 网络文件系统 (NFS)

NFS 是网络文件系统，Unix 和类 Unix 系统之间共享文件的标准方法。Linux 可以是其他 Linux（或 Unix）系统的 NFS 服务器，也可以是 Linux（或 Unix）系统的 NFS 客户端。

## NFS 服务器

Red Hat 6.0 使用 2.2 Linux 内核的新内核 NFS 功能。因此，为了使用 NFS 服务器，内核必须配置相应的内核支持。`nfsd` 需要 `nfsd.o` 模块（该模块又需要 `lockd.o` 和 `sunrpc.o` 模块）。此外，NFS 服务器还需要以下特定的用户空间守护进程和实用程序。

### 第 10 章

- Portmap: NFS 服务器系统必须运行 portmap 守护进程。它包含在 portmap 软件包 `portmap-4.0-15.i386.rpm` 中。

- RPC: 必须运行 `knfsd` 包的 RPC 守护进程。这些包括 `rpc.statd`、`rpc.bind`、`rpc.mountd` 和 `rpc.nfsd`。（可以通过运行 `/etc/rc.d/init/nfs start` 来启动）。

> 注意：如果由于原因 nfs-d 模块不可用，`rpc.nfsd` 将继续运行，行为与旧的用户空间 unfsd 相同。通常情况下，它会将控制权移交给内核 nfsd 并退出。

## 配置 NFS 服务器导出

`knfsd` 服务器使用 `/etc/exports` 来配置导出的 NFS 文件系统。文件条目的格式如下：

```
/path/to/export host(options)
```

第一个字段 (`/path/to/export`) 是您希望通过 NFS 提供的路径。例如 `/mnt/cdrom`。第二个字段 (`host`) 是您希望共享文件系统的主机名（IP 地址或地址/子掩码）。如果没有提供 host，则该文件系统将导出给所有人。最后一个字段 (`options`) 是一个用逗号分隔的导出选项列表。一些示例包括 `ro` 表示只读，`rw` 表示读写。选项字段的示例可以是 `(ro)`，指定导出的文件系统为只读，或者 `(rw)`，指定导出的文件系统为可读可写。以下是 `/etc/exports` 文件的示例：

```
/mnt/cdrom (ro)
/tmp (rw)
/home 192.168.0.0/255.255.255.0(rw)
```

在上述示例中，第一行 `/mnt/cdrom` 对所有人只读。上述示例中的第二行 `/tmp` 对所有人可读写。上述示例中的第三行 `/home` 仅对 `192.168.0.0` 网络可读写。有关关于 `/etc/exports` 格式和选项的更多信息，请查看 exports 手页（`man 5 exports`）。

在将文件系统条目添加到 `/etc/exports` 后，您必须执行以下步骤：

1. 运行 `exportsfs -av`。要初始将 `/etc/exports` 中的所有条目添加到导出文件系统列表（假设 `mountd` 已经运行），请运行 `exportsfs -av`。`a` 选项指定 `exportsfs` 添加条目，`v` 选项指定详细打印输出。

## 标准网络服务

2. 运行 `exportfs -rv`。在对 `/etc/exports` 进行更改后，您必须使用 `exportfs -rv` 更新 NFS 服务器。此命令会重新导出 `/etc/exports` 中的所有目录，将服务器的导出列表（由 `/var/lib/nfs/stab` 中的 `mount` 维护）与 `/etc/exports` 文件同步。

要从 mount 的可导出文件系统列表中删除一个文件系统，请使用 `exportfs -u`。关于 `exportfs` 的更多信息可以在 `exportfs(8)` 手页中找到（`man 8 exportfs`）。

## NFS 客户端

NFS 客户端包含在 RPM 包 `knfsd-1.2.2-4.i386.rpm` 中。此外，还有一个名为 `knfsd-clients-1.2.2-4.i386.rpm` 的 RPM 包。它包含了 `showmount` 等实 NFS 客户端工具。Linux 默认 NFS 客户端由几个部分组成。最重要的部分包括特定的内核模块 `port` 和 `mount`。

## 内核模块

NFS 客户端需要特定的内核模块。这些包括 `nfs.o`、`lockd.o` 和 `sunrpc.o`。这些内核模块安装在默认的 Red Hat 6.0 内核安装中，并在通过内核模块加载器挂载远程文件系统时自动加载。

## portmap

NFS 客户端（以及服务器）要求系统运行 portmap 守护进程。为了让 NFS lockd（跨 NFS 的文件锁定）守护进程正常工作，必须运行 portmap 守护进程。在 Red Hat 6.0 中，portmap 守护进程被安装在 `/sbin/portmap`（包含在 portmap RPM `portmap-4.0-15.i386.rpm` 中）。要启动 portmap，请运行 `/etc/rc.d/init.d/portmap start`。

## mount

使用 NFS 所工具是 `mount` 工具。`mount` 工具用于挂载远程 NFS 文件系统。`mount` 工具的常用用法是 `remothost:/path /local/path`。NFS 有几个常用的 mount 选项。表 10.2 列出了 NFS 上最常用的 mount 选项。

使用上述 mount 选项，可以通过执行以下命令在 NFS 服务器 `linux.example.com` 上以 8k 块大小挂载文件系统 `/export` 到 `/mnt/nfs`：

```
mount linux.example.com:/export /mnt/nfs -o rsize=8192,wsize=8192
```

## 10.2 NFS mount 选项。

| Mount 选项 | 描述 |
| --- | --- |
| size=num | 每次读取 num 字节（而不是默认的 1024 字节）。 |
| wsize=num | 每次写入 num 字节（而不是默认的 1024 字节）。 |
| soft | 如果发生超时，向调用程序返回 I/O 错误。 |
| hard | 如果发生超时，向控制台发送“Server not responding”并继续重试。（这是默认值） |
| intr | 对于超时的硬挂载，允许通过信号向调用程序中断 I/O。（默认不允许在硬挂载上进行 I/O。） |

## NFS 工具

除了用于挂载文件系统的 `mount` 命令外，还有其他一些实用的工具可以帮助使用和管理文件系统。表 10.3 列出了几个让您的生活变得更方便的额外工具。

## Samba (SMB)

Samba 是实现 SMB（服务器消息块）的源软件。SMB 允许您设置 Red Hat Linux 6.0 机器作为 Windows 95/98 服务（如文件共享）的服务器。

## 设置 SMB

在 Red Hat Linux 6.0 中，您可以在安装期间安装 Samba（“设置文件共享”）。

## 表 10.3 NFS 工具。

| NFS 工具 | 用法 | 描述 |
| --- | --- | --- |
| df | df | 列出挂载在您的机器上的文件系统 |
| showmount | showmount -e host | 显示主机的导出信息 |
| rpcinfo | rpcinfo -p | 列出运行的 RPC 服务 |

## 设置 Samba 共享

设置 Samba 共享时，遵循以下步骤：

1. 检查 `/etc/smb.conf` 中的 workgroup 设置。默认设置为“WORKGROUP”。要将工作组（域）设置为 MYGROUP，请在 `[globals]` 部分添加一行：

```
workgroup = MYGROUP
```

## 表 10.4 SMB 文件。

| 文件 | 路径 | 描述 |
| --- | --- | --- |
| smb.conf | /etc/smb.conf | Samba 配置文件 |
| smbpasswd | /etc/smbpasswd | Windows 密码 |
| smbuser | /etc/smbuser | Unix 用户映射 |
| nmbd | /usr/sbin/nmbd | NetBIOS 名称 |
| smbd | /usr/sbin/smbd | SMB 守护进程 |
| swat | /usr/sbin/swat | Web 配置工具 |
| smbadduser | /usr/sbin/smadduser | 添加用户 |
| smbclient | /usr/bin/smbclient | 连接 SMB 客户端 |
| smbmount | /usr/bin/smbmount | 挂载 SMB |
| smbprint | /usr/bin/smbprint | 打印 |
| smbrun | /usr/bin/smbrun | 启动 SMB |
| smbdstatus | /usr/bin/smbdstatus | 状态信息 |
| smbtar | /usr/bin/smbtar | 备份 Windows |
| smbumount | /usr/bin/smbumount | 卸载 SMB |

2. 将共享添加到 `/etc/smb.conf`。您首先需要在 `/etc/smb.conf` 的共享定义部分添加共享条目。该条目将包含六行。第一行将命名您的共享，例如 `[USER_HOME]`：

```
[USER_HOME]
comment = Home Directories
path = /home
public = yes
printable = no
writable = yes
```

3. 检查您的 `/etc/smb.conf` 语法。在对 `/etc/smb.conf` 进行更改后，您应该检查 `smb.conf` 语法。一个允许您执行此操作的工具是 `testpar`。

4. 重启 Samba。在 `/etc/smb.conf` 配置恰当后，您需要重启 SMB 服务器。执行为此，运行 `/etc/rc.d/init.d/smbd restart`。

5. 测试您的 SMB 共享。首先检查 SMB 是否正在运行（`/etc/rc.d/init.d/smbd status`）。如果 SMB 运行正常，尝试通过 `smclient` 挂载您的 SMB 共享：`-L localhost`。（当提示密码时，直接按回车即可。）如果您的系统工作正常，您应该看到您的机器作为 SMB 共享提供的所有内容。

# 动态主机配置协议 (DHCP)

DHCP 是 bootp 的超集，用于为网络上的客户端分配 IP 地址。DHCP 用于可以移动、连接和断开网络连接的动态主机。DHCP 可以从 `/etc/dhcpd.leases` 中预先分配的 IP 地址中动态分配 IP 地址，并根据 NIC 的 MAC（媒体访问控制器）地址设置静态 IP 地址。DHCP 甚至可以通过仅接受来自指定 MAC 地址的请求来限制访问。

# 设置 DHCP 服务器

要设置 DHCP 服务器，请确保你已经安装了 DHCP RPM 包。与 Red Hat Linux 6.0 一带的 DHCP RPM 包是 `dhcp-2.0b1pl6-6i386.rpm`。完成 DHCP 服务器的设置，请按照以下步骤操作：

- 1. 检查你的内核是否支持 MULTICAST（多播）。要执行此操作，请运行 `ifconfig -a`。如果你已经支持 MULTICAST，你将在 `ifconfig` 输出的 `eth0` 部分看到有一行显示 `UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1`。如果配置中没有 MULTICAST，你必须重新配置你的内核以支持 MULTICAST、更换你的 NIC（如果不支持），或更改你的接口设置。

- 2. 为 255.255.255.255 添加路由（微软客户端需要）。要执行此操作，请输入 `route add -host 255.255.255.255 dev eth0`（其中 `eth0` 是你的以太网设备）。

> 注意：如果在添加此路由时遇到“unknown host”（未知主机）错误，请在 `/etc/hosts` 中添加以下条目：`255.255.255.255 all-ones`。

- 3. 启动 DHCP 服务器。要启动服务器，输入 `/etc/rc.d/init.d/dhcpd start`。

- 4. 验证 DHCP 是否正常工作。输入 `/usr/sbin/dhcpd -d -f`。

- 5. 配置你的 `/etc/dhcpd.conf` 文件（以下为客户端设置随机 IP 的示例）。

# 配置 DHCP 用于随机分配 IP

要设置 DHCP 为网络上的 DHCP 客户端分配随机 IP，你需要配置 `/etc/dhcpd.conf` 文件，它是 DHCP 的主配置文件。以下列表包含了 `/etc/dhcpd.conf` 的示例设置，这些设置允许 DHCP 在你的网络上随机分配位于 `192.168.1.10` 到 `192.168.1.100` 之间的 IP 地址，以及 `192.168.1.150` 到 `192.168.1.200` 范围。列表 10.3 是一个示例 `/etc/dhcpd.conf` 配置。

# 列表 10.3 示例 /etc/dhcpd.conf。

```
default-lease-time 500;
max-lease-time 6000;
option subnet-mask 255.255.255.0
option broadcast-address 192.168.1.255
option routers 192.168.1.254
option domain-name-servers 192.168.1.1, 192.168.1.2;
option domain-name "example.com";
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.10 192.168.1.100;
  range 192.168.1.150 192.168.1.200;
}
```

# 使用 DHCP 客户端

Red Hat Linux 上使用的 DHCP 客户端称为 `pump`。如果你在 Red Hat Linux 安装期间没有安装 `pump`，你可以从 Red Hat Linux 6.0 光盘安装 pump RPM。该文件为 `pump-0.6.4-i386.rpm`，可以在 Red Hat 6.0 光盘的 `/RedHat/RPMS/` 目录下找到。要配置你的 Linux DHCP 客户端，请采取以下步骤：

- 1. 在根提示符下输入 `netcfg` 执行 `netcfg`。

- 2. 选择 Interfaces（接口）按钮（参见图 10.4 的步骤 2、3、8 和 9）。

- 3. 选择你网络连接的以太网接口（通常为 `eth0`）。

- 4. 选择 Edit（编辑）按钮以调出以太网接口的配置窗口。（参见图 10.5 的步骤 4、5、6 和 7）。
