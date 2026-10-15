

of dfstab 并运行它们。由于 NFS 是唯一遵循此约定的原生文件共享系统，shareall 等价于 sh /etc/dfs/dfstab。）

## 表 18.2 在何处设置导出的目录

| 系统 | 导出信息在 | 修改后需要执行的操作 |
|---|---|---|
| Linux | /etc/exports | 运行 /usr/sbin/exportfs -a |
| Solaris | /etc/dfs/dfstab | 运行 shareall |
| HP-UX | /etc/dfs/dfstab | 运行 shareall |
| AIX | /etc/exports | 运行 /usr/sbin/exportfs -a |

NFS 处理文件系统的逻辑层。任何目录都可以被导出；它不必是挂载点或物理文件系统的根目录。然而，出于安全考虑，NFS 确实会注意文件系统之间的边界，并要求每个设备单独导出。例如，在一台将 /users 设置为单独分区的机器上，你可以导出根目录而不导出 /users。

客户端通常被允许按需挂载导出目录的子目录，尽管协议并不要求此功能。例如，如果服务器导出 /chimchim/users，客户端可以只挂载 /chimchim/users/joe 而忽略其余的用户目录。

大多数版本的 UNIX 不允许你以不同的选项导出导出目录的子目录，但在 Linux 下这种做法是可以的。

## share 命令和 dfstab 文件（Solaris、HP-UX）

/etc/dfs/dfstab 对每个导出的文件系统执行一次 share 命令。

例如，在一台将 /home 与主机 monk 和 leopard 共享（monk 允许 root 访问）并将 /usr/share/man 与主机 ross 和 harp 共享的服务器上，/etc/dfs/dfstab 文件将包含以下命令：

```
share -F nfs -o rw=monk.at rust.com,leopard.at rust.com,root=monk.at rust.com /home
share -F nfs -o rw=ross.at rust.com,harp.at rust.com /usr/share/man
```

编辑 /etc/dfs/dfstab 后，记得运行 shareall 使更改生效。由于 shareall 只是运行 dfstab 文件中的命令，它不会取消你删除的文件系统的共享。使用命令 unshare /path/to/fs 来显式移除共享。表 18.3 列出了 share 的最常用选项。

![](img/14d78e3cecac4581d37024baf1e94cca_748_0.png)

![](img/14d78e3cecac4581d37024baf1e94cca_748_1.png)

## 表 18.3 share 命令的选项（Solaris、HP-UX）

| 选项 | 描述 |
|---|---|
| ro | 对全世界只读导出（不推荐） |
| ro=list | 只读导出，仅允许列出的主机访问 |
| rw | 对全世界读写导出（不推荐） |
| rw=list | 读写导出，仅允许列出的主机访问 |
| root=list | 列出允许作为 root 访问此文件系统的主机；否则，来自客户端的 root 访问等同于 "nobody" 的访问（通常为 UID -2） |
| anon=uid | 指定 root 被映射到的 UID；默认值为 "nobody" |
| nosub | 禁止客户端挂载导出目录的子目录 |
| nosuid | 防止通过 NFS 创建 setuid 和 setgid 文件 |

在 share 选项中需要列表的地方，它应由表 18.4 中所示项目的冒号分隔组组成，所有这些都是指定主机或主机组的方式。

## 表 18.4 share 命令的客户端规范

| 类型 | 语法 | 含义 |
|---|---|---|
| 主机名 | hostname | 单个主机（必须是完全限定） |
| 网组 | groupname | NIS 网组（不常用） |
| DNS 域 | .domain.com | 域内的任何主机 |
| IP 网络 | @netname | /etc/networks 中定义的网络名称* |
| a. 也接受 CIDR 风格的规范；例如，@128.138.92.128/25。 | | |

表 18.4 中关于主机名的注释值得重申：单个主机名必须是完全限定的，否则将被忽略。

你可以在项目前加上连字符以显式禁止它。列表在每次查找时从左到右检查，直到找到匹配项，因此否定应置于它们所修改的更通用项目之前。例如，行

```
share -F nfs -o rw=@192.168.10.0/24:booklab.atrust.com /users
```

将 /users 对 booklab.atrust.com DNS 域中的所有主机只读导出，但排除 192.168.10 网络上的主机。在该命令中，-F 标志表示 share 应使用 nfs 文件系统类型，而不是 /etc/dfs/fstypes 中的其他类型。

可以对某些客户端只读导出目录，而对其他客户端读写导出。只需同时包含 rw= 和 ro= 选项即可。

share 手册页记录了一些基本 NFS 选项。完整列表请参考 share_nfs 手册页。

