
这些预防措施的意图是好的，但它们的最终价值并没有看起来那么大。NFS 客户端上的 root 可以做它想做的事，因此文件永远不受保护。像 "bin" 和 "sys" 等系统登录经过 UID 映射，因此它们拥有的任何文件（系统文件的很大比例）都会受到攻击。UID 映射的唯一作用是防止访问由 root 所有且全球不可读或不可写的文件。

## Cookie 和无状态挂载

客户端在使用 NFS 文件系统之前必须显式挂载它，就像它必须挂载存储在本地磁盘上的文件系统一样。然而，由于 NFS 是无状态的，服务器不会跟踪哪些客户端挂载了每个文件系统。相反，服务器在成功协商结束后仅披露一个秘密的 "cookie"。该 cookie 向 NFS 服务器标识挂载的目录，并为客户端访问其内容提供方法。

在服务器上卸载并重新挂载文件系统通常会更改其 cookie。作为一个特殊情况，cookie 跨越重启存在，因此服务器崩溃后可以恢复之前的状态。但不要尝试对文件系统进行单用户模式，否则重启将撤销 cookie 并导致客户端无法访问它们挂载的文件，直到它们重新挂载或重启。

一旦客户端拥有了 Cookie，它就使用 RPC 协议对文件系统操作提出请求，例如创建文件或读取数据块。由于 NFS 是无状态的，服务器不在乎客户端之前是否发送过请求。特别是，客户端负责在删除自己的待写入数据副本之前确保服务器确认了写入请求。

## 共享文件系统的命名规范

不幸的是，此方案要求目录/锚点存在于所有客户端的根目录下。如果客户端从多个其他主机获取文件系统……（此处原文存在大量重复，已按要求处理），WebNFS 提供了一种挂载方法。

## 表 17.2 导出目录的设置位置

| 系统 | 导出信息 | 修改后的操作 |
| --- | --- | --- |
| Solaris | `/etc/dfs/dfstab` | 运行`shareall`。 |
| HP-UX | `/etc/exports` | 运行`/usr/sbin/exportfs -a`。 |
| Red Hat | `/etc/exports` | 运行`/usr/sbin/exportfs -a`。 |
| FreeBSD | `/etc/exports` | 向`mountd`发送 HUP信号。 |

NFS 处理文件系统的逻辑层。任何目录都可以被导出；它不必是挂载点或物理文件系统的根目录。然而，出于安全考虑，NFS 注意文件系统之间的边界，并要求对每个设备单独导出。例如，在具有`/users`分区的机器上，可以导出根目录而不导出`/users`。

客户端通常被允许挂载导出目录的子目录，尽管该协议并不要求此功能。例如，如果导出`/chimchim/users`，客户端可以只挂载`/chimchim/users`而忽略`users`目录的其他部分。大多数系统不允许你使用不同的选项导出子目录，但 Red Hat 是一个例外。

## `share` 命令和 `dfstab` 文件 (Solaris)

`/etc/dfs/dfstab`为每个导出的文件系统执行一次`share`命令。例如，一个服务器向主机 band 和 moon（band 具有 root 权限）共享`/chimchim/users`，并向 chimchim 和 radon 共享`/usr/share/man`，则`/etc/dfs/dfstab`文件将包含以下命令：

```
share -F nfs -o rw=band.xor:moon.xor,root=band.xor
	 /chimchim/users
share -F nfs -o rw=chimchim.xor:radaston.xor:/usr/share/man
```

在编辑`/etc/dfs/dfstab`后，记得运行`shareall`以使你的更改生效。注意，`shareall`只是运行`dfstab`文件中的命令，它不会取消共享你已移除的文件系统。表 17.3 列出了最常用的选项。

## 表 17.3 `share` 命令的选项 (Solaris)

| 选项 | 说明 |
| --- | --- |
| `ro` | 向所有人导出只读权限（不推荐） |
| `ro=/list` | 仅向列表中的主机导出只读权限 |
| `rw` | 向所有人导出读写权限（不推荐） |
| `rw=/list` | 仅向列表中的主机导出读写权限 |
| `root=/list` | 允许以 root 身份访问此文件系统的列表。否则，客户端的 root 访问等同于 "nobody"（通常为 UID -2）的访问。 |
| `anon=uid` | 指定映射到 root 的 UID；默认值是 "nobody" |
| `nosub` | 禁止客户端挂载导出目录的子目录 |
| `nosuid` | 防止通过 NFS 创建 setuid 和 setgid 文件 |

## 第 17 章 网络文件系统 495

每当为 `share` 选项调用列表时，它应该由表 17.4 所示条目的冒号分隔组组成，所有条目都是指定主机或主机组的方法。

## 表 17.4 `share` 命令的客户端规范

| 类型 | 语法 | 含义 |
| --- | --- | --- |
| 主机名 | `hostname` | 单个主机（如果使用 DNS，必须是完全限定的） |
| 网络组 | `groupname` | NIS 网络组；详情请见第 522 页 |
| DNS 域 | `.xxx,yyy` | 域内的任何主机 |
| IP 网络 | `@netname` | 定义在`/etc/networks`⁴ 中的网络名称 |

- a. 也接受 CIDR 类型的规范；例如，`@128.138.92/128/25`。

在表 17.4 关于主机名的部分值得重复的是：如果你使用 DNS，单个主机名必须是完全限定的，否则将被忽略。列表在每次查找期间从左到右检查，直到找到匹配项为止，因此否定项应放在它们要修改的更通用项之前。例如，该行：

```
share -F nfs -o rw=@128.138.243/24:cs.colorado /users
```

向 `cs.colorado` DNS 域内的所有主机导出`/users`的读写权限， 128.138.243 网络上的主机除外。

可以对某些客户端导出只读，对其他客户端导出读写：只需同时包含 `rw=` 和 `ro=` 选项即可。

`share(1M)` 手页记录了少量基础 NFS 选项。有关完整列表，请参考 `share_nfs(1M)` 手页。

## `exports` 命令和 `exports` 文件（HP-UX, Red Hat, FreeBSD）

`exports` 文件由最左列的导出目录列表组成，随后是相关选项和属性列表。例如，HP-UX 导出：

```
/chimchim/users -access=band:moon,root=band
/usr/share/man -access=xorasaurus:rastadon:moon,ro
```

允许机器 band 和 moon 挂载`/chimchim/users`，允许 band 从 root 权限访问文件系统。此外，允许机器 band 和 moon 挂载`/usr/share/man`，允许 band 从 root 权限访问文件系统……（注：此处已移除 OCR 源中的冗余重复）。

# UNIX 系统管理手册

Red Hat 的 NFS 软件有一个异常特性，允许对导出的目录使用不同的选项进行导出。`noaccess` 选项用于“取消导出”那些你不希望共享的子目录。例如，以下配置：

```
- /users *,,xor.com (rw)

- /users/evi (noaccess)
```

该配置允许 com 域的主机访问`users`下的所有目录，但`/users/evi`除外。第二缺少客户端意味着该选项适用于所有主机；这种做法可能更安全一些。

Red Hat 提供了一套丰富的设施来映射远程和本地 UID。虽然我们不建议在异构站点使用它们，但 AI-Linux 船只（ship）可能会发现它们很有用。更多信息请参阅 `exports(5)` 手页。

Red Hat 的 `mount` 可以以后惰性模式运行，而不是持续运行。此配置允许通过 Wietse Venema 的 TCP 程序 `tcpd` 执行辅助性访问控制。更多信息请参阅第 666 页。

Red Hat 的 NFS 实现目前不支持 NFS 3，尽管预计在不久之后将支持。默认使用版本 3 的客户端必须明确指示使用版本 2，否则将产生晦涩错误。

# FreeBSD 下的 Exports

在对 `exports` 文件的第三种相似但不同的处理方式中，FreeBSD 条目由一个由空格分隔的目录列表、一组由空格分隔的选项（全部以连字符开头）以及随后由空格分隔的一系列客户端规范组成。这是一个简短的示例：

```
/chimchim/users -maproot-root band
/chimchim/users moon
/usr/share/man -ro -mapall-daemon xorasaur rastadon moon
```
