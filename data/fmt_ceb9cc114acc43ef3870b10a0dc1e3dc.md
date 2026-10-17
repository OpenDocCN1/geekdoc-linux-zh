
通过使用根所有抑制（root squashing），所有三个导出将 UID 0 映射到 `nobody` 账户的 UID，该账户具有普通用户的权限。如果用户在 NFS 客户端上拥有 root 权限，但在挂载的 NFS 文件系统上没有 root 权限，则会执行根所有抑制。如果禁用根所有抑制，管理员必须确保没有任何 NFS 客户端拥有 root 权限。否则，远程 root 可能会读取或删除其不应具有权限的文件。要确定网络上每台机器的完整性几乎是不可能的；因此不建议禁用根所有抑制。

根所有抑制将 root 账户视为来自占位符账户 `nobody`。由于根所有抑制是默认执行的，且 `nobody` 账户在 Linux 安装时创建，因此所有导出的文件系统将自动执行根所有抑制。

# 练习

为了配置 NFS 服务器允许导出，用户必须编辑 `/etc/exports`。文件中添加三条规则，每行一条。每条规则将管理一个导出的文件系统。此外，还需要第四条规则来明确说明 `/projects/secret/` 不会被导出。由于根所有抑制是默认执行的，第一条规则将管理文件系统：

```
/notes *.lucasdigital.com(ro)
```

导出选项 `ro` 用于只读模式导出。下一条规则将管理文件系统：

```
/workinprogress designer.lucasdigital.com(rw)
```

在这里，导出选项 `rw` 用于读/写模式导出。第三条规则将管理文件系统：

```
/projects foo fee tele.lucasdigital.com(ro)
```

客户端名称用空格分隔。由于 `/projects/secret` 不应被导出，需要额外的规则：

```
/projects/secret (noaccess)
```

为了拒绝访问特定目录，使用了 `noaccess` 选项。因此，`/etc/exports` 文件将类似于：

```
# /etc/exports NFS 服务器
# lucasdigital.com 域中的所有人允许以只读模式
# 挂载 /notes
/notes *.lucasdigital.com(ro)

# designer 机器可以以完全权限挂载 /workinprogress。
/workinprogress designer.lucasdigital.com(rw)

# 三个客户端 foo、fee 和 tele.lucasdigital.com 可以
# 以只读模式挂载 /projects。然而，
# 他们无法访问 /projects/secret 目录。
/projects foo(ro) fee(ro) tele.lucasdigital.com(ro)
/projects/secret (noaccess)
```

在修改 `/etc/exports` 后，用户必须运行 `/usr/sbin/exportsfs -a`。读取新配置：

```
$ /usr/sbin/exportsfs -a
```

要验证更改，使用不带任何选项的 `exportfs` 命令。应该出现类似下面的输出：

```
$ /usr/sbin/exportfs
/notes *.lucasdigital.com
/workinprogress designer.lucasdigital.com
/projects foo fee tele.lucasdigital.com
```

# 问题

- 1. 为什么没有使用 squash 和 anonuid 选项？

- 2. 编辑 `/etc/exports` 文件后必须发送什么命令？

# 答案

- 1. 没有使用 `root_squash` 选项是因为根所有抑制是默认执行的。没有使用 `anonuid` 选项是因为 UID 为 0 的用户默认映射到 `nobody` 账户。

- 2. 必须带有 `-a` 选项发送 `/usr/sbin/exportsfs` 命令，以便重新读取修改后的 `/etc/exports` 文件。

# 高级问题

- 1. 更改 root 被抑制到的 UID 而不是使用默认值为什么是一个坏主意？

- 2. 如果给 NFS 客户端授予了错误的访问权限，可能会产生哪些安全问题？

## hosts.allow, hosts.deny, 和 hosts.lpd

### 目的

本实验演示了如何编辑 `hosts.allow`、`hosts.deny` 和 `hosts.lpd` 文件来保护系统。通过编辑这些文件，可以过滤系统连接，防止未授权的用户进入本地网络；或者在 `hosts.lpd` 文件的情况下，防止未经授权的打印机使用。

### 理论

`tcp_wrapper` 工具用于通过允许本地或远程网络中的某些主机访问本地主机上运行的服务，来提高系统安全性。同时，它可以拒绝其他主机访问相同的服务。这使得管理员能够确定系统用户的权限。这种能力的核心是 `tcp_wrapper` 守护进程 `tcpcpd`。`tcpcpd` 使用三个文件：`hosts.allow`、`hosts.deny` 和 `hosts.print` 来决定传入的请求（如 Telnet 或 FTP 连接）是否允许。

`hosts.allow` 和 `hosts.deny` 文件遵循简单的格式指南。以井号 (`#`) 开头的是注释；所有其他行都被视为文件的一部分。每行的第一部分是服务名，后跟着一个冒号 (`:`），然后是主机或域名的列表。可以通过可选的第三字段添加额外的安全性，该字段会执行命令。同样，使用冒号将域名或主机名与新字段分开，命令放在括号中。

`tcpd` 会从上到下检查 `hosts.allow` 和 `hosts.deny` 文件，当找到服务/主机的匹配项时检查停止。由于由于原因，规则在文件中的排列顺序非常重要。如果 `ALL:ALL` 是 `hosts.allow` 文件的第一行，那么无论该文件中的其他项或 `hosts.deny` 文件中的其他项如何，所有主机都可以访问所有服务。第一行总是会被检查，其后的所有内容都会与之匹配。

以下示例展示了如何配置 `hosts.allow` 和 `hosts.deny` 文件：

```
/etc/hosts.allow:
# hosts.allow 此文件描述了允许使用本地 INET 服务的主机名称，
# 这些主机由 '/usr/sbin/tcpd' 服务器决定。
telnetd:.starwars.com EXCEPT web.starwars.com
ftpd: 24.41.207.50
ALL: LOCAL

/etc/hosts.deny:
# hosts.deny 此文件描述了不允许使用本地 INET 服务的主机名称，
# 这些主机由 '/usr/sbin/tcpd' 服务器决定。
ftpd: ALL; /bin/mail -s WH root &
ALL: ALL
```

这些文件使用了 `hosts_options` 控制语言扩展，其中包含 `ALL`、`EXCEPT` 和 `LOCAL` 等关键字，使规范变得更简单。域名前的点 (`.`) 被读取为该网络中的所有计算机，如 `hosts.allow` 文件中的 `telnetd` 所示。也可以通过在 `hosts.allow` 或 `hosts.deny` 文件中放置主机的精确地址并指定适当的服务，来允许或拒绝单个主机的访问。此示例中的 `EXCEPT` 通配符告诉系统不要允许 `web.starwars.com` 访问 `telnetd`，即使它在被授予宽泛访问的网络中。在服务名或主机名处使用 `ALL` 通配符将包含所有服务或所有主机（视情况而定）。`LOCAL` 指向本地网络上的所有主机。

这些文件最安全的配置是在 `hosts.allow` 文件中指定授予访问服务的 la主机，并在 `hosts.deny` 文件的末尾拒绝所有主机访问所有服务。这样做效果良好，因为 `tcpd` 会首先读取 `hosts.allow` 文件查找尝试连接的主机。如果主机在该文件中，则授予其访问权限；如果不在，守护进程将处理 `hosts.deny` 文件并检查匹配项。允许所有主机访问所有服务器永远不是明智之。如果这样做，`hosts.deny` 文件将永远不会被读取，从而使系统对任何想要连接的用户开放。

记住，这些文件仅控制通过 TCP、UDP 或任何其他协议的访问。

### /etc/hosts.lpd

虽然 `hosts.lpd` 文件与 `hosts.allow` 和 `hosts.deny` 使用相同的格式，但在表示主机权限时存在某些语法差异。

- `+ A A`：加号 (`+`) 表示网络上的任何主机都可以通过本地主机进行打印。

- `* HostName`：`HostName` 条目是远程主机的名称，表示 `HostName` 通过本地主机进行打印。

- `-Hostname`：`-Hostname` 条目表示该主机不允许通过本地主机进行打印。

- `+NetGroup A`：`+NetGroup` 条目允许 `/etc/netgroup` 文件指定的给定 NIS 网组中的所有主机通过本地主机进行打印。

- `-NetGroup A`：`-NetGroup` 条目拒绝给定网组中的所有主机通过本地主机进行打印的权利。
