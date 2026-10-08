
Linux 提供了多种工具来访问连接到网络的远程文件。网络文件系统 (`NFS`) 允许你连接并直接访问位于另一台机器上的资源，如文件或 CD-ROM 等设备。网络信息服务 (`NIS`) 为网络上的所有系统维护配置文件。通过 Samba，你可以将 Microsoft Windows 网络上的 Windows 客户端连接到由 Linux Samba 服务器控制的共享文件、系统和打印机（见第 37 章）。

## 网络文件系统：NFS 和 `/etc/exports`

`NFS` 允许你将远程计算机上的文件系统挂载到你的系统中，就像它是本地系统一样。你可以直接访问该远程文件系统上的任何文件。这种方法的优点是允许网络上的不同系统访问相同的文件，而无需每个系统都保留自己的副本。远程文件系统上只有一份副本，每台计算机都可以访问它。你可以在网站 `nfs.sourceforge.net` 了解更多关于 `NFS` 的信息。

注意

基于 BSD Unix 的 Macintosh 电脑 Mac OS X 现在支持使用 `NFS` 进行文件共享。要使用旧版 Apple 操作系统访问 Apple 文件系统和打印机，你可以使用 `Netatalk`。`Netatalk` 在 Unix 和 Linux 系统上实现了经典的 AppleTalk 和 ShareIP 网络协议。目前的 `Netatalk` 网站是 `netatalk.sourceforge.net`，包含指向 FAQ 和 HOW-TO 部分的链接。

## NFS 守护进程

`NFS` 运行在 TCP/IP 网络上。持有文件系统的远程计算机向网络上的其他计算机提供服务。它是通过导出文件系统来实现的，这需要在名为 `/etc/exports` 的 `NFS` 配置文件中创建条目，并运行多个守护进程以支持其他系统的访问。这些包括 `rpc.mountd`、`rpc.nfsd` 和 `rpc.portmapper`。对你的 `NFS` 服务器的访问可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件进行控制。`NFS` 守护进程如下：

- `rpc.nfsd` 接收来自远程系统的 `NFS` 请求并将其翻译对本地系统的请求
- `rpc.mountd` 执行请求的挂载和卸载操作
- `rpc.portmapper` 将远程请求映射到相应的 `NFS` 守护进程
- `rpc.quotad` 提供用户磁盘配额管理
- `rpc.statd` 在远程主机启动时提供锁定服务
- `rpc.lockd` 为已宕机的系统处理锁定恢复

注意

建议仅在本地安全网络上使用 `NFS`。如果在互联网上使用，`NFS` 将导致你的系统条目面临不安全的访问。

## 启动和停止 NFS

在 Red Hat 上，你可以使用 `/etc/rc.d/nfs` 服务来启动和关闭 `NFS` 守护进程，你可以使用 `service` 命令调用它。要让 `NFS` 自动启动，可以使用 `chkconfig` 或 `redhat-config-services` 工具指定其运行的级别。以下示例将在 Red Hat 的级别 3 和 5 自动启动 `NFS`：

```
chkconfig --level 3 nfs on
```

`nfs` 将使用 `portmapper`、`nfsd`、`mount` 和 `quotad` 守护进程。要启用 `NFS` 锁定，使用 `nflock` 脚本。这将启动 `statd` 和 `lockd` 守护进程。`NFS` 锁定为远程主机发生崩溃的操作提供了更好的恢复。要查看 `NFS` 是否正在运行，可以使用带有 `-p` 选项的 `rpcinfo` 命令。你应该看到 `mount` 和 `nfs` 条目。如果没有，说明 `NFS` 未在运行。

## 分析工具

`NFS` 软件包还包含了一些分析工具，你可以通过这些工具衡量 `NFS` 的性能。`nfsstone` 会在服务器上生成指定测试的数据。`nfsrun` 将运行各种负载的 `nfsstone`。使用 `nfsnum` 生成数据图表，`nfsstat` 显示关于 `NFS` 客户端和服务器当前信息。你可以将请求缩小到网络活动、`NFS` 协议和服务器使用。

## 使用 Red Hat 配置 NFS

与其手动挂载和配置 `NFS`，可以使用 Red Hat 配置 (`redhat-config-nfs`)。从 Settings 选择 `NFS Server`。这会打开 `NFS` 配置窗口。确保你的 `NFS` 软件已安装 (`redhat-config-packages`) 并且服务器正在运行 (`redhat-config-services`)。

要添加共享目录，点击 `Add` 按钮打开 `NFS` 共享对话框，如图 36-1。你可以输入要共享的目录并指定访问权限。在 `General Options` 选项卡中，你可以设置基本安全以及锁定或立即同步写入的功能。设置 `Sync` 选项。在 `Access` 选项卡中，你可以将用户视为本地 root 用户或具有特定用户组 ID 的匿名用户。点击 `OK`，条目将列在 `NFS` 配置窗口中。更改在点击 `Apply` 后生效。以后可以通过选择条目并点击 `Properties` 更改这些设置中的任何一项。要保存你的设置，点击。图 36-1 显示了下一节描述的 `/etc/exports` 文件生成的条目：

```
/home/foodstuff/           ro, sync)
/mnt/cdrom             (ro, sync)
```

`Basic`、`General Options` 和 `Access` 选项卡中设置的选项每个条目显示。例如，读取访问为 `ro` 或读写访问为 `rw`。完整列表请查看 `NFS` 配置帮助文档。选项位于表 36-1。

## NFS 配置：`/etc/exports`

`/etc/exports` 文件中的条目指定要导出的文件系统以及可以访问它的网络主机。对于每个条目，它进入在主机系统上的挂载点（目录）。后面是可以访问此项的主机列表以及选项。每个主机后面可以是逗号分隔的选项列表。例如，你可能希望给一个主机只读访问权限，给另一个读写访问权限。如果选项以 `*` 开头，则适用于任何主机。表 36-1 提供了选项列表。`/etc/exports` 中的条目格式所示：

```
directory-pathname host-designation(options)
```

## NFS 主机条目

你可以为同一个目录设置多个主机条目，每个条目对该目录都有访问权限：

```
directory-pathname host(options) host(options) host(options)
```

在指定主机时，你有很大的灵活性。对于域内的主机，你可以使用主机名，而对于外部，可以使用完全限定域名。你也可以使用主机的 IP 地址。与其只指定一个，你可以引用特定域内的所有主机，允许通过条目访问。实现此点的简单方法是在主机段使用 `*`，后跟域名，例如 `*.mynetwork.com` 代表 `mynetwork.com` 域中的所有主机。与其域名，你可以使用 CIDR 格式的 IP 地址或指定网络来识别 IP 地址范围。你也可以使用 `NIS` 组名来引用一组主机。`NIS` 网络组名以前有 `@` 符号。

```
directory host(options)
directory *(options)
directory *.domain(options)
directory 192.168.1.0/255.255.255.0(options)
directory @netgroup(options)
```

## NFS 选项

`/etc/exports` 中的选项作为控制导出目录访问的权限。只读访问通过 `ro` 选项设置，读写通过 `rw` 选项设置。`sync` 和 `async` 选项指定写入操作是立即执行 (`sync`) 还是当服务器准备好处理时执行 (`async`)。默认情况下，执行写入请求 (`wdelay`)。这可能会降低性能。你可以用 `no_delay` 覆盖此设置并在请求时执行写入。如果导出了两个目录，其中一个是子目录，则除非显式挂载，否则子目录是不可的 (`hide`)。换句话说，挂载父目录不会使子目录可用。子目录在挂载之前保持隐藏。你可以通过 `no_hide` 选项绕过这一点（尽管这会导致文件系统出现问题）。如果导出的目录实际上较大文件系统中的子目录，则会检查其父目录以确保子目录是有效目录 (`subtree_check`)。该选项对于只读文件系统效果良好，但对于可写入的文件系统可能会产生问题，因为文件名和目录可以更改。你也可以通过 `no_subtree_check` 选项检查此项。

| `insecure` | 关闭安全选项。 |
| --- | --- |
| `ro` | 仅允许读取访问。这是默认值。 |
| `rw` | 允许读写访问。 |
| `sync` | 在请求时执行所有写入。这是默认值。 |
| `async` | 在服务器准备就绪时执行所有写入。 |
| `no_wdelay` | 立即执行写入，不检查它们是否相关。 |
| `wdelay` | 检查写入是否相关，如果是，则等待一起执行。可能会降低性能。这是默认值。 |
| `hide` | 自动隐藏作为另一个导出目录的子目录的导出目录。该子目录必须显式挂载才能被访问。挂载父目录不会允许访问。这是默认值。 |
| `no_hide` | 不隐藏作为另一个导出目录的子目录的导出目录（`hide` 的反选项）。仅对单主机有效，且可能不可靠。 |
| `subtree_check` | 检查文件系统中的父目录以验证导出的子目录。这是默认值。 |
| `no_subtree_check` | 不检查文件系统中的父目录以验证导出的子目录。 |
| `insecure_locks` | 不需要锁定请求的身份验证。用于旧版本的 `NFS`。 |
| `User ID Mapping` | 描述 |
| `all_squash` | 将所有 UID 和 GID 映射到匿名用户。适用于 `NFS` 导出的公共 FTP 目录、新闻堆叠目录等。 |
| `no_all_squash` | `all_squash` 的反选项。这是默认值。 |
| `root_squash` | 将来自远程 root 用户的请求映射到匿名 UID/GID。这是默认值。 |
| `no_root_squash` | 关闭 root 压缩。允许 root 用户以远程 root 身份进行访问。 |
| `anonuid anongid` | 显式设置用于 `all_squash` 和 `root_squash` 选项的匿名账户的 UID 和 GID。默认值是 `nobody` 和 `nogroup`。 |

## NFS 用户级访问

除了通用选项外，还有适用于用户级访问的选项。作为一种安全措施，`NFS` 服务器会将客户端的 root 用户视为匿名用户。这被称为“用户压缩”（squashing）。对于客户端用户而言，压缩防止客户端尝试伪装成 `NFS` 服务器的 root 用户。如果你希望客户端的 root 用户对 `NFS` 服务器拥有 root 级控制权，可以指定 `no_root_squash` 选项。为了防止任何客户端尝试伪装成 `NFS` 服务器，可以将其分类为匿名用户（`all_squash` 选项）。此类匿名用户将仅访问匿名组部分的目录和文件。

通常，如果客户端系统上的用户在 `NFS` 服务器上拥有用户账户，该用户就可以挂载并访问其在 `NFS` 服务器上的文件。`NFS` 要求用户在两个系统上的 User ID 相同。如果不是如此，他/她将被视为两个不同的用户。为了解决这个问题，可以使用 `NIS` 服务，将 User ID 信息维护在一个处，即 `NIS` 密码文件（请见下一节有关 `NIS` 的信息）。

## NFS `/etc/exports` 示例

此处显示了 `/etc/exports` 文件的条目示例。所有主机对挂载在 `/pub` 通用名下用于公共访问的文件系统具有只读权限。然而，用户被视为匿名用户（`all_squash`）。对于 `lizard.mytrek.com` 计算机，挂载在 `/home/foodstuff` 目录下的文件系统具有读写权限。下一个条目允许 `rabbit.mytrek.com` 访问 `NFS` 服务器的刻驱，但仅使用读取权限。最后一条目允许对 `/home/richlip` 进行安全访问。

```
/etc/exports
/pub * (ro, insecure, all_squash, sync)
/lizard.mytrek.com (rw, sync)
/mnt/cdrom rabbit.mytrek.com (ro, sync)
/home/richlip * (secure, sync)
```

## 应用更改

每当系统启动 `NFS` 服务器时（通常在系统启动时），`/etc/exports` 文件就会被读取，并根据文件指定这些目录。当一个目录被导出时，`/var/lib/nfs/stab` 文件中会为其创建一个条目。这是 `NFS` 读取并使用以执行实际导出的文件。条目从 `/etc/exports` 读取，相应的条目建立在 `/var/lib/nfs/stab` 中。`stab` 文件维护了实际导出的列表。

如果你想在不重启的情况下导出 `/etc/exports` 文件中的条目，可以使用带有 `-a` 选项的 `exports` 命令。使用 `-v` 选项来显示 `NFS` 正在执行的操作很有帮助。使用相同的命令可以影响 `/etc/exports` 文件的任何更改。

```
exports -a -v
```

如果你对 `/var/lib/nfs/stab` 文件进行了更改，可以使用 `-r` 选项重新导出其条目。`-r` 选项将 `/var/lib/nfs/stab` 文件与 `/etc/exports` 条目重新同步，移除任何其他导出或具有不同选项的导出。

```
exports -r -v
```

要同时导出新增的条目并重新导出更改的条目，可以组合 `-r` 和 `-a` 选项。

```
exports -r -a -v
```

## 手动导出文件系统

你可以使用 `exports` 命令手动导出文件系统，而不是在 `/etc/exports` 文件中使用条目定义。导出条目将被添加到 `/var/lib/nfs/stab`。

```bash
iptables -A INPUT -i eth0 -p 111 -j DENY
iptables -A INPUT -i eth0 -p 2049 -j DENY
```

要为本地网络启用 `NFS`，你必须允许数据包分片。假设 `eth0` 是本地网络使用的设备，可以使用以下示例：

```
iptables -A INPUT -i eth0 -f -j ACCEPT
```

远程主机上的 root 用户可以尝试以具有 root 权限的 root 用户访问远程 `NFS` 服务器。`root_squash` 选项（默认选项）会自动将远程用户更改为 `nobody`（匿名）用户。

## 挂载 NFS 文件系统：NFS 客户端

一旦 `NFS` 让目录对不同主机可用，这些主机就可以在自己的系统上挂载这些目录并访问它们。该主机需要能够以 `NFS` 客户端的身份运行。当前的 Linux 内核已经内置了所有 `NFS` 功能。这意味着任何 `NFS` 客户端都可以通过简单的操作挂载其具有访问权限的远程目录。

## 自动挂载 NFS：`/etc/fstab`

你可以通过 `/etc/fstab` 中的条目或显式挂载命令来挂载 `NFS` 目录。你可以通过在 `/etc/fstab` 文件中为其放置条目来实现 `NFS` 文件系统的自动挂载。`/etc/fstab` 中的条目挂载类型为 `NFS`。后面是其所在计算机的文件系统名称，然后是挂载该目录的路径。它们之间用冒号分隔：`rabbit.trek.com:home/project` 指定了 `rabbit.trek.com` 计算机上挂载在 `/home/project` 的文件系统。`/etc/fstab` 文件中的 `NFS` 条目如下。请注意文件类型为 `nfs`。

```
host:remote-directory  local-directory  nfs  options  0 0
```

你还可以在你的 `NFS` 条目中包含 `NFS` 特有的选项。你可以指定数据报往返传输的大小，以及你等待主机响应的时间。你还可以指定文件系统是硬挂载（hard-mounted）还是软挂载（soft-mounted）。对于硬挂载的文件系统，如果由于某种原因远程系统未响应，你的计算机将持续尝试连接。对于软挂载的文件系统，在指定的间隔后，它将放弃连接并发出错误消息。硬挂载是默认选项。如果硬挂载尝试持续失败，它将在不断尝试实现挂载时向用户做出响应。因此，软挂载可能是更好的选择，因为它们会简单停止持续失败的挂载。参见表 36-2 和 `mount` 手页，其中包含了这些 `NFS` 客户端选项。该条目与之前指示 `NFS` 选项不同。

以下是一个 `NFS` 条目的示例。远程是 `rabbit.trek.com`，文件系统挂载在 `/home/projects`。该文件系统必须挂载在本地系统作为 `/home/dylan/projects` 目录。`NFS` 类型为 `nfs`，时间指定为响应的二十十分之一（秒）。该挂载是软挂载，可以被 `NFS` 中断。

```
rabbit.trek.com:/home/projects /home/dylan/projects  nfs  soft,intr,timeo=20
```

## 手动挂载 NFS：`mount`

你也可以使用 `mount` 命令配合 `-t nfs` 选项显式挂载 `NFS` 文件系统。要显式挂载之前的条目，请使用以下命令：

```bash
mount -t nfs -o soft,intr,time=20 rabbit.mytrek.com:/home/projects /home/dylan/projects
```

你可以选择使用 `mount` 命令挂载 `NFS` 目录。你可以像这里一样指定本地挂载点或远程主机和目录：

```bash
mount /home/dylan/projects
mount rabbit.mytrek.com:home/projects
```

注意

在 Red Hat 系统上，你还可以通过 `/etc/rc.d/init.d/netfs` 脚本同时挂载和卸载 `NFS` 文件系统，通过 `service` 命令调用它。该脚本读取 `/etc/fstab` 文件中的 `NFS` 条目，并它们来挂载和卸载远程目录。使用 `stop` 参数停止文件系统，使用 `start restart` 参数重新挂载文件系统。

## 按需挂载 NFS：`autofofs`
