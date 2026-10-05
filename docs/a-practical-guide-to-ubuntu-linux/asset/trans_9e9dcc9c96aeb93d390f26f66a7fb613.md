
fstab 的最后一个示例显示了一个远程挂载的家目录。由于 dog 是本地服务器且通过可靠的高速连接的，因此时间被缩短，且 `rsize` 和 `wsize` 显著增加：

```
dog/home /dog.home nfs timeout=4,rsize=16384,wsize=16384 0 0
```

# 设置 NFS 服务器

# 前提条件

安装

安装以下包：

- nfs-kernel-server

portmap 实用程序（它是 portmap 包的一部分，当使用 nfs-kernel-server 时作为依赖项安装；见第 406 页）必须运行以启用可靠的文件锁定。

nfs-kernel-server：当安装 nfs-kernel-server 包时，dpkg postinst 脚本会启动 init 脚本 nfsd（NFS 内核守护进程）。在你配置好 NFS 后，该守护进程会调用 nfs-kernel-server init 脚本来重新导出目录树并重启 NFS 守护进程：

- $ sudo service nfs-kernel-server restart
* Stopping NFS kernel daemon [OK]
* Exporting directories for NFS kernel daemon... [OK]
* Exporting directories for NFS kernel daemon... [OK]
* Starting NFS kernel daemon [OK]

在活动状态的服务器上更改 NFS 配置后，使用 `reload` 代替 `restart` 以导出目录树，而不会干扰连接到服务器的客户端。

# 注意事项

防火墙：NFS 服务器使用 TCP 端口 111 用于 portmap，使用 TCP 端口 2049 用于 nfsd。此外，如果你有其他指令，NFS 服务器将使用 portmap 为其提供的服务分配（所有）随机端口：rpc.statd、rpc.mountd 以及（可选的）rpc.quota。设置防火墙来保护你的服务器免受随机端口的影响更好；指定这些服务各使用哪个端口要容易得多，请如下所示修改以下文件中的行：

```bash
$ grep STATD /etc/default/nfs-common
NEED_STATD="--port 32765 --outgoing-port 32765"
```

```bash
$ grep MOUNT /etc/default/nfs-kernel-server
RPCMOUNTS="--port 32767"
```

```bash
$ grep QUOTA /etc/default/quota
RPCQUOTADOPTS="--port 32769"
```

如果你没有运行 rpc-quotad，则不需要创建或修改 quota 文件。
示例中使用的端口是 Linux NFS-HOWTO 中建议的端口，你可以根据需要使用任何未使用的端口。更多信息请参见 wiki.debian.org/SecuringNFS。

如果 NFS 服务器系统正在运行防火墙，你需要打开端口 111 和 2049。要做到这一点，请使用 gufw（端口 876）设置允许 NFS 服务的策略。此外，如前文所述，打开 /etc/default 文件文件中你指定的端口。
由于 gufw 对这些端口没有定义策略，因此在向 gufw 中添加规则时，需要手动指定端口。

rpc-mountd 守护进程使用 TCP 封装来控制对服务器的访问。
如第 465 页所示，你可以设置 /etc/hosts.allow 和 /etc/hosts.deny 来指定哪些客户端可以联系服务器上的 rpc-mountd 并使用 NFS。
这些文件中守护进程的名称为 mounted。

# 第二部分开始：配置 NFS 服务器
使用 shares-admin

共享文件夹窗口（图 22-2）允许本地系统使用 Samba（第 23 章）和/或 NFS 共享目录树。要显示此窗口，请从终端模拟器或运行应用程序窗口 (ALT+2) 给 shares-admin 命令。点击标记为“点击进行更改”的锁图标并输入密码以启用此窗口设置共享。

在设置 NFS 服务器的过程中，共享文件夹窗口会识别 /etc/exports 文件。如果系统正在运行防火墙，请参见第 782 页的“防火墙”。shares-admin 实用程序允许你指定想要共享哪些目录树以及如何使用 NFS 进行共享。每个导出的树被称为“共享”（share）——该术语借自 Samba。

![](img/45ff4cd21497435daa35084a84)

# 第 22 章：NFS：共享文件系统

![](img/45ff4cd21497435daa35084a84)

要添加共享，点击“添加”（图 22-3）。此窗口有两个部分：共享文件夹和允许的主机。在第一部分，从列表中选择你想要共享的目录路径。如果目录树没有列在列表中，点击“其他”（图 22-4）。然后在列表中选择你想要的目录。

