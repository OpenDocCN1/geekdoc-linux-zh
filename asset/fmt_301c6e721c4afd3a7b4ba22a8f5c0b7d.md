
然后，在 `hosts.allow` 文件中，您可以为每个服务添加条目：

```
mountd: 192.168.0.0/255.255.255.0, 10.0.0.43
rquotad: 192.168.0.0/255.255.255.0, 10.0.0.43
statd: 192.168.0.0/255.255.255.0, 10.0.0.43
lockd: 192.168.0.0/255.255.255.0, 10.0.0.43
```

## Netfilter 规则

您可以使用 Netfilter 来检查来自特定主机对 NFS 服务使用的端口的传输，从而进一步控制访问。请参阅第 19 章了解 Netfilter 的说明。端口映射器使用端口 111，`nfsd` 使用 2049。如果您有一个具有 Internet 连接的私有网络，并且想要保护它免受 Internet 的侵害，Netfilter 会很有帮助。通常，一个特定的网络设备，例如以太网卡，专门用于 Internet 连接。

以下示例假设设备 `eth1` 连接到 Internet。任何尝试访问端口 111 和 2049 的数据包都会被拒绝。

```
iptables -A INPUT -i eth1 -p 111 -j DENY
iptables -A INPUT -i eth1 -p 2049 -j DENY
```

要为本地网络启用 NFS，您将必须允许数据包分片。假设 `eth0` 是用于本地网络的设备，您可以使用以下示例：

```
iptables -A INPUT -i eth0 -f -j ACCEPT
```

> 注意 远程主机上的 root 用户可以尝试以 root 用户身份并使用 root 级权限访问远程 NFS 服务器。`root_squash` 选项（默认）会自动将远程 root 用户更改为 `nobody`（匿名）用户。

## 挂载 NFS 文件系统：NFS 客户端

一旦 NFS 将目录提供给不同的主机，这些主机就可以在自己的系统上挂载这些目录并访问它们。主机需要能够作为 NFS 客户端运行。当前所有 Linux 内核都内置了 NFS 客户端功能。这意味着任何 NFS 客户端都可以通过执行简单的挂载操作来挂载其有权访问的远程 NFS 目录。

## 自动挂载 NFS：/etc/fstab

您可以通过 `/etc/fstab` 文件中的条目或通过显式的 `mount` 命令来挂载 NFS 目录。您可以通过在 `/etc/fstab` 文件中为它们放置条目，使 NFS 文件系统自动挂载。`/etc/fstab` 文件中的 NFS 条目的挂载类型为 NFS。NFS 文件系统名称由其所在的计算机的主机名，后跟其挂载的目录的路径名组成。两者用冒号分隔。例如，`rabbit.trek.com/home/project` 指定在 `rabbit.trek.com` 计算机上挂载在 `/home/project` 的文件系统。`/etc/fstab` 文件中 NFS 条目的格式如下。请注意文件类型为 `nfs`。

```
host:remote-directory   local-directory   nfs   options   0   0
```

您还可以包含多个 NFS 特定的挂载选项与您的 NFS 条目一起使用。您可以指定发送和接收的数据报的大小，以及您的计算机等待主机系统响应的时间。您还可以指定文件系统是要硬挂载还是软挂载。对于硬挂载文件系统，如果由于某种原因远程系统未能响应，您的计算机将不断尝试建立联系。软挂载文件系统在指定间隔后放弃尝试建立联系并发出错误消息。硬挂载是默认值。持续失败的硬挂载尝试的系统在不断尝试实现挂载时将停止响应用户输入。因此，软挂载可能更可取，因为它们会简单地停止尝试持续失败的挂载。表 36-2 和 `mount` 的手册页包含这些 NFS 客户端选项的列表。它们与前面指出的 NFS 服务器选项不同。

下面是一个 NFS 条目的示例。远程系统是 `rabbit.mytrek.com`，文件系统挂载在 `/home/projects`。此文件系统在本地系统上挂载为 `/home/dylan/projects` 目录。`/home/dylan/projects` 目录必须已在本地系统上创建。系统类型为 NFS，`timeo` 选项指定本地系统等待响应的时间最长为 20 个十分之一秒（两秒）。挂载为软挂载，并且可以被 NFS 中断。

```
rabbit.mytrek.com:/home/projects   /home/dylan/projects   nfs   soft,intr,timeo=20
```

## 手动挂载 NFS：mount

您也可以使用 `mount` 命令并带 `-t nfs` 选项来显式挂载 NFS 文件系统。要显式挂载之前的条目，请使用以下命令：

```
# mount -t nfs -o soft,intr,timeo=20 \
    rabbit.mytrek.com:/home/projects   /home/dylan/projects
```

当然，您也可以使用 `umount` 命令卸载 NFS 目录。您可以指定本地挂载点或远程主机和目录，如下所示：

```
umount /home/dylan/projects
umount rabbit.mytrek.com:/home/projects
```

> 注意 在 Red Hat 系统上，你也可以使用 `/etc/rc.d/init.d/netscript` 一次性挂载和卸载所有 NFS 文件系统，该脚本可通过 `service` 命令调用。此脚本读取 `/etc/fstab` 文件中的 NFS 条目，使用它们来挂载和卸载 NFS 远程目录。使用 `stop` 参数会卸载文件系统，而使用 `start` 参数则会重新挂载它们。`restart` 参数会先卸载然后再重新挂载文件系统。

## 按需挂载 NFS：autofs

你也可以使用 `automount` 服务 `autofs` 来挂载 NFS 文件系统。这需要在客户端进行额外的配置。`autofs` 服务仅在你尝试访问文件系统时才挂载它。对指定目录的目录更改操作（`cd`）会触发挂载操作，此时挂载远程文件系统。

`autofs` 服务使用主文件来列出映射文件进行配置，而映射文件则列出要挂载的文件系统。`/etc/auto.master` 文件是 `autofs` 主文件。主文件会列出可以挂载文件系统的根路径名以及每个路径名对应的映射文件。映射文件随后会列出键（子目录）、挂载选项以及可在该根路径名目录中挂载的文件系统。在某些发行版中，`/auto` 目录已实现为自动挂载文件系统的根路径名。你也可以在 `/etc/auto.master` 文件中添加自己的条目以及自己的映射文件。 你会发现 `/etc/auto.master` 文件包含以下用于 `/auto` 目录的条目，其映射文件为 `auto.misc`：

```
/auto    auto.misc    --timeout 60
```

在映射文件之后，你可以添加选项，如前例所示。`timeout` 选项指定在尝试自动卸载前等待的非活动秒数。

在映射文件中，你列出键、挂载选项和要挂载的文件系统。键将是文件系统在本地系统上挂载的子目录。例如，要将 `rabbit.mytrek.com` 主机上的 `/home/projects` 目录挂载到 `/auto/projects` 目录，你可以使用以下条目：

```
projects  soft,intr,timeo=20  rabbit.mytrek.com:/home/projects
```

你也可以在主文件中为 NFS 文件系统创建新条目，如下所示：

```
/myprojects    auto.myprojects    --timeout 60
```

然后你将创建 `/etc/auto.myprojects` 文件并在其中放置 NFS 文件系统挂载的条目，如下所示：

```
dylan    soft,intr,rw    rabbit.mytrek.com:/home/projects
newgame  soft,intr,ro    lizard.mytrek.com:/home/supergame
```

> 注意 `autofs` 服务可用于任何文件系统，包括软盘和 CD-ROM。参见第 30 章。

| Options | Description |

|---|---|

| rsize=n | NFS 从 NFS 服务器读取文件时使用的字节数。默认值为 1,024 字节。设置为 8,192 可大大提高性能。 |

| wsize=n | NFS 向 NFS 服务器写入文件时使用的字节数。默认值为 1,024 字节。设置为 8,192 可大大提高性能。 |

| timeo=n | 超时后发送第一次重传前的值，单位为十分之一秒。默认值是零点七秒。 |

| retry=n | 在放弃之前重试 NFS 挂载操作的分钟数。默认值为 10,000 分钟（一周）。 |

| retrans=n | NFS 挂载操作在发生主要超时前重传或次要超时的次数（默认为 3）。届时，连接将被取消或显示“服务器无响应”消息。 |

| soft | 使用软挂载挂载系统。 |

| hard | 使用硬挂载挂载系统。这是默认值。 |
