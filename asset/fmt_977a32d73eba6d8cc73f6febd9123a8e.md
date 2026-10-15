
NFS 分区无法通过 `umount` 命令卸载。如果你在尝试卸载时 NFS 文件系统正在使用中，你将得到类似如下的错误信息：

> umount: coyote/home/boggs: device is busy

和任何其他文件系统一样，NFS 文件系统在在使用时无法卸载。使用 `fsof` 找到在文件系统上打开文件的进程；将它们杀死，或者如果是 shell，则更改目录。如果所有方法都失败或你的服务器已宕机，尝试使用 `umount -f` 强制卸载文件系统。

## 在启动时挂载文件系统

你可以使用 `mount` 命令建立临时的网络挂载，但你应该将系统永久配置的挂载项列在 `/etc/fstab` 中，以便它们在启动时自动挂载。或者，挂载可以由 `mount` 或 `amd` 等自动挂载服务处理；参见第 479 页的自动挂载。

3. 我们的技术评审员之一 Jeff Forys 评论：“大多数挂载应该使用 `hard`、`intr` 和 `bg`，因为这些选项保留了 NFS 的原始设计目标（可靠性和无状态），`soft` 是一种恶行，除非用户想要中断（cool）。否则，请等待服务器，一切最终都会恢复正常且没有数据丢失。”

4. 如果你使用 `iptables` 或其他过滤工具，你可能需要添加规则来接受分片包，因为 8K 超过了以太网的 MTU。接受分片包可能会让你更容易受到拒绝服务攻击。

## 安全端口限制

NFS 客户端在连接到 NFS 服务器时可以自由使用任何 TCP 或 UDP 源端口。然而，如果由于在导出文件系统时使用了 `secure` 导出选项（这是默认选项），Linux 服务器可能要求请求来自特权端口（小于 1024 的数字）。在 PC 和桌面 Linux 机器的世界，使用特权端口提供的实际安全性非常有限。

NFS 客户端采用了传统的（且仍推荐的）方法，默认使用特权端口，以避免潜在的冲突。要接受来自非特权源端口的挂载，请使用 `insecure` 选项导出文件系统。

## 17.4 NFSSTAT：NFS 统计数据

NFS 提供了一个名为 `nsstat` 的命令，可以显示 NFS 系统维护的各种统计数据。`nsstat -s` 显示 NFS 服务器进程的统计数据，`nsstat -c` 显示与客户端操作相关的信息。例如：

```
% nsstat -s

  Server rpc stats:

    calls      badcalls  badauth  badcint  xdrcall

    2434112    311       9        302      0

  Server nfs2

    getattr    null      setattr  root     lookup   readlink

    8470054    35 0%     55199 0%  118297 4% %%

    8470054    35 0%     55199 0%  118297 4% %%

    8470054    35 0%     55199 0%  118297 4% %%

    write      symlink   remove

    ...（此处已截断）
```

以下 `fstab` 条目挂载了来自主机 coyote 和 inura 的 /home 和 /usr/local 文件系统：

| filesystem | mountpoint | ftype | dump fsck |
| --- | --- | --- | --- | --- | --- |
| cote/home | coyote/home | nfs | rw,bg,intr,hard | 0 0 |
| inura/local | /usr/local | nfs | ro,bg,intr,sort | 0 0 |

当你向 `fstab` 添加条目时，请务必使用 `mkdir` 创建相应的挂载点目录。你可以通过运行 `mount -a -t nfs` 来挂载 fstab 中所有类型为 nfs 的文件，从而让更改立即生效（无需重启）。

`/etc/fstab` 的标志指定了 NFS 挂载的选项；这些选项与你在 `mount` 命令中指定的选项相同。

## 17.5 专用 NFS 服务器

## 17.6 自动挂载

## 17.7 自动卸载

# 第 17 章 网络文件系统

你很少需要直接运行 `automount` 命令，因为自动挂载的所有管理几乎都是通过 `/etc/init.d/autofs` 完成的。与大多数启动脚本一样，`autofs` 脚本接受命令行上的单个参数，可以是 `start`、`reload`、`restart` 或 `status`。每当对自动挂载配置进行更改时，你必须运行 `autofs reload` 以使更改生效。`autofs status` 可向你显示现有自动挂载的状态。

`auto.master` 文件将挂载点与“映射（map）”关联起来。映射将被称为“键（key）”的目录名称翻译为可用于执行实际挂载的命令行。映射可以是文本文件、可执行程序，或者是 NIS 或 LDAP 数据库。

当用户引用一个使用 `autofs` 内核文件系统挂载的目录时，它会通知用户态自动挂载进程该访问。自动挂载进程通过查询映射或程序来确定要挂载哪个文件系统，然后在将控制权返回给触发它的用户之前执行挂载。

你可以通过运行 `mount` 和 `ps` 来看到 `autofs` 文件系统以及它们所属的自动挂载进程：

```text
+ mount
/dev/hda3 / type ext2 (rw)
proc on /proc type proc (rw)
/dev/hda1 /boot type ext2 (rw)
automount(pid8359) / /misc type autofofs (rw,fd=5,pg=8359,minproto=2,maxproto=4)
automount(pid8372) / /net type autofofs (rw,fd=5,pg=8372,minproto=2,maxproto=4)
+ root 8359 0.0 1360 652 ? S Dec27 0:00
/usr/sbin/automount /misc file /etc/auto.misc
root 8372 0.0 1360 652 ? S Dec27 0:00
/usr/sbin/automount /net /etc/auto.net
```

在这里，我们看到 `/misc` 和 `/net` 上挂载了两个 `autofs` 文件系统。这些虚拟文件系统分别连接到 PID 为 8359 和 8372 的自动挂载进程。由 `/etc/init.d/autofs` 脚本运行的自动挂载命令可以在 `ps` 输出中“看到”。`auto.misc` 是一个普通的映射文件，而 `auto.net` 是一个可执行程序。这些映射在下文中会有详细描述。

## 主文件 (master file)

主文件列出了应该挂载 `autofs` 文件系统的目录，并为每个目录关联一个映射。除了提供映射名称根目录外，你还可以通过 `mount` 命令使用的 `-` 格式提供额外选项。这些选项将适用于任何条目。

- 7. 不要混淆 `autofs` 脚本。它们（脚本与内核）之间的关系是，脚本告诉内核如何配置文件系统。

Linux 的习惯与 Sun 的不同之处，主文件中的选项与映射的选项是累积的；两组选项都会被处理用于挂载。系统自动挂载信息的来源由 `/etc/nsswitch.conf` 中的 `automount` 字段指定。有关 `nsswitch.conf` 文件的更多信息，请参见第 498 页的“优先考虑管理信息的源”。

一个使用下一节所示映射文件的简单主文件看起来如下：

| 目录 | 映射 | 选项 |
| :--- | :--- | :--- |
| /chimchim | /etc/auto.chim | -secure,hard,bg.intr |

主文件可以用通过 NIS 共享的版本替换或增强。系统自动挂载信息的来源由 `/etc/nsswitch.conf` 中的 `automount` 字段指定。

## 映射文件 (Map files)

其他系统上的映射文件（被称为“间接映射”）在一个公共目录下方自动挂载多个文件系统。目录的路径在主文件中指定，而不是在映射中。例如，对于挂载在 `/chimchim` 下的文件系统，映射可能如下：

```text
users /chimchim/devel -soft,nfsproto=3 chimchim/devel
info -ro chimchim/info
```
