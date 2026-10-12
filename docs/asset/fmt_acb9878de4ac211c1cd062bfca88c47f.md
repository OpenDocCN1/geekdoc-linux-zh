
然后，在其他机器上（torgo、poodle 和 devel），我们需要编辑 `/etc/sendmail.cf`，在发送邮件时将它们“伪装”为 mail.redhat.com，并将任何本地邮件处理转发到 redhat.com。在 `/etc/sendmail.cf` 中找到 `DH` 和 `DM` 行，并按如下方式进行编辑：

```
# who I send unqualified names to
# (null means deliver locally)
DRmail.redhat.com

# who gets all local email traffic
DHmail.redhat.com

# who I masquerade as (null for no masquerading)
DMredhat.com
```

在这种配置下，所有发送的邮件看起来都像从 redhat.com 发出的，任何发送到 torgo.redhat.com 或其他主机的邮件都将投递到 mail.redhat.com。

请注意，如果你配置你的系统伪装为另一个主机，那么从你的系统发送到你的系统的任何电子邮件都会被发送到你所伪装的那台机器。例如，在上述说明中，由 cron 守护进程定期发送到 root@poodle.redhat.com 的日志文件将被发送到 root@mail.redhat.com。

### 2.10 控制对服务的访问

作为一种安全措施，大多数网络服务由一个称为 `TCP wrapper` 的保护程序管理。受保护的服务是那些在 `/etc/inetd.conf` 中指定了 `/usr/sbin/tcpd` 的服务。`tcpd` 可以根据请求的来源以及 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中的配置来允许或拒绝访问某个服务。

默认情况下，Red Hat Linux 允许所有服务请求。要禁用或限制服务，你可以编辑 `/etc/hosts.allow`。这里有一个示例 `/etc/hosts.allow` 文件：

```
ALL: redhat.com .redhat.com
in.talkd: ALL
in.ntalkd: ALL
in.fingerd: ALL
in.ftpd: ALL
```

此配置允许来自 `redhat.com` 和 `*.redhat.com` 机器的所有连接。它还允许来自所有机器的 talk、finger 和 FTP 请求。

`tcpd` 使用 `/etc/hosts.allow` 和 `/etc/hosts.deny` 的组合允许更复杂的访问控制。阅读 `tcpd(8)` 和 `hosts_access(5)` 手册页以获取完整详情。

### 2.11 匿名 FTP

设置匿名 FTP 很简单。你需要做的只是安装 `anon-ftp` RPM 包（你在安装时可能已经完成了这一步）。一旦安装完毕，匿名 FTP 即可运行。

有几个文件你可能希望编辑以配置你的 FTP 服务器。

#### /etc/ftpaccess

此文件定义了你 FTP 服务器的大多数访问控制。你可以做一些事情包括：设置本地“组”以控制来自不同站点的访问，限制同时 FTP 连接的数量，配置传输日志记录等等。阅读 `ftpaccess` 手册页以获取完整详情。

#### /etc/ftphosts

`ftp.hosts` 文件用于允许或拒绝从不同主机访问特定账户。阅读 `ftp.hosts` 手册页以了解详情。

#### /etc/ftpusers

此文件列出了所有*不允许*通过 FTP 登录你机器的用户。例如，默认情况下 `root` 列在 `/etc/ftpusers` 中。这意味着你不能通过 FTP 登录你的机器并以 `root` 身份登录。这是一个很好的安全措施，但一些管理员喜欢将 `root` 从该文件中移除。

### 2.12 NFS 配置

NFS 代表 Network File System（网络文件系统）；它是一种在机器之间共享文件的方式，就好像它们在本地硬盘上一样。Linux 既可以作为 NFS 服务器也可以作为 NFS 客户端，这意味着它可以**导出**文件系统给其他系统，并**挂载**从其他机器导出的文件系统。

#### 2.12.1 挂载 NFS 文件系统

使用 `mount` 命令从另一台机器挂载 NFS 文件系统：

```bash
mkdir /mnt/local # Only required if /mnt/local doesn't exist
mount bigdog:/mnt/export /mnt/local
```

在此命令中，`bigdog` 是 NFS 服务器的主机名，`/mnt/export` 是 `bigdog` 导出的文件系统，`/mnt/local` 是本地机器上我们想要挂载文件系统的目录。在 `mount` 命令运行后（并且如果我们拥有来自 `bigdog` 的正确权限），我们可以输入 `ls /mnt/local` 并获得 `bigdog` 上 `/mnt/export` 中文件的列表。

#### 2.12.2 导出 NFS 文件系统

控制你希望导出哪些文件系统的文件是 `/etc/exports`。其格式为：

```text
directory          hostname (options)
```

`(options)` 是可选的。例如：

```text
/mnt/export       speedy.redhat.com
```

允许 *speedy.redhat.com* 挂载 `/mnt/export`，但是：

```text
/mnt/export speedy.redhat.com(ro)
```

只是允许 *speedy* 以只读方式挂载 `/mnt/export`。每次你更改 `/etc/exports` 时，你必须告诉 NFS 守护进程检查其中的新信息。实现这一点的一种简单方法是停止并重新启动守护进程：

```text
/etc/rc.d/init.d/nfs stop
/etc/rc.d/init.d/nfs start
```

或者你可以使用此命令重新启动守护进程：

```text
/etc/rc.d/init.d/nfs restart
```

以下操作也可以：

```text
killall -HUP rpc.nfsd rpc.mountd
```

有关更多详情，请参阅以下手册页：`nfsd(8)`、`mountd(8)` 和 `exports(5)`。另一个良好的参考书是 Hal Stern 撰写的 *Managing NFS and NIS Services*，由 O'Reilly & Associates 出版。

### 2.13 启动过程、Init 和关机

本节包含有关当你启动或关闭 Red Hat Linux 系统时发生什么的信息。

#### 2.13.1 启动过程的幕后

当计算机启动时，处理器会查看系统内存的末尾，寻找 `BIOS`（基本输入/输出系统）并运行它。`BIOS` 程序被写入只读永久内存中，并且始终准备就绪。`BIOS` 提供了外围设备的最低层接口，并控制启动过程的第一步。

`BIOS` 会对系统进行测试，查找并检查外设，然后寻找用于引导的驱动器。通常，它会检查软驱（在许多较新的系统中则是 CD-ROM 驱动器，如果存在的话），然后检查硬盘。在硬盘上，`BIOS` 会查找从第一块硬盘的第一个扇区开始的 `主引导记录`（`MBR`），并启动 `MBR`。

`MBR` 会寻找第一个活动分区并读取该分区的引导记录。引导记录包含了如何加载引导加载程序 `LILO`（*Linux LOADER*）的指令。然后 `MBR` 加载 `LILO`，`LILO` 接着接管该过程。

`LILO` 读取文件 `/etc/lilo.conf`，该文件详细说明了要配置哪个操作系统或启动哪个内核，以及它将自身安装在哪里（例如，你的硬盘为 `/dev/hda`）。`LILO` 在屏幕上显示 `LILO:` 提示符，并等待预设的一段时间（也在 `lilo.conf` 文件中设置）以接收用户输入。如果你的 `lilo.conf` 设置为让 `LILO` 提供操作系统选择，此时你可以输入想要启动的 OS 的标签。

在等待一段设定时间（通常是五秒）后，`LILO` 将继续启动在 `lilo.conf` 文件中出现的第一个操作系统。

如果 `LILO` 正在引导 Linux，它首先引导内核，内核是一个位于 `/boot` 目录下的 `vmlinux` 文件（外加版本号，例如 `vmlinuz-2.2.15-xx`）。然后内核接管控制权。

内核会在几个不同的地方查找 `init`（`/sbin` 是一个常见位置），并运行它找到的第一个 `init`。`init` 接管控制权。
