
10. 使用什么可以在只有一个 IP 地址的情况下让网络访问 Internet？

#### 执行安全管理任务

##### 1.13 网络服务

- **配置和管理 `inetd` 及相关服务。** 配置通过 `inetd` 可用的服务，使用 `tcpwrappers` 按主机允许或拒绝服务，手动启动、停止和重启网络服务，配置包括 `telnet` 和 `ftp` 在内的基本网络服务。包括管理 `inetd.conf`、`hosts.allow` 和 `hosts.deny`。

##### 1.14 安全性

- **执行安全管理任务。** 配置和使用 `TCP` wrappers 来锁定系统，列出所有设置了 `SUID` 位的文件，确定任何软件包（`.rpm` 或 `.deb`）是否已损坏，在安装前验证新软件包，在目录上使用 `setgid` 以保持组所有权一致，更改用户密码，设置用户密码的过期日期，获取、安装和配置 `ssh`。

管理员可以执行多项操作来保护新安装的系统。这些操作包括使用 `TCP` wrappers 锁定某些服务以及管理用户和组。

> 分配和使用密码是第 10 章更详细涵盖的主题。

###### 配置 TCP wrappers

`tcpd` 守护程序，也称为 `TCP` wrappers 软件包，可用于限制可以针对某些网络服务建立的连接。这样，您可以将对这些服务的访问限制为仅限授权用户。它易于配置并集成到正在运行的系统中。无需对网络守护程序进行任何更改，只需对 `inetd.conf` 文件进行少量更改。例如，如果您的 `inetd.conf` 文件目前包含以下 FTP 服务器条目：

```
ftp stream tcp nowait root /usr/sbin/in.ftpd in.ftpd -l -a
```

若要使用 TCP wrappers，请将其更改为以下内容：

```
ftp     stream    tcp     nowait    root    /usr/sbin/tcpd   in.ftpd
    -l -a
```

通常的守护进程服务器路径被替换为 `tcpd` 的路径，而参数则是实际要运行的服务器。TCP wrappers 使用两个文件来配置允许的连接：

- `/etc/hosts.allow`
- `/etc/hosts.deny`

这两个配置文件使用相同的格式。如果任一文件不存在，则被视为空。如果 `hosts.allow` 中有条目，但 `hosts.deny` 中没有，则任何未明确授予权限的连接都将被拒绝。相反，如果 `hosts.deny` 中有条目，但 `hosts.allow` 中没有，则连接被允许，除非被明确拒绝。如果两个文件中都存在条目，则先检查 `hosts.allow`，然后检查 `hosts.deny`。因此，即使某个连接在 `hosts.deny` 中被拒绝，也可以通过 `hosts.allow` 来覆盖。这些文件的语法如下：

```
service: host_list [: shell command]
```

服务名称与 `/etc/services` 和 `/etc/inetd.conf` 中列出的名称完全一致。主机列表是主机、域名、通配符或 `CIDR` 地址的列表。例如，`/etc/hosts.allow` 中的以下条目允许 `nashes.net` 域名下的任何主机连接到 FTP 服务器：

```
in.ftpd: .the-nashes.net
```

表 17-1 展示了可能的主机和服务匹配方法。

####### 表 17-1 匹配方法

| 方法 | 功能 |
| :--- | :--- |
| `.domain.org` | 以点开头的域名表示“该域名内的任何主机”。 |
| `192.168.` | 以点结尾的数值地址表示拥有该 IP 前缀的任何主机。这匹配 `192.168*`。 |
| `Address/Mask` | 网络地址和子网掩码的组合，例如 `192.168.0.0/16`。 |
| `ALL` | 匹配任何客户端或服务名称。 |
| `LOCAL` | 匹配任何不包含点号的客户端主机名。 |
| `EXCEPT` | 允许对 `ALL` 进行例外处理。 |

> **注意** 请小心使用 `LOCAL` 命令。如果您的 `/etc/hosts` 文件包含一个仅带有主机名而没有域名的条目，无论其是否实际上是本地主机，都可能允许其访问。

可选的 shell 命令可用于在客户端连接且匹配指定规则时执行功能。shell 命令中可以使用多种模式，这些模式在运行时会被展开。表 17-2 列出了这些模式。另一个有用的选项是 `twist` 命令。它会将 shell 命令的输出显示给连接的客户端，同时还会显示来自展开模式的信息。例如：

```
in.telnetd : .evil.org : twist /bin/echo "Sorry &c, but we don't want your kind around here."
```

这将导致该消息回显给来自 `evil.org` 域并连接到 Telnet 服务器的任何用户。

**表 17-2 tcpd 模式**

| 模式 | 功能 |
| :--- | :--- |
| `%a` | 连接客户端的主机地址。 |
| `%A` | 服务器的主机地址。 |
| `%c` | 客户端信息，如 `user@host`、`user@address`、`hostname` 或 `address`，具体取决于可用信息。 |
| `%d` | 守护进程名称。 |
| `%h` | 连接客户端的主机名，如果无法获取主机名，则为地址。 |
| `%H` | 服务器的主机名，如果无法获取主机名，则为地址。 |
| `%n` | 客户端主机名。 |
| `%N` | 服务器主机名。 |
| `%p` | 守护进程的进程 ID。 |
| `%s` | 服务器信息，如 `daemon@host`、`daemon@address` 或仅守护进程名称，具体取决于可用信息。 |
| `%u` | 客户端用户名，或 `unknown`。 |

TCP wrappers 提供了一些实用工具来检查您的配置。第一个是 `tcpdchk`。它用于检查您的语法，并确保规则按预期工作。表 17-3 列出了 `tcpdchk` 的命令行选项。以下是 `tcpdchk` 的示例输出。

```
Using network configuration file: /etc/inetd.conf
>>> Rule /etc/hosts.allow line 7:
daemons: in.ftpd
clients: .the-nashes.net
access: granted

>>> Rule /etc/hosts.deny line 9:
daemons: ALL
clients: ALL
access: denied
```

**表 17-3 tcpdchk 选项**

| 选项 | 功能 |
| :--- | :--- |
| `-a` | 报告允许访问但没有显式 `ALLOW` 语句的规则。 |
| `-d` | 检查当前目录中的 `hosts.allow` 和 `hosts.deny` 文件，而不是 `/etc` 中的文件。 |
| `-i inetd_conf` | 如果不使用 `/etc` 中的当前文件，则指定 `inetd.conf` 文件的路径。 |
| `-v` | 显示所有访问控制规则。默认情况下，如果没有发现问题，则不显示任何输出。 |

提供的另一个工具是 `tcpdmatch`。其语法如下：

```
tcpdmatch [-d] [-i inet_conf] daemon client
```

`-d` 和 `-i` 选项与 `tcpdchk` 相同。`tcpdmatch` 工具允许您为系统提供理论连接并查看结果。例如，使用以下规则：

```
hosts.deny
ALL      :   ALL

hosts.allow
in.ftpd  :   .the-nashes.net
```

测试从 `norbert.the-nashes.net` 到 FTP 和 Telnet 服务器的连接将产生以下结果：

```
[root@redhat /etc]# /usr/sbin/tcpdmatch in.ftpd
jason@norbert.the-nashes.net
client:  hostname norbert.the-nashes.net
client:  address   216.254.90.133
client:  username jason

server: process in.ftpd
matched: /etc/hosts.allow line 7
access: granted

[root@redhat /etc]# /usr/sbin/tcpdmatch in.telnetd
jason@norbert.the-nashes.net
client: hostname norbert.the-nashes.net
client: address 216.254.90.133
client: username jason
server: process in.telnetd
matched: /etc/hosts.deny line 9
access: denied
```

![](img/96d9ccd181675a8ae8b6a1146c919d2b_733_0.png)
