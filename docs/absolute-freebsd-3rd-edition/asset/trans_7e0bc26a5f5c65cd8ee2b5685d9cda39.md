

使用 zfs(8) 管理 NFS 既有优点也有缺点。你可以基于每个数据集来配置 NFS，并且在每次更改后都不需要手动重启 mountd(8)。命令行配置更容易自动化，而且许多人觉得打字也更简单。

使用 `sharenfs` 属性来启用、禁用和配置 NFS 导出。将此属性设置为 *on* 以全局共享该数据集及其所有后代。这相当于在 `/etc/exports` 中单独列出该数据集。如果没有其他访问控制措施（例如防火墙），世界上任何人都可以挂载此数据集或其任何子项，且不受限制，也没有选项。

```
# zfs set sharenfs=on zroot/home
```

同样，将其设置为 *off* 可以取消共享该数据集。

不过，你很可能希望导出时包含一些 NFS 选项。将 `sharenfs` 设置为该数据集所需的选项。此示例设置了 `maproot` 用户，并将客户端限制在我的本地网络中。请将选项放在引号内。

```
# zfs set sharenfs="-network 203.0.113.0/24 -maproot=nfsroot" zroot/home
```

使用 ZFS 管理 NFS 导出的问题在于，所有允许的主机都获得相同的选项。也就是说，如果你大多数主机都需要使用 `-maproot=nfsroot` 来挂载 `/home`，但你有一台主机需要 root 以 root 身份挂载该数据集，那么你就无法使用 ZFS 属性。同样，你只能使用 ZFS 属性定义一个允许的网络。

## 启用 NFS 客户端

配置 NFS 客户端要简单得多。在 `/etc/rc.conf` 中，输入：

```
nfs_client_enable="YES"
```

你可以重启或运行 `service nfsclient start`。两者都会启动 NFS 客户端功能。

## 显示可用挂载

NFS 客户端的一个显而易见的问题是：“我可以从该服务器挂载什么？” showmount(8) 命令列出对客户端可用的所有导出。提供 `-e` 标志和 NFS 服务器的名称。在这里，我问 storm 服务器提供哪些导出：

```
# showmount -e storm
Exports list on storm:
/usr/home              203.0.113.0
```

此客户端允许在允许网络 203.0.113.0 的规则下挂载 `/usr/home`。

运行 showmount(8) 不提供任何服务器端选项，例如 `-maproot`。这些详细信息对客户端来说并不易得，尽管 touch(1) 可以让你轻松测试只读导出。

## 挂载导出

现在你可以挂载由 NFS 服务器导出的目录或文件系统。不再使用设备名称，而是使用 NFS 服务器的主机名和你想挂载的目录。例如，要将我的 storm 服务器上的 `/home/mwlucas` 目录挂载到 `/mnt` 目录，我会运行：

```
# mount storm:/usr/home/mwlucas /mnt
```

之后，使用 df(1) 测试你的挂载。

```
# df -h
Filesystem             Size  Used Avail Capacity  Mounted on
--snip--
storm:/usr/home       891G  2.7G  888G   0%      /mnt
```

NFS 挂载的目录显示为普通分区，我可以随意在其中读写文件。

## NFS 挂载选项

FreeBSD 使用保守的 NFS 默认值，以便它可以与任何类 Unix 操作系统互操作。你可以使用挂载选项来调整 FreeBSD 如何挂载 NFS 导出。使用这些选项在命令行中使用 `-o` 或添加到 `/etc/fstab` 条目中。

如果你需要访问仅支持 UDP 的 NFS 服务器，请使用挂载选项 `udp` 以使用 UDP 而不是默认的 TCP。

程序期望文件系统不会消失，但当你使用 NFS 时，服务器有可能从网络中消失。这会使客户端上试图访问 NFS 文件系统的程序永远挂起。通过使你的 NFS 挂载*可中断*，你可以使用 CTRL-C 中断挂起在不可用 NFS 挂载上的进程。使用 `intr` 设置可中断性。

通过使用软挂载，FreeBSD 将通知程序它们正在处理的文件不再可用。程序如何处理这些信息取决于程序本身，但它们将不再永远挂起。使用 `soft` 选项启用软挂载。

如果你想要一个只读挂载，请使用 `ro` 挂载选项。

把所有东西放在一起，我可能会将我的主目录挂载为一个可中断的软挂载。

```
# mount -o soft,intr storm:/usr/home/mwlucas /mnt
```

我可以这样将其添加到 `/etc/fstab` 中：

| 设备 | 挂载点 | 文件系统 | 选项 | 转储 | 通过 |
| :----- | :---------- | :--------- | :----- | :-: | ---: |
| storm:/usr/home/mwlucas | /mnt | nfs | rw,soft,intr | 0 | 0 |

虽然 NFS 对于简单用途来说相当直接，但你可能会花费许多小时来调整、调优和增强它。如果你希望构建复杂的 NFS 环境，不要完全依赖这份简短的介绍，而是花时间在相关主题的一本好书上。

现在，让我们看看如何读取 Windows 共享。

## 通用 Internet 文件系统

如果你在一个典型的办公室网络中，标准的网络文件共享协议是微软的*通用 Internet 文件系统* (CIFS)。你可能知道 CIFS 是服务器消息块 (SMB)、“网上邻居”或“为什么我无法挂载那个驱动器？”。虽然最初仅由 Microsoft Windows 系统提供，但此协议已经成为某种伪标准。

FreeBSD 包含 smbutil(8) 程序，用于作为 CIFS 客户端查找、挂载和使用 CIFS 共享。FreeBSD 的基础系统中不包含 CIFS 服务器，但开源 CIFS 服务器 Samba (https://www.samba.org/) 在 FreeBSD 上运行良好。

使用 FreeBSD 的 CIFS 支持与现有的 Microsoft 基础设施互操作。不要部署 CIFS 来支持类 Unix 系统。

## 先决条件

在开始处理 Microsoft 文件共享之前，请收集有关你的 Windows 网络的以下信息：

- 工作组或 Windows 域名
- 有效的 Windows 用户名和密码
- Windows DNS 服务器的 IP 地址

## 内核支持

FreeBSD 使用几个内核模块来支持 CIFS。`smbfs.ko` 模块支持基本的 CIFS 操作。`libmbchain.ko` 和 `libiconv.ko` 模块提供支持功能，并在你加载 `smbfs.ko` 时自动加载。你可以在内核中静态编译这些模块，如下所示：

```
options NETSMB
options LIBMBCHAIN
options LIBICONV
options SMBFS
```

你可以在启动时通过 boot/loader.conf 条目自动加载这些模块。

```
smbfs_load=YES
```

现在你可以配置 CIFS 了。

## 配置 CIFS

CIFS 依赖于一个配置文件，即 `$HOME/.nsmbrc` 或 `/etc/nsmb.conf`。`/etc/nsmb.conf` 中的所有设置都覆盖用户主目录中的设置。配置文件由方括号中的标签分成各个部分。例如，适用于每个 CIFS 连接的设置位于 `[default]` 部分。创建你自己的部分来指定服务器、用户和共享，格式如下之一：

```
[servername]
[servername:username]
[servername:username:sharename]
```

适用于整个服务器的信息放入以服务器命名的部分。适用于特定用户的信息保留在用户名部分中，而仅适用于单个共享的信息保留在包含共享名称的部分中。如果你没有更具体的按用户或按共享的信息，你可以将所有共享的信息归并到一个普通的 `[servername]` 条目下。

配置条目使用 CIFS 系统的值——例如，Bert 的 Windows 用户名是 *bertjw*，但他的 FreeBSD 用户名是 *xistence*，所以我在 `nsmb.conf` 中使用 *bertjw*。

## nsmb.conf 关键字

在适当的部分下，使用关键字和值来指定 `nsmb.conf` 配置。例如，服务器有 IP 地址，而用户没有，所以你在服务器部分中只使用 IP 地址分配。要使用关键字，使用等号分配值，如 `keyword=value`。以下是常见关键字；完整列表请参见 `nsmb.conf`(5)。

### workgroup=string

workgroup 关键字指定你要访问的 Windows 域或工作组的名称。这通常是一个用于所有服务器的默认设置。

### addr=a.b.c.d

`addr` 关键字设置 CIFS 服务器的 IP 地址。此关键字只能出现在普通的 `[servername]` 标签下。如果你有可用的 CIFS 名称解析，你不应该需要这个，但现实有时会有所不同。

### nbns=a.b.c.d

`nbns` 关键字设置 NetBIOS (WINS) 名称服务器的 IP 地址。你可以将此行放在默认部分中，或放在特定服务器下。如果你有 Active Directory（基于 DNS），你可以使用 DNS 主机名。然而，添加 WINS 服务器不会损害你的配置，并且有助于测试基本的 CIFS 设置。

### password=string

`password` 关键字为用户或共享设置明文密码。如果你必须在 `/etc/nsmb.conf` 中存储密码，请绝对确保只有 root 可以读取该文件。在多用户系统中，在 `$HOME/.nsmbrc` 中存储密码是一个坏主意。

你可以使用 `smbutil crypt` 混淆你的 Windows 密码，生成一个你可以用于此关键字的字符串。混淆的字符串前面有两个美元符号 ($$)。虽然这有助于防止某人意外发现密码，但恶意用户可以轻松解混淆。

```
# smbutil crypt superSecretPassword
$$1624a53302a6d
```

如果服务器需要访问 CIFS 共享以完成其例行工作，请不要使用你的账户。请 Windows 团队为你的服务器申请一个账户，这样你的账户问题就不会中断服务器功能。

## 示例配置

