

## 网络过滤规则

你可以进一步使用 Netfilter 来控制访问权限，通过检查从特定主机发出的、使用 NFS 服务端口的传输数据来进行限制。（关于 Netfilter 的详细说明请参见第 20 章。）portmapper 使用端口 111，nfsd 使用端口 2049。如果你拥有一个拥有互联网连接的私有网络，并希望保护它免受来自互联网的威胁，Netfilter 非常有用。通常，一个特定的网络设备（如以太网卡）会被专门用于互联网连接。以下示例假设设备 eth1 连接到互联网。任何试图在端口 111 或 2049 上进行访问的数据包都将被拒绝。

```
iptables -A INPUT -i eth1 -p 111 -j DENY
iptables -A INPUT -i eth1 -p 2049 -j DENY
```

为了在你的本地网络中启用 NFS，你必须允许数据包分片。假设 eth0 是用于本地网络的设备，你可以使用以下示例：

```
iptables -A INPUT -i eth0 -f -j ACCEPT
```

> **注意** 远程主机上的 root 用户可以尝试以 root 用户身份和 root 级别的权限访问远程 NFS 服务器。root_squash 选项（默认设置）会自动将远程 root 用户更改为 nobody（匿名）用户。

请查阅 `nfs` 手册页以获取关于 NFSv4 选项的信息。

## 挂载 NFS 文件系统：NFS 客户端

一旦 NFS 将目录提供给不同的主机，这些主机就可以在自己的系统上挂载这些目录并访问它们。该主机需要能够作为 NFS 客户端运行。当前的 Linux 内核都内置了 NFS 客户端功能。这意味着任何 NFS 客户端都可以通过执行简单的挂载操作来挂载其有权限访问的远程 NFS 目录。

## 自动挂载 NFS：/etc/fstab

你可以通过在 `/etc/fstab` 文件中添加条目或使用显式的 mount 命令来挂载 NFS 目录。通过在 `/etc/fstab` 文件中放置相应条目，可以让你的 NFS 文件系统自动挂载。`/etc/fstab` 文件中的 NFS 条目的挂载类型为 NFS。NFS 文件系统名称由存放该系统的计算机的主机名组成，后跟挂载该目录的路径名。两者之间用冒号分隔。例如，`rabbit.trek.com:/home/project` 指定了挂载在 `rabbit.trek.com` 计算机上 `/home/project` 位置的文件系统。`/etc/fstab` 文件中 NFS 条目的格式如下。请注意，文件类型是 `nfs`。

```
host:remote-directory local-directory nfs options 0 0
```

你还可以在 NFS 条目中包含多个 NFS 特定的挂载选项。你可以指定往返发送的数据报大小，以及你的计算机等待主机系统响应的时间。你还可以指定文件系统是采用硬挂载还是软挂载。对于硬挂载的文件系统，如果由于某种原因远程系统未能响应，你的计算机将不断尝试建立联系。软挂载的文件系统在经过指定间隔后，会停止尝试建立联系并发出错误消息。硬挂载是默认设置。持续失败的硬挂载尝试会导致系统停止响应用户输入，因为它会不断尝试实现挂载。因此，软挂载可能更优，因为它们只会简单停止尝试持续失败的挂载。表 38-2 以及 **mount** 的手册页列出了这些 NFS 客户端选项。它们与前面提到的 NFS 服务器选项不同。

以下是一个 NFS 条目的示例。远程系统是 **rabbit.mytrek.com**，文件系统挂载在 */home/projects*。该文件系统将在本地系统挂载为 */home/dylan/projects* 目录。*/home/dylan/projects* 目录必须在本地系统中预先创建。系统类型为 NFS，**timeo** 选项指定本地系统最多等待 20 个 0.1 秒（即 2 秒）以获取响应。该挂载为软挂载，且可被 NFS 中断。

```
rabbit.mytrek.com:/home/projects /home/dylan/projects nfs soft,intr,timeo=20
```

## 手动挂载 NFS：mount

你还可以使用带有 **-t nfs** 选项的 **mount** 命令显式地挂载 NFS 文件系统。对于 NFSv4 文件系统，你需要使用 **-t nfs4**。若要显式挂载上述条目，请使用以下命令：

```
# mount -t nfs -o soft,intr,timeo=20 \
rabbit.mytrek.com:/home/projects /home/dylan/projects
```

| 选项 | 描述 |
| :--- | :--- |
| **rsize=n** | NFS 从 NFS 服务器读取文件时使用的字节数。默认值为 1,024 字节。8,192 的大小可以极大提高性能。 |
| **wsize=n** | NFS 向 NFS 服务器写入文件时使用的字节数。默认值为 1,024 字节。8,192 的大小可以极大提高性能。 |
| **timeo=n** | 超时后发送第一次重传之前的 0.1 秒数值。默认值为 0.7 秒。 |
| **retry=n** | 在放弃 NFS 挂载操作前重试的分钟数。默认值为 10,000 分钟（一周）。 |
| **retrans=n** | NFS 挂载操作在发生主要超时之前的小超时或重传次数（默认为 3）。此时，连接将被取消，或显示“服务器无响应”消息。 |
| **soft** | 使用软挂载系统。 |
| **hard** | 使用硬挂载系统。这是默认设置。 |
| **intr** | 允许 NFS 中断文件操作并返回到调用程序。默认不允许中断文件操作。 |
| **bg** | 如果第一次挂载尝试超时，则在后台继续尝试挂载。默认是在不转入后台的情况下失败。 |
| **tcp** | 使用 TCP 协议而非默认的 UDP 协议挂载 NFS 文件系统。 |

**表 38-2 NFS 挂载选项**

当然，你可以使用 `umount` 命令卸载 NFS 目录。你可以指定本地挂载点，或者远程主机和目录，如下所示：

```
umount /home/dylan/projects
umount rabbit.mytrek.com:/home/projects
```

> **注意** 你还可以使用 `/etc/rc.d/init.d/netfs` 脚本一次性挂载和卸载所有的 NFS 文件系统，该脚本可以通过 `service` 命令调用。该脚本读取 `/etc/fstab` 文件中的 NFS 条目，并使用它们来挂载和卸载 NFS 远程目录。使用 `stop` 参数将卸载文件系统，使用 `start` 参数则重新挂载它们。`restart` 参数首先卸载，然后重新挂载文件系统。

## 按需挂载 NFS：autofs

你还可以使用自动挂载服务 `autofs` 来挂载 NFS 文件系统。这需要客户端进行额外的配置。`autofs` 服务只在你尝试访问文件系统时才进行挂载。更改目录操作（`cd`）进入指定目录将触发挂载操作，届时将挂载远程文件系统。

`autofs` 服务使用主文件配置以列出映射文件，而映射文件则列出要挂载的文件系统。`/etc/auto.master` 文件是 `autofs` 的主文件。主文件将列出可以挂载文件系统的根路径名，以及每个路径名对应的映射文件。映射文件随后列出键（子目录）、挂载选项以及可以在该根路径名目录中挂载的文件系统。在某些发行版中，`/auto` 目录已经作为自动挂载文件系统的根路径名实现。如果你愿意，可以在 `/etc/auto.master` 文件中添加你自己的文件系统以及你自己的映射文件。你会发现 `/etc/auto.master` 文件包含针对 `/auto` 目录的以下条目，并列出 `auto.misc` 作为其映射文件：

```
/auto auto.misc --timeout 60
```

在映射文件中，你可以添加选项，如前面的示例所示。`timeout` 选项指定在尝试自动卸载之前等待的非活动秒数。

在映射文件中，你列出键、挂载选项以及要挂载的文件系统。键将是本地系统中挂载该文件系统的子目录。例如，要将 `rabbit.mytrek.com` 主机上的 `/home/projects` 目录挂载到 `/auto/projects` 目录，你会使用以下条目：

```
projects soft,intr,timeo=20 rabbit.mytrek.com:/home/projects
```

你还可以在主文件中为 NFS 文件系统创建新条目，如下所示：

```
/myprojects auto.myprojects --timeout 60
```

然后，你将创建一个 `/etc/auto.myprojects` 文件，并在其中放置 NFS 文件系统挂载条目，如下例：

```
dylan soft,intr,rw rabbit.mytrek.com:/home/projects
newgame soft,intr,ro lizzard.mytrek.com:/home/supergame
```

