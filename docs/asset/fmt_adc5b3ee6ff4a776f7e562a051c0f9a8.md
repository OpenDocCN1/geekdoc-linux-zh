
![](img/494a93e1dbdce90cc5cca36f1589d45f_524_0.png)

Apache Web Server Config 生成类似以下的内容：

```
<VirtualHost 192.168.1.9>
  ServerAdmin gabriele@home.now
  DocumentRoot /home/httpd/gabriele/html
  ServerName gabriele.home.now
  ErrorLog /var/log/httpd/gabriele/error_log
  CustomLog /var/log/httpd/gabriele/referer_log
  CustomLog /var/log/httpd/gabriele/access_log
</VirtualHost>
```

你可以添加其他指令（如 `ScriptAlias`）来覆盖 CGI 程序的来源：

```
ScriptAlias /cgi-bin "/home/httpd/gabriele/cgi-bin/"
```

大多数目录指令都允许位于 `<VirtualHost>` 容器标签内。尝试一下。你应该能够输入你的新别名 `http://gabriele.home.now/` 并看到 `/home/httpd/gabriele/html` 的索引。

## 总结

TurboLinux 是一个极好的 Web 服务器。Linux 与世界上最流行的 Web 服务器 Apache 的结合，构成了一个成本效益且稳健的内容交付系统。无论你是在互联网上与朋友共享文件，还是分发企业范围的信息，在本章中，我仅仅浅尝了 Apache 所能做的皮毛。本章的目标是对可用的主要功能和配置选项提供全面的覆盖。

*(注：由于原文结尾处存在重复文本，译文已根据逻辑要求进行了去重处理以保持流畅)*

括号内可以放置许多有效选项。

常见的条条目有 `ro`（导出为只读）和 `rw`（导出为可读写）。

以下的 `/etc/exports` 文件示例直接取自导出手册页。它说明了许多主机和选项规范。

```
# sample /etc/exports file
/
master(rw) trusty(rw,no_root_squash)
/projects proj*\.local.domain(rw)
/usr *.local.domain(ro)
/home/joe pc001(rw,all_squash,anuid=150,anagid=100)
/pub/private (ro,insecure,noaccess)
```

第一条目使名为 `master` 和 `trusty` 的机器可以使用根文件系统。这两个机器对磁盘都具有读写权限。此外，`trusty` 的 root 用户可能对磁盘具有完全访问权限。默认情况下，Linux 的 NFS 实现设置了 `root_squash` 选项，将用户 ID 0 转换为匿名用户，从而禁止任何挂载该文件系统的机器上的 root 账户执行删除或移动导出目录等更改。下一行显示任何名称在 `local.domain` 上以 `proj` 开头的主机都可以访问 `/projects` 目录。这些主机必须具有读写权限。`/usr` 导出对本地域提供只读访问，允许下一组的主机具有读写权限。目录 `/home/joe` 可供单个主机 `pc001` 访问。它具有读写权限，并且所有用户 ID 都被更改为匿名 ID `user-150` 和 `group-100`。最后两个条目相关。`/pub` 目录对所有人开放，包括那些使用 `insecure` 选项指定的、不使用保留端口的 NFS 的主机。在这种情况下，这是合理的，所有用户都将转换为匿名 ID `nobody`。对于 `/pub` 条目的注意事项是 `exports` 文件中的最后一行，它禁止任何人访问子目录 `/pub/private`。

在你配置好想要与其他系统共享的文件的 `exports` 文件后，你必须启用 `mountd` 和 `nfsd` 守护进程。你可以使用 `turbnoservice` 为所有相关的运行级别启用这些服务，或者可以使用以下命令手动启动它们：

```
/etc/rc.d/init.nfs start
```

你可以通过 `status` 选项确认这些进程正在运行：

```
/etc/rc.d/init.nfs status
rpc.mountd (pid 537) is running...
nfsd (pid 552 551 550 549 547 546 545) is running...
rpc.rcquotad (pid 529) is running...
```

你看到的第三个进程 `rpc.rquotad` 为远程文件系统返回配额信息。如果你正在使用磁盘配额，这可以限制用户在 NFS 挂载的文件系统上存储多少的内容。

你还应该看到这些进程已向 `portmapper` 注册。以下是 `rpcinfo -p` 输出的片段。

```
rpcinfo -p
vers proto port
100011 1 udp 706 rquotad
100011 2 udp 706 rquotad
100005 1 udp 713 mountd
100005 1 tcp 715 mountd
100005 2 udp 718 mountd
100005 2 tcp 720 mountd
100003 2 udp 2049 nfs
```

如果你在 NFS 服务运行期间对 `/etc/exports` 文件进行了更改，可以使用 `exportfs` 命令强制 NFS 重新读取该文件。另一种替代方案是重启 NFS 服务，`/etc/rc.d/init.nfs restart`。如果 `/etc/exports` 为空，NFS 服务将不会启动。如果你修改了 `exports` 文件并执行 `/etc/rc.d/init.nfs restart`，NFS 服务仍然不会启动。你需要通过执行 `/etc/rc.d/init.nfs restart` 来告诉 NFS 启动。关于主机名和挂载选项的完整列表，请参阅 `exports` 手册。

# 客户端

NFS 客户端-服务器关系负责挂载服务器导出的文件系统。以下 `mount` 命令挂载导出系统：

```
mount -o rsize=8192,wsize=8192 gabriele:/mnt/home
```

此命令将 `gabriele` 挂载到本地系统的 `/mnt/home`。`-o` 表示挂载选项。`rsize` 和 `wsize` 表示从远程文件系统读取和写入的数据块大小（字节为单位）。NFS 有许多其他选项。你可以参阅 `mount` 手册中的 NFS 部分以获取选项列表。

# 第 26 章 - UNIX 和 Windows 文件服务

用于挂载 NFS 的常用选项除了 `rsize` 和 `wsize` 外还有 `hard`、`soft` 和 `intr`。`hard` 和 `soft` 选项定义了客户端如何连接系统以及写入文件系统的程序的行为。如果 NFS 服务器由于原因不可用，使用 `soft` 选项挂载的客户端将向写入文件系统的程序返回错误，写入可能会损坏或读取可能会错误。由于存在数据丢失，我不建议使用此选项。`hard` 选项会一直重试读写操作直到成功，这可能会导致程序挂起。如果你指定 `intr` 选项，你将能够中断正在等待的程序。这将中止文件操作。根据这些信息，更好的 `mount` 命令是：

```
mount -o rsize=8192,wsize=8192,hard,intr gabelle:/home /mnt/home
```

要为本地文件系统进行后续，必须手动编辑 `/etc/fstab` 文件或使用 `TurboFSCfg`。选择 Filesystems；添加 NFS filesystem。在 Hostname 或 IP address 填写服务器的 IP 地址或名称。输入 NFS 服务器上导出的文件系统路径。如果你不知道路径，点击 NFS Exports 按钮时可以看到它们的列表。从列表中选择你想使用的一个并输入到 Remote Pathname。接下来，选择你想挂载到本地文件系统的位置。你可以从几个常用的 NFS 选项中进行选择。见图 26-1。

![](img/494a93e1dbdce90cc5cca36f1589d45f_530_0.png)

`/etc/fstab` 中相同的挂载条如下所示：

```
gabelle:/home /mnt/home nfs defaults,user,intr 0 0
```

由于性能部分描述的原因，你可能希望调整 `rsize` 和 `wsize` 选项。这时你需要直接编辑 `/etc/fstab`。
