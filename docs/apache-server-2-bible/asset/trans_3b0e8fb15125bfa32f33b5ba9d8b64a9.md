
## 与 NFS 服务器共享驱动器空间

虽然你可以通过网络文件系统（NFS）共享静态内容，但我之前建议使用静态文件的本地副本。除非你选择高端 SAN 解决方案，否则存储在本地驱动器上的文件访问时间会比任何网络存储解决方案都快得多。

我强烈建议你只将在 NFS 分区上放置需要共享、频繁更改或必须在所有 Web 节点间使用相同数据的文件。例如，你的 Web 应用程序可以在所有节点间共享，这样你只需保留一份软件副本。然而，更重要的是，这些应用程序创建的数据也应共享。例如，如果你有一个 CGI 脚本为购物车写入磁盘会话数据，当用户发起下一个请求时，你所使用的负载均衡方案可能会将用户引导到网络中的另一个 Web 服务器，这意味着会话数据必须对其他 Web 服务器可用，否则用户将不得不重新开始他们的购物车。

创建一个目录，在其中保存所有必须共享的数据。例如，在 NFS 服务器上创建 `/www/cgi-data` 作为你的 CGI 脚本数据目录。你可以为每个 CGI 应用程序创建子目录，并配置每个应用程序在其 `/www/cgi-data` 内的专属目录中写入数据。然后，通过 NFS 挂载此目录，它将对网络中的所有 Web 服务器可用。以下部分将展示如何操作。

### 设置 NFS 服务器

NFS 服务器需要运行一个名为 portmapper（也称为 portmap 或 rpc.portmap）的程序，它通常由 rc 脚本启动。要检查 portmapper 是否已在运行，请使用以下命令：

```
ps auxw | grep portmap
```

在 RedHat Linux 下，portmapper 会自动由 `/etc/rc.d/rc3.d/S4/portmap` 脚本（即 `/etc/rc.d/init.d/portmap` 初始化脚本）启动，因此无需手动启动。

下一步是修改 `/etc/exports` 文件，以告知系统哪些文件系统或目录需要导出给 NFS 客户端。由于 XC News 只需将 `/www/cgi-data` 目录导出给 Web 服务器，`ns.xcnews-lan.com` 主机上的导出文件看起来如下：

```
/www/cgi-data www1.xcnews-lan.com(rw) www2.xcnews-lan.com(rw)
```

这一行指示 NFS 服务器允许 `www1.xcnews-lan.com` 和 `www2.xcnews-lan.com` 对 `/www/cgi-data` 目录进行读写访问。

> 导出文件的语法在所有 Unix 品牌中可能并不相同。

必须运行的下一个程序是 mountd（rpc.mountd）和 nfsd（rpc.nfsd）。这两个程序也是由 /etc/rc.d/rc3.d 中的 rc 脚本自动启动的。然而，每当 /etc/exports 文件发生变更时，需要告知这两个程序该变更。名为 exportfs 的脚本可以重启这两个程序，如下所示：

```
exportfs
```

如果系统中缺少 exportfs，则可以使用如下脚本代替：

```
#!/bin/sh
killall -HUP /usr/sbin/rpc.mountd
killall -HUP /usr/sbin/rpc.nfsd
echo re-exported file systems
```

此脚本使用大多数 Linux 系统中存在的 killall 程序；如果该程序不可用，你始终可以运行 ps 命令，找到这些进程的 PID，并手动对每个进程执行 kill -HUP。现在，为确保 mountd 和 nfsd 正在正常运行，请运行名为 rpcinfo 的程序，如下所示：

```
rpcinfo -p
```

输出如下：

| 程序 | 版本 | 协议 | 端口 | 服务 |
|---------|------|-------|------|---------|
| 100000  | 2    | tcp   | 111  | rpcbind |
| 100000  | 2    | udp   | 111  | rpcbind |
| 100005  | 1    | udp   | 635  | mountd  |
| 100005  | 2    | udp   | 635  | mountd  |
| 100005  | 1    | tcp   | 635  | mountd  |
| 100005  | 2    | tcp   | 635  | mountd  |
| 100003  | 2    | udp   | 2049 | nfs     |
| 100003  | 2    | tcp   | 2049 | nfs     |

这表明 portmapper、mountd 和 nfsd 已通告其服务并运行正常。在 Web 服务器上设置 NFS 客户端之前，务必解决安全问题，正如我在下一节中讨论的那样。

### 服务器安全问题

portmapper 与 `nfsd` 结合使用可能会受到欺骗，使得无需任何权限即可访问 NFS 服务器上的文件。幸运的是，Linux 使用的 portmapper 相对安全，抵御攻击的能力较强，并且可以通过在 `/etc/hosts.deny` 文件中添加以下行来提高其安全性：

```
portmap: ALL
```

系统将拒绝所有人访问 portmapper。现在需要修改 `/etc/hosts.allow` 文件如下：

```
portmap: 192.168.1.0/255.255.255.0
```

这使得 `192.168.1.0` 网络中的所有主机能够访问由 portmapper 管理的程序，如 `nfsd` 和 `mountd`。

> **警告** 切勿在 `/etc/hosts.allow` 中的 `portmap` 行中使用主机名，因为使用主机名查找可能会间接引发 `portmap` 活动，从而在循环中触发主机名查找。

服务器端另一个安全问题是是否允许客户端的 root 账户在服务器端被当作 root 处理。默认情况下，Linux 禁止 NFS 客户端端的 root 在服务器端被当作 root 处理。换句话说，服务器上由 root 拥有的导出文件不能由客户端的 root 用户修改。若要显式强制执行此规则，可以按如下方式修改 `/etc/exports` 文件：

```
/www/cgi-data www1.xcnews-lan.com(rw, root_squash) www2.xcnews-lan.com(rw, root_squash)
```

现在，如果客户端上一个 UID 为 0（root 用户）的用户尝试访问（读取、写入或删除）文件系统，服务器会用服务器“nobody”账户的 UID 替代该 UID。这意味着客户端的 root 用户无法访问或更改仅服务器 root 可以访问或更改的文件。

> **提示** 若要授予对 NFS 文件系统的 root 访问权限，请改用 `no_root_squash` 选项。

至此，NFS 服务器已设置并配置好安全，现在让我们设置 NFS 客户端主机。

### 设置 NFS 客户端

默认情况下，Red Hat Linux 支持 NFS 文件系统，因此无需折腾内核。要挂载由 `ns.xcnews-lan.com` 主机导出的 `/www/cgi-data` 目录，请在两台 Web 服务器的 `/etc/fstab` 文件中添加以下行：

```
ns.xcnews-lan.com:/www/cgi-data /www/cgi-data nfs
```

此行会在任何 Web 服务器重启时自动挂载 /www/cgi-data 目录。

接下来，在两个系统上创建 /www/cgi-bin 目录，并使用 mount 命令手动挂载该目录，如下所示：

```
ns.xcnews-lan.com:/www/cgi-data nfs
```

> **警告**
>
> 一个典型的 NFS 挂载问题发生的原因是，许多开发者在修改 NFS 服务器上的 /etc/exports 文件后，忘记了运行 **exportfs**（即**重启 rpc.mountd 和 rpc.nfsd**）。

卸载 NFS 文件系统与卸载本地文件系统完全相同。请注意，也可以通过不太信任 NFS 服务器来增强 NFS 客户端的安全性。例如，你可以使用 **nosuid** 选项禁用 suid 程序在 NFS 文件系统上运行。这意味着服务器的 root 用户无法在文件系统中创建一个 suid-root 程序，登录客户端作为普通用户，然后使用该 suid-root 程序在客户端上也成为 root。还可以使用 **noexec** 选项完全禁止在挂载的文件系统上执行文件。你可以在 /etc/fstab 文件中描述你的 NFS 挂载点的那一行的选项列中输入这些选项。

此时，文件分发方案和基于 NFS 的 CGI 数据目录都已就绪。现在是配置 Apache 并确保其安全的时候了。

NFS 环境中的主要瓶颈是 NFS 服务器的磁盘 I/O 速度。磁盘 I/O 速度取决于你为 NFS 服务器使用何种磁盘子系统。对于大多数情况，使用 IDE 磁盘运行 NFS 服务器的性能不如使用具有高转速的 ultra-wide SCSI 驱动器的服务器。每秒的最大 I/O 操作次数将决定你的 NFS 服务器表现如何。我使用过一台配备 10 块 ultra-wide SCSI 磁盘组 RAID 5 的 Intel Xeon 500 系统作为 NFS 服务器，为大约 50 名用户提供服务，取得了很好的成功。

在确定了良好的磁盘子系统（例如使用 10K RPM ultra-wide SCSI 磁盘阵列和带有大容量内置磁盘缓存的磁盘控制器的 RAID 5）之后，你的下一个硬件瓶颈就是网络本身。将高带宽流量隔离到其专用网络中是减少性能损失的好方法。因此，我建议你使用专用的 100Mbits 以太网连接 NFS 服务器和 NFS 客户端。换言之，创建一个仅传输 NFS 数据包的 NFS 骨干网。这将实现一个高性能的 NFS 网络。

可以帮助你调整 NFS 服务器性能的软件配置选项将在以下部分中介绍。

### 优化读写块大小

NFS 的默认读写块大小为 4096 字节（4K），这对所有情况来说可能并不最优。你可以执行测试来确定更改块大小是否会提高性能。执行此类测试的方法如下。

