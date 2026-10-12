
`/mm/eris/local` `apollon(rw)`

上述行赋予了`apollon`对`/mm/eris/local`的读/写权限。除了`rw`，也可以`ro`，表示只读（如果你什么都不写，默认是只读）。你还可以给它提供其他选项，我将讨论一些与安全相关的选项。它们在`exports`页面中都有列出，你一生至少应该读一次。在`exports`文件中列出主机还有更好的方法。例如，如果你正在运行NIS（或NFS），可以使用网络组（NIS曾被称为YP），并始终指定网域通配符和IP子网作为允许挂载的主机。但如果你使用通用的授权，就应该考虑谁可能会通过未经授权的方式访问服务器。

注意：此`exports`文件的语法与Unix使用的不同。在本HOWTO中有一个单独的章节介绍其他Unix系统的`exports`文件。

现在我们准备好开始挂载（可能名为`rpc.mount`和`nfs`（可能名为`rpc.nfs`）。它们都会读取`exports`文件。

如果你编辑了`/etc/exports`，必须让nfs挂载意识到文件已更改。传统方法是运行`exportfs`。许多Linux发行版带有`exportfs`程序。如果你没有`exportfs`，可以在你的机器上安装此脚本：

```sh
#!/bin/sh
killall -HUP /usr/sbin/rpc.mountd
killall -HUP /usr/sbin/rpc.nfs
echo re-exported file systems
```

将其保存为`/usr/sbin/exportfs`，并不要忘记对其执行`chmod a+rx`。现在，每当你更改`exports`文件后，都要以root身份运行`exportfs`。

现在你应该检查mount和nfs是否运行正常。首先使用`rpcinfo -p`查看。它应该显示类似如下的内容：

| program | vers | proto | port |
| :--- | :--- | :--- | :--- |
| 100000 | 2 | tcp | 111 portmapper |
| 100000 | 2 | udp | 111 portmapper |
| 100005 | 1 | udp | 745 mount |
| 100005 | 1 | tcp | 747 mount |
| 100003 | 2 | udp | 2049 nfs |
| 100003 | 2 | tcp | 2049 nfs |

如你所示，portmapper已经发布了它的服务，mount和nfs也是如此。

如果你得到`rpcinfo: can't connect portmapper: RPC: Remote system error - Connection refused`或类似的错误，说明portmapper没有在运行。修复它。如果得到`no remote programs registered`，要么是portmapper没有与你通信，要么某些地方坏了。杀死`nfsd`、`mount`和`portmapper`，重新尝试该序列。

在确认portmapper报告了服务后，你也可以用`ps`进行检查。即使在扩展服务的程序崩溃后，portmapper也会继续报告这些服务。因此，如果某些地方看起来坏了，进行`ps`检查是明智的。

## 设置 NFS 客户端

当然，你将需要修改系统的rc文件，以便在启动时同时启动`mountd`和`portmapper`。这些脚本很可能已经存在于你的机器上，你只需要取消关键部分的注释，或者为正确的init运行级别激活它们。

你现在应该熟悉的man手：`portmap`、`mountd`、`nfsd`和`exports`。

好了，如果你按照我说的做了所有操作，你应该已经准备好开始NFS客户端了。

### 4. 设置 NFS 客户端

首先，你需要一个已经编译了NFS文件系统或可以作为模块可用的内核。这在编译内核之前就已经配置。如果你从未编译过内核，可能需要检查内核HOWTO来弄清楚。如果你使用一个非常酷的发行版（如Red Hat），并且从未对它的内核或模块进行过修改（因此没有搞坏它；），那么nfs对你来说是自动可。

现在你可以在root提示符下输入相应的挂载命令，文件系统就会出现。继续上一节的示例，我们从`eris`挂载`/mnt/eris/local`。这是通过你的命令实现的：

```bash
mount -o rsize=1024,wsize=1024 eris:/eris/local /mnt
```

（我们将回来讨论rsize和size选项。）文件系统现在位于`/mnt`下，你可以进入该目录，进入其中并查看单个文件。你会发现它没有本地文件系统那么快，但比fpt方便得多。如果mount并没有挂载文件系统，而是产生了类似错误消息，例如：`eris:/mn/eris/local failed, reason given by server: Permission denied`，说明`exports`文件错误，或者你忘记在编辑`exports`文件后运行`exportfs`。如果显示`mount: clpt.create: RPC: Program not registered`，说明服务器上的`nfsd`或`mount`未运行。

要移除该文件系统，你可以运行：

```bash
umount /mnt
```

要让系统在启动时挂载nfs文件系统，你需要按通常方式编辑`/etc/fstab`。对于我们的示例，需要这样的一行：

| device | mountpoint | fs-type | options | dump | fs |
| :--- | :--- | :--- | :--- | :--- | :--- |
| eris:/eris/local | /mnt | nfs | rsize=1024,wsize=1024 | 0 |

## 慢速链路上的 NFS

非易失性介质（通常是磁盘）。这在某种程度上限制了写入性能，异步写入将提高NFS的写入速度。Linux nfs从未进行过同步写入，因为Linux文件系统的实现并不适合这种方式，但在非Linux服务器上，你可以通过导出配置以这种方式提高性能：

```bash
/dir -async,access=linuxbox
```

或类似的配置。请参考相关机器上的man页面。请注意，这会增加数据丢失的风险。

### 5. 慢速链路上的 NFS

慢速链路包括调制解调器、ISDN以及可能的其他远距离连接。

本节基于对所用协议的了解，而非实际实验。我的家用电脑已经关机了6个月（硬盘坏了，资金紧张），所以我没有调制解调器连接可以测试。如果你有以下想法，请告诉我：

首先要记住的是，NFS是一个慢速协议。它的开销很大。使用NFS几乎就像使用kermit传输文件。它很慢。几乎任何东西都比NFS快。FTP更快，HTTP更快，rcp更快，ssh更快。

还是不确定吗？

NFS的默认参数非常快，延迟低。如果你在高延迟链路上使用这些默认参数，可能会导致NFS报告错误、终止操作、假装文件比实际短，并在其他情况下表现得诡异。

要做的第一件事是不要使用`soft`（软挂载）选项。这会导致超时并向软件返回错误，而软件可能完全不会处理这种情况。这是导致各种诡异故障的好方法。请使用`hard`（硬挂载）选项。当硬挂载活动超时时，它会无限重试，而不是终止软件想要执行的操作。这正是你需要的。

接下来要做的是微调`timeout`和`retrans`挂载选项。它们在NFS(5) man页面中有描述，这里有一份副本：

| 选项 | 描述 |
| :--- | :--- |
| timeout=n | RPC 超时后发送第一次重传的时间值，单位为十分之一秒。默认值为 7 分之一秒。在第一次超时后，每次连续超时时间都会翻倍，直到达到 60 秒的最大超时时间，或者发生了足够次数重传导致主超时。然后，如果文件系统是硬挂载的，每个新的超时级联从上一次级联初始值的两倍重启，每次重传再次翻倍。最大超时时间为 60 秒。在繁忙网络、到慢速服务器或通过多个路由器或网关挂载时，增加超时时间可能会获得更好的性能。 |
| retrans=n | 在发生主超时之前必须发生的次要超时和重传的次数。默认为 3 次超时。当发生主超时时，文件操作将被终止，或者在控制台上打印“服务器正在响应”的消息。 |

换句话之：如果在0.7秒（700ms）的超时时间内没有收到回复，NFS客户端将重复请求并将超时时间翻倍到1.4秒。如果回复在1.4秒内没有出现，将再次重复并将超时时间翻倍到2.8秒。

可以使用与你的`size/wsize`选项相同的数据包大小来测量链路：

```bash
$ ping -s 8192 lugumbanda
PING lugumbanda.u.no(129.240.222.99): icmp_seq0 ttl=15.2 ms
```
