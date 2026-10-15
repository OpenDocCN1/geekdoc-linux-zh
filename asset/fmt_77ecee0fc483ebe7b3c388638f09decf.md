
主机没有更改，但增加了额外的导出选项。所有文件系统都使用 `mp` 选项以确保只有文件系统可导出。`/usr/local`、`/usr/devtools`、`/home` 和 `/projects` 只能从使用安全端口（`secure` 选项）的客户端访问，但服务器接受任何端口的请求，因为指定了 `insecure` 选项。对于 `/projects`，匿名用户被映射到 UID 和 GID 600，如 `anonuid=600` 和 `anongid=600` 所示，NIS 开发者的 UID 和 GID 将被映射，因为他们是允许挂载 `/projects` 的唯一 NFS 客户端。

`/home` 和 `/var` 使用 `no_subtree_check` 选项导出，因为它们会看到大量的文件重命名、移动和删除。`sync` 和 `no_wdelay` 选项启用了对 `/projects` 文件系统的写入缓存和删除。`sync` 和 `no_wdelay` 的原理是，在服务器崩溃时数据丢失的影响将是巨大的。以这种方式强制磁盘也会带来性能损失，因为 NFS 服务器正常的磁盘缓存和缓冲启发式算法无法应用。

如果你打算使用 NFSv4 特有的功能，你需要熟悉 RPCSEC_GFS 配置文件、`/etc/gssapi_mech.conf` 和 `/etc/idmapd.conf`。`idmapd.conf` 是 NFSv4 的 `idmapd` 守护进程的配置文件。`idmapd` 的原理是映射 ID。

## 第 12 章

TCP Wrappers 包将在第 19 章中进行详细介绍。我们并不在此预先讨论这一话题，而是建议如何修改这些文件，并简要解释其原理，同时建议你参考第 19 章详细了解这些修改。

首先，在 `/etc/hosts.deny` 中添加以下条目：

```
portmap:ALL
lockd:ALL
mount:ALL
quotad:ALL
statd:ALL
```

这些条目拒绝所有未在 `/etc/hosts.allow` 中被显式允许访问的主机对 NFS 服务的访问。因此，下一步是在 `/etc/hosts.allow` 中添加条目，以允许特定主机访问 NFS 服务。正如你将在第 19 章中学到的，`/etc/hosts.allow` 中的条目格式如下：

```
daemon:host_list [host_list]
```

> 提示：NFS HOWTO (http://nfs.sourceforge.net/nfs-howto/server.html#CONFIG) 不建议在 `/etc/hosts.deny` 中使用 `ALL:ALL` 语法，其理由是：“虽然[拒绝所有服务的访问]是更安全的行为，但当你安装新服务时，可能会遇到麻烦，因为你忘记在那里设置了限制，而你无论如何也想不出为什么它们无法工作。”

我们对此持保留意见。在 `/etc/hosts.deny` 中通过 `ALL:ALL` 结构实现的更强安全性，远大于在配置新服务时可能带来的任何不便。

`daemon` 是如 `portmap` 或 `lockd` 这样的守护进程，`host_list` 是一个或多个主机的列表，可用主机、IP 地址、使用通配符的 IP 地址模式或地址/子网掩码对指定。例如，以下条目允许 `example.com` 域中的所有主机访问 `portmap` 服务：

```
portmap:.example.com
```

下一个条目允许位于子网络 `192.168.0.0` 和 `192.168.1.0` 的所有主机访问：

```
portmap:192.168.0.0, 192.168.1.0.
```

你需要为 `/etc/hosts.deny` 中的五个守护进程中的每一个为每个允许 NFS 访问的主机或主机组添加条目。例如，为了允许 `example.com` 域中的所有主机访问，请在 `/etc/hosts.allow` 中添加以下条目。

```
portmap .:example.com
lockd .:example.com
mountd .:example.com
rquotad .:example.com
statd .:example.com
```

因此，`.domain.com` 形式的匹配所有主机，包括子域（如 `.subdomain.domain.com`）中的主机。

## NFS 服务器守护进程

提供 NFS 需要六个守护进程的服务：`/sbin/portmap`、`/usr/sbin/rpc.mountd`、`/usr/sbin/rpc.nfsd`、`/sbin/rpc.statd`、`/sbin/rpc.lockd`，以及在需要时的 `/usr/sbin/rpc.rquotad`。它们通常分别被称为 `portmap`、`mountd`、`nfsd`、`statd`、`lockd` 和 `rquotad`。如果你打算利用 NFSv4 的增强功能，还需要了解 `.rpc.gssd`、`rpc.idmapd` 和 `rpc.nsecd`。为了方便起见，我们将使用缩写 `gssd`、`idmapd` 和 `nsecd` 来引用这些守护进程。表 12-2 简述了每个守护进程的作用。

| 守护进程 | 功能 |
|---|---|
| gssd | 在 RPC 客户端上创建安全上下文，使用 GSS 通过 SecureRPC (RPCSEC) 交换信息 |
| idmapd | 将本地用户组名映射到 NFSv4 ID（反之亦然） |
| lockd | 启动内核 NFS 锁管理器 |
| mountd | 处理 NFS 客户端请求 |
| nfsd | 提供文件锁定和配额管理外的所有 NFS 服务 |
| portmap | 允许 NFS 客户端发现给定 NFS 服务器上可用的 NFS 服务 |
| rquotad | 使用文件系统配额向 NFS 客户端提供文件系统配额信息 |
| statd | 在 NFS 服务器系统崩溃时实现 NFS 锁恢复 |
| svcssd | 在 RPC 服务器上创建安全上下文，使用 GSS 通过 SecureRPC (RPCSEC) 交换信息 |

NFS 服务器守护进程应按以下顺序启动以正常工作。

1. `portmap`
2. `nfsd`
3. `mountd`
4. `statd`
5. `rquotad`（如有必要）
6. `idmapd`
7. `svcgssd`

如果你使用服务配置工具（`/usr/bin/system-config-services`）启用了 NFS 服务，则启动顺序会在启动时自动为你处理。

注意，`lockd` 和 `nfsd` 根据需要启动的，因此你很少（如果有的话）手动调用它们。幸运的是，Red Hat 的 NFS 初始化脚本 `/etc/rc.init.d/nfs` 会替你启动 NFS 守护进程。如果需要，你可以直接执行实用脚本来手动启动 NFS：

```
# nfs start
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS daemon: [ OK ]
Starting NFS mountd: [ OK ]
```

你也可以使用：

```
# /etc/rc.init.d/nfs start
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS daemon: [ OK ]
Starting NFS mountd: [ OK ]
```

默认情况下，启动脚本会启动八个 `nfsd` 副本以启用服务器。要更改此值，你需要在 `/etc/hosts.deny` 中为每个允许 NFS 访问的主机或主机组为五个守护进程中的每一个添加条目。例如，为了允许 `example.com` 域中的所有主机访问，请在 `/etc/hosts.allow` 中添加以下条目。

```
portmap .:example.com
lockd .:example.com
mountd .:example.com
rquotad .:example.com
statd .:example.com
```

因此，`.domain.com` 形式的名称匹配所有主机，包括子域（如 `.subdomain.domain.com`）中的主机。

```bash
$ /usr/bin/rpcinfo -p
| program | vers | proto | port | alias |
| :--- | :--- | :--- | :--- | :--- |
| 100000 | 2 | tcp | 111 | portmapper |
| 100000 | 2 | udp | 111 | portmapper |
| 100001 | 2 | udp | 961 | rquotad |
| 100001 | 2 | udp | 961 | rquotad |
| 100001 | 1 | tcp | 964 | rquotad |
| 100001 | 2 | tcp | 964 | rquotad |
| 100003 | 2 | udp | 2049 | nfs |
| 100003 | 3 | udp | 2049 | nfs |
| 100003 | 2 | tcp | 2049 | nfs |
| 100003 | 3 | tcp | 2049 | nfs |
| 100003 | 4 | tcp | 2049 | nfs |
| 100021 | 1 | udp | 32770 | nlockmgr |
| 100021 | 3 | udp | 32770 | nlockmgr |
| 100021 | 4 | udp | 32770 | nlockmgr |
| 100021 | 1 | tcp | 35605 | nlockmgr |
| 100021 | 3 | tcp | 35605 | nlockmgr |
| 100021 | 4 | tcp | 35605 | nlockmgr |
| 100005 | 1 | tcp | 32772 | mountd |
| 100005 | 1 | tcp | 32825 | mountd |
| 100005 | 2 | udp | 32772 | mountd |
| 100005 | 3 | udp | 32772 | mountd |
| 100005 | 3 | tcp | 32825 | mountd |
```

`rpcinfo` 的输出显示了 RPC 程序的 ID、版本号、其正在使用的网络协议、正在使用的端口号以及程序号的别名。程序号和名称（第一列和第五列）取自 `/etc/rpc` 文件，该文件将程序映射到程序名称，并列出了程序名称列表。至少为了使一个 NFS 服务器正常运行，`rpcinfo` 应该列出 `portmapper`、`nfs` 和 `mountd` 的条目。

`exportfs` 命令允许你操作可用导出列表，在某些情况下无需编辑 `/etc/exports`。它还会在 `/var/lib/nfs/stab` 中维护当前已导出的文件系统列表，并维护内核中导出文件系统的内部表。事实上，本小节之前讨论的 NFS 初始化脚本大量使用了 `exportfs`。例如，`exportfs -a` 命令初始化 `/var/lib/nfs/stab`，并与 `/etc/exports` 的内容同步。要在不编辑 `/etc/exports` 的情况下向 `stab` 和内核 NFS 导出内部表添加新导出，请以下语法：

```bash
exportfs -o opts host:dir
```

`opts`、`host`、`dir` 使用与章节之前描述的 `/etc/exports` 相同的语法。考虑以下命令：

```bash
# exports -o async,rw 192.168.0.3:/var/spool/mail
```

该命令向 IP 地址为 `192.168.0.3` 的主机以 `async` 和 `rw` 选项导出 `/var/spool/mail`，与 `/etc/exports` 中的以下条目完全等：

```bash
/var/spool/mail 192.168.0.3 (async,rw)
```

裸使用的 `exports` 列出所有已导出的文件；添加 `-v` 选项列出当前导出的文件及其挂载选项。

```bash
# exports -v
/usr/local      192.168.0.4 (ro,wdelay,root_squash)
/home           192.168.0.4 (rw,wdelay,root_squash)
```

要删除已导出的文件系统，请使用 `exports` 的 `-u` 选项。例如，以下命令删除了上一个示例中的 `home` 文件。

```bash
# exports -v -u 192.168.0.4:/home
exporting 192.168.0.4:/home
```

`showmount` 命令查询挂载守护进程 `mountd` 关于 NFS 服务器的状态。其语法为：

```bash
showmount [-v]host
```

不带任何选项调用时，`showmount` 会显示从当前主机挂载文件系统的所有客户端列表。指定 `host` 来查询挂载守护进程，其中 `host` 可以是解析的 DNS 主机名，或者如下例所示，是一个 IP 地址：

```bash
# showmount 192.168.0.1
```

`192.168.0.1` 上的主机：

表 12-3 描述了 `showmount` 选项的影响。

| OPTION | DESCRIPTION |
| :--- | :--- |
| -a | 显示所有挂载点 |
| -d | 显示当前已导出的目录 |
| -e | 显示服务器的导出列表 |
| -h | 显示主机名 |
| --no-headers | 禁止显示标题 |
| -v | 显示详细信息 |

以下示例显示了 `showmount` 在 `bubble.com` 上的输出，该主机 IP 地址为 `192.168.0.2`，使用了 `/etc/exports` 中的以下条目：

```bash
# showmount -a
All mount points on bubble.com:
192.168.0.0/24:/media

# showmount -d
Directories on bubble.com:
/media

# showmount -e
Export list for bubble.com:
192.168.0.0/24
```

`showmount` 命令对潜在的客户端非常有用，因为它们可以识别 NFS 服务器导出的目录。然而，如果没有在 `/etc/hosts.deny` 禁止访问，任何主机都可以获取这些信息。

## 使用安全 NFS

尽管安装了 NFS4，但默认安装并没有启用 NFS4 的安全性增强。你需要手动设置。按照以下步骤操作：

1. 通过向 `/etc/sysconfig/nfs` 添加以下行启用安全 NFS：

```bash
SECURE_NFS=no
```

注意：在 Fedora Core 4 和 RHEL 4 上不存在 `/etc/sysconfig/conf`。使用 Kerberos 5 或其他强加密机制时，你应该将此变量设置为 `yes`。

2. 编辑 `/etc/idmapd.conf` 将 `Domain` 选项设置为你的域名，并将 `Nobody-User` 和 `Nobody-Group` 选项设置为 `nobody`：

```
Domain = example.com
[Mapping]
Nobody-User = nobody
Nobody-Group = nobody
```

你可能不需要进行此更改，因为 `idmapd.conf` 通常默认使用 `nobody` 用户和组。

3. 使用 `service` 工具重启 `portmapper` 和 NFS：

```bash
# service portmap restart
# service nfs restart
```

你不需要启动 GSS 客户端和服务器守护进程 `rpcgssd` 和 `rpcsvcssd`，除非你想使用 Kerberos 5 或另一种强加密机制（如果是的话，本章不涉及额外的设置）。

## NFS 服务器示例

本节演示了一个简单但代表性的 NFS 服务器配置。它导出两个文件系统，`/home` 和 `/media`。以下是 `/etc/exports` 中对应的条目：

```bash
/home 192.168.0.0/24 (rw,async,no_subtree_check)
/media 192.168.0.0/24 (rw)
```

# 网络文件系统 293

![](img/b5ebc2d43ffbc3488ca0205212f962cb_329_0.png)

图 12-2 NFS 服务器配置对话框。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_329_1.png)

图 12-3 添加 NFS 共享对话框。

要修改新 NFS 导出的挂载选项，请点击“常规选项”（General Options）选项卡。在此选项卡上，勾选复框框启用相应的挂载选项。可能的挂载选项包括：

- 允许来自 1024 及更高端口的连接 — 此选项对应表 12-1 列出的 `insecure` 选项。
- 允许安全文件锁定 — 此选项对应表 12-1 列出的 `insecure_locks` 选项。
- 禁用子树检查 — 此选项对应表 12-1 列出的 `no_subtree_check` 选项。
- 请求时同步写操作 — 此选项（默认启用）对应表 12-1 列出的 `sync` 选项。
- 强制立即同步写操作 — 此选项仅在启用“请求时同步写操作”时才可用，并对应表 12-1 列出的 `no_wdelay` 选项。
