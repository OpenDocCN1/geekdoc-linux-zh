
> `nfs-kernel-server` `portmap`

安装过程还将自动为你启动 NFS 服务器及其所有相关服务。你可以运行以下命令进行检查：

```bash
yyang@ubuntu-serverA:-$ rpcinfo -p
```

要停止 Ubuntu 中的 NFS 服务器，你可以输入：

```bash
yyang@ubuntu-serverA:-$ sudo /etc/init.d/nfs-kernel-server stop
```

## NFS 的组件

NFS 协议第 2 和第 3 版本严重依赖 RPC 处理客户端与服务器之间的通信。Linux 中的 RPC 服务由 `portmap` 服务管理。如前所述，这种辅助服务在 NFSv4 中不再需要。

以下列表列了 Linux 下促进 NFS 服务的各种 RPC 进程。RPC 进程主要适用于 NFS 第 2 和第 3 版本，但在适用于 NFSv4 时也会提及。

- `rpc.statd`: 此进程负责在 NFS 服务器在未正常关闭的情况下重启时向 NFS 客户端发送通知。为 `rpc.lockd` NSM RPC 协议提供服务器的状态信息。这是一个可选服务，在 Fedora 系统上由 `nfslock` 服务自动启动。它在 NFSv4 中不被使用。
- `rpc.quotad`: 正如其名，`rpc.quotad` 提供了 NFS 与配额管理器之间的接口。NFS 用户/客户端将受到相同的配额限制，这些限制与它们在本地文件系统而非 NFS 上工作时所受的限制相同。
- `rpc.mount`: 当发出挂载分区的请求时，`rpc.mount` 守护程序验证客户端是否有权发出该请求。此权限存储在 `/etc/exports` 文件中（接下来的章节“/etc/exports 配置”将会说明）。
- `rpc.nfsd`: 这是 NFS 的核心组件。
- `rpc.lockd`: 此服务处理文件锁定。
- `rpc.statd`: 此服务提供状态信息和恢复。
- `rpc.idmapd`: 此进程将 ID 转换为名称。
- `rpc.gss`: 提供与安全相关的服务。

## NFS 的内核支持

NFS 在各种发行版中以两种形式实现。大多数发行版都默认启用了支持。从 Linux 2.2 开始就有内核支持。大多数现代 Linux 发行版都默认启用了该支持。

## 配置 NFS 服务器

设置 NFS 服务器是一个两步骤的过程。第一步是创建 `/etc/exports` 文件。该文件定义了服务器磁盘的哪些部分与网络其他部分共享以及共享规则。第二步是启动读取 `/etc/exports` 文件的 NFS 服务器进程。

### /etc/exports 配置文件

这是 NFS 服务器的主要配置文件。该文件列出了共享的分区、可以与哪些主机共享以及以什么权限共享。文件指定了 NFS 挂载协议的远程挂载点。

该文件的格式简单。文件中的每行指定了一个本地服务器文件系统中一个或多个的挂载点和导出标志。

`/etc/exports` 文件中每个条目的格式如下：

```
/directory/to/export client|ip_network(permissions) client|ip_network(permissions)
```

- `directory/to/export`: 这是你想与其他用户共享的目录，例如 `/home`。
- `client`: 指 NFS 客户端的主机。
- `ip_network`: 允许通过 IP 地址或网络地址结合掩码组合来匹配主机。
- `permissions`: 对应每个客户端的权限。

## 第 22 章：网络文件系统 (NFS)

以下是一个完整的 NFS `/etc/exports` 文件示例。请注意，列表中添加了 (1–4) 行以提高可读性。

+   1) # serverA 的 /etc/exports 文件
2) #
3) /hostA(rw) hostB(rw) clientA(ro,no_root_squash)
4) /usr/local 172.16.0.0/16(ro)

第 1 行和第 2 行是注释，读取文件时会被忽略。第 3 行将 `/home` 系统导出到名为 hostA 和 hostB 的机器，赋予它们读/写 (rw) 权限，并向名为 clientA 的机器赋予其只读 (ro) 访问权限，允许远程 root 用户对导出的文件系统 (/home) 拥有 root 权限。

第 4 行将 `/usr/local/` 目录导出到 172.16.0.0/16 网络上的所有主机。网络中的主机被允许只读访问。

| 权限选项 | 含义 |
| --- | --- |
| secure | 客户端请求挂载的端口号必须小于 1024。此权限默认开启。若要关闭它，请指定 insecure。 |
| ro | 允许对分区进行只读访问。当没有显式指定任何内容时，这是默认权限。 |
| rw | 允许标准的读/写访问。 |
| noaccess | 客户端将被拒绝访问 /dir/to/mount 下的所有目录。这允许你将目录 /dir 导出给客户端，然后指定 /dir/to 为不可访问，而不会剥夺对 /dir/from 等内容的访问。 |
| root_squash | 防止远程 root 用户在 NFS 挂载卷上拥有超级用户（root）权限。“squash”字面意思是压制远程 root 用户的权限。 |
| no_root_squash | 允许 NFS 客户端上的 root 用户以超级用户通常拥有的权利和权限访问 NFS 挂载目录。 |
| all_squash | 将所有用户 ID (UIDs) 和组 ID (GIDs) 映射为匿名用户。相反的选项是 no_all_squash，它是默认设置。 |

表 22-1.NFS 权限

Linux 管理：入门指南

### 告 NFS 服务进程关于 /etc/exports

一旦你写好了 `/etc/exports` 文件，请使用 `exportfs` 命令通知 NFS 进程重新读取配置信息。`exportfs` 的参数如下：

| exportfs 命令选项 |or |
| - | - |
| -a | 导出 /etc/exports 文件中的所有项目。当与 u 选项一起使用时，也可用于取消导出的文件系统，例如 `exportfs -ua`。 |
| -r | 重新导出 /etc/exports 文件中的所有项目。这将同步 `/var/lib/nfs/stab` 的内容。例如，它会删除 /var/lib/nfs/stab 中不再存在于 /etc/exports 中的项目，并移除内核导出表中的过时项目。 |
| -u clientA:/dir/to/mount | 取消主机 clientA 目录 /dir/to/mount。 |
| -o options | 此处指定的选项与表 22-1 中描述的客户端权限相同。这些选项仅适用于 exportfs 命令行指定的le系统，而不适用于 /etc/exports 中的系统。 |

以下是 `exportfs` 命令行的示例。

```
[root@serverA ~]# exportfs -a
```

要以读/写和 no_root_squash 权限将 `/usr/local` 目录导出到主机 clientA，

```
[root@serverA ~]# exportfs -o rw,no_root_squash clientA:/usr
```

在大多数情况下，你只需要使用 `exportfs -r`。注意，Fedora 和 RHEL 系统有一个强大的图形用户界面 (GUI) 工具（见图 22-1），用于创建、修改和删除 NFS 共享。该工具名为 `system-config-nfs`。可以通过执行以下命令从命令行启动它：

```
[root@serverA ~]# system-config-nfs
```

![](img/92d05360cfbe3adba30a0993f6974865_537_0.png)

**图 22-1.** NFS 服务器配置实用

### showmount 命令

在配置 NFS 时，使用 `showmount` 命令检查一切是否运行正常是非常帮助的。该命令用于显示 NFS 服务器的挂载信息。

通过使用 `showmount` 命令，你可以快速判断是否正确配置了 `nfs`。
在你配置好 `/etc/exports` 文件并使用 `exportfs -e` 导出所有文件系统后——这可以查看本地 NFS 服务器上导出的文件系统列表。`-e` 选项告诉 `showmount` 显示 NFS 服务器的导出列表。例如：

```
[root@serverA ~]# showmount -e localhost
Export list for localhost:
/home *
```

如果你只是不带选项运行 `showmount` 命令，它将列出连接到服务器的客户端。例如

```
[root@serverA ~]# showmount localhost
Client                               from directory
```
