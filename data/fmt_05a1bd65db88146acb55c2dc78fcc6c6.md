
### DHCP 选项

| option broadcast-address ip-address; | 客户端的广播地址。 |
| option nis-domain string; | 客户端的网络信息服务（NIS）域。 |
| option nis-servers-ip-address [ ip-address... ]; | 客户端可以使用的 NIS 服务器。 |
| option smtp-server-ip-address [ ip-address... ]; | 客户端使用的 SMTP 服务器列表。 |
| option pop-server-ip-address [ ip-address... ]; | 客户端使用的 POP 服务器列表。 |
| option nmtp-server-ip-address [ ip-address... ]; | 客户端使用的 NMTP 服务器列表。 |
| option www-server-ip-address [ ip-address... ]; | 客户端 Web 服务器列表。 |

你使用 `subnet` 告知 DHCP 服务器给定子集包含的可能 IP 地址。`subnet` 语句包含了子网的子网掩码。

```
subnet 192.168.1.0 netmask 255.255.255.0 {
```

通过 `range`，你指定可以动态分配给客户端的地址范围。你在范围内输入第一个和最后一个地址。

```
range 192.168.1.5 192.168.1.128 {
```

通过 `参数`，你可以指定服务器如何处理客户端。`default-lease-time` 参数设置分配给租期的秒数。`filename` 参数指定客户端使用的启动文件。`server-name` 参数告知客户端服务器。`fixed-address` 参数可用于分配静态地址。这是由服务器提供的查找并使用客户端的 IP 地址。

- `rpc.stat` 在远程主机重启时提供锁定服务。
- `rpc.lockd` 为已宕机的系统处理锁恢复。

注意：建议仅在本地安全网络上使用 NFS。如果通过 网使用，NFS 将使你的系统面临不安全访问的风险。

在 Red Hat 上，你使用 `/etc/rc.cd/init.d/nfs` 脚本来启动和关闭 NFS 守护进程。你可以直接访问此脚本，或如所示使用 `service` 命令：

```
service nfs start
```

要让 NFS 自动启动，你可以使用 `chconfig`（服务配置工具）或 `ksysv` 指定其运行的级别。以下示例将使 NFS 在运行级别 3 和 5 下启动：

```
chconfig -level 35 nfs on
```

`nfs` 脚本将启动 `portmapper`、`nfsd`、`mountd` 和 `quotad` 守护进程。要启用 NFS 锁定，你需要 `nfslock` 脚本。它将启动并锁定守护进程。NFS 锁定可以更好地恢复因远程主机崩溃而发生的中断操作。

```
service nfslock start
```

要查看 NFS 是否实际上正在运行，你可以如所示使用带有 `-p` 的 `rpcinfo` 命令。你应该看到 `mount` 和 `nfs` 的条目。如果没有，说明 NFS 未在运行。

| rpcinfo | vers | proto | port | program |
|---|---|---|---|---|
| 100000 | tcp | 111 | portmapper |
| 100000 | udp | 111 | portmapper |
| 100024 | udp | 32768 | status |
| 100024 | tcp | 32768 | status |
| 100011 | udp | 647 | rquotad |
| 100011 | tcp | 647 | rquotad |
| 100005 | udp | 32769 | mountd |
| 100005 | tcp | 32769 | mountd |
| 100005 | tcp | 32769 | mountd |
| 100002 | tcp | 32769 | nfs |
| 100003 | udp | 2049 | nfs |
| 100003 | tcp | 2049 | nfs |
| 100021 | udp | 32770 | nlockmgr |
| 100021 | tcp | 32770 | nlockmgr |

## NFS 配置：`/etc/exports`

`/etc/exports` 中的条目指定了要导出的文件系统以及网络上可以访问它的系统的主机。对于文件系统，指的是其挂载点（即在主机上挂载的目录）。它由一个可以访问该文件系统的主机列表，以及用于控制该访问的选项组成。每个主机后面可以跟一个位于括号内的逗号分隔的导出选项列表。例如，你可能想给一个主机只读访问权限，给另一个主机读写访问权限。如果选项前面有一个符号，则它们将应用于任何主机。表 37-1 提供了选项列表。`/etc/exports` 文件中条目的格式如下所示：

### 表 37-1：`/etc/exports` 选项

| 通用选项 | 说明 |
|---|---|
| secure | 要求请求源自小于 1024 安全端口。这是默认设置。 |
| insecure | 关闭 `secure` 选项。 |
| ro | 仅允许只读访问。这是默认。 |
| rw | 允许读写访问。 |
| sync | 在请求时执行所有写入操作。这是默认设置。 |
| async | 当服务器准备好时执行所有写入。 |
| no_wdelay | 立即执行，不检查它们是否有关联。 |
| wdelay | 检查写入是否有关联，如果是，则等待执行。这会降低性能。这是默认设置。 |
| hide | 自动隐藏作为导出目录子目录的目录。子目录必须挂载才能访问。父目录不允许访问。这是默认设置。 |
| no_hide | 不隐藏作为导出目录子目录的目录（`hide` 的反）。适用于单主机且可能失效。 |
| subtree_check | 检查文件系统中的父目录以验证导出的子目录。这是默认设置。 |
| no_subtree_check | 不检查文件系统中的父目录以验证导出的子目录。 |
| insecure_locks | 不需要对锁定请求进行认证。用于旧版本的 NFS。 |
| 用户 ID 映射 |  |
| all_squash | 将 uid 和 gid 映射为匿名用户。适用于 导出的 FTP 目录、新闻池目录等。 |
| no_all_squash | `all_squash` 的相反选项，默认设置。将请求映射到原始用户。 |
| no_root_squash | 防止 root 用户被映射为匿名用户。 |
| root_squash | 将 root 用户映射为匿名用户。 |

你有多种选项可用：

```
pathname (options)
```

对于导出的目录具有灵活性：

```
pathname (options)
subdirectory (options)
```

你可以使用：

```
pathname (options)
hostname (options)
```

你可以使用：

```
pathname (options)
network (options)
```

你可以使用：

```
pathname (options)
CIDR (options)
```

你可以使用：

```
pathname (options)
@group (options)
```

`/etc/exports` 文件中条目的示例如下所示。所有主机对挂载在 `/pub` 目录的文件系统具有只读访问权限，`/pub` 是公共的常用名称。

访问。然而，用户被视为匿名用户（`all_squash`）。对于挂载在 `/home/foodstuff` 目录上的文件系统，`lizard.mytrek.com` 具有读写权限。下一条目将允许 `rabbit.mytrek.com` 访问 NFS 服务器的 CD-ROM。最后一条目允许对 `/home/richhlp` 进行安全访问。

`/etc/exports`

| /pub | (ro,secure,all_squash) |
| /home/foodstuff | lizard.mytrek.com (rw) |
| /mnt/cdrom | rabbit.mytrek.com(ro) |
| /home/richhlp | * (secure) |

注意编辑 `/etc/exports` 文件时，您可以使用 Linuxconf 中“配置(Config)”下的“服务器任务(Server Tasks)”列表中的“导出文件系统(Exported File Systems)”。点击“Add”按钮添加新条目。
