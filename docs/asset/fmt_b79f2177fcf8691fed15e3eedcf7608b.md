
**program** 是要执行的程序。

**arguments** 与程序相关的参数。

本章描述的守护进程有：

| | |
|---|---|
| `fingerd` | 提供 finger 服务。 |
| `erd` | 提供 finger 服务。 |
| `ftpd` | 提供 ftp 服务。 |
| `gated` | 处理网络路由。 |
| `gde` | 控制 `gated` 的程序。 |
| `identd` | TCP/IP 标识协议。 |
| `imapd` | 远程邮件访问。 |
| `inetd` | 根据需要调用其他守护进程。 |
| `klogd` | 内核日志守护进程。 |
| `lpd` | 提供行打印服务。 |
| `mountd` | NFS 挂载守护进程。 |
| `named` | 域名服务。 |
| `pppd` | 处理对点协议通信。 |
| `reexecd` | 远程命令执行。 |
| `rlogin` | 远程登录 |
| `rcmd` | 远程命令执行 |
| `rshd` | 远程命令执行。 |
| `rwhod` | 提供 rwho/runtime 服务 |
| `syslog` | 系统日志守护进程。 |
| `talk` | 两个用户之间的通信 |
| `tcpd` | Internet 服务的访问控制。 |
| `telnetd` | 提供 telnet 服务。 |
| `tftpd` | 提供 tftp 服务。 |
| `yppasswdd` | 修改密码 |

## 相关文件

| | |
|---|---|
| `/usr/tmp/gated/dump` | `gated` 将状态信息写入此文件 |
| `/etc/gated.conf` | `gated` 的配置文件 |
| `/etc/gated.pid` | `gated` 写入其进程 ID 的文件 |
| `Comm/etc/gated.conf+` | 由 `gdc` 安装的新 `gated` 配置文件 |
| `/etc/gated.conf-` | 被 `gdc` 替换的旧 `gated` 配置文件 |
| `/etc/gated.conf--` | 被 `gdc` 替换了两次的老旧配置文件 |
| `/etc/printcap` | 打印机描述文件 |
| `/var/spool/*` | 打印池目录 |
| `/dev/lp*` | 行打印设备 |
| `/dev/printer` | 用于本地请求的套接字。 |
| `/etc/hosts.equiv` | 列出允许打印机访问的机器。 |
| `/etc/hosts.lpd` | 列出允许打印机访问的机器，但不处于相同的管理控制下。 |
| `/etc/named.conf` | 默认名称服务器配置文件。 |
| `/var/run/named.pid` | `named` 的进程 ID。 |
| `/var/tmp/named_dump.db` | 名称服务器数据库的转储。 |
| `/var/tmp/named.run` | Named 的调试输出。 |
| `/var/tmp/named.stats` | 域名服务器统计数据。 |

## 命令

### `fingerd [-wul] [-pL path]`

返回关于系统或特定人员的可可读状态报告。该命令的选项应在 `/etc/inetd.conf` 中指定。

示例：此守护进程通常由 `inetd` 调用（它使用 `tcpd` 提供访问控制和日志服务）。要启动 `fingerd`，请向你的 `inetd.conf` 文件中添加以下行：

```
finger stream tcp nowait root /usr/sbin/tcpd in.fingererd
```

- `-w` 告诉 `fingerd` 在输出中包含包含某些系统信息（运行时间、操作系统名称、版本）的欢迎横幅
- `-u` 拒绝所有格式为 "`finger@host`" 的请求。
- `-l` 记录有关请求的信息。
- `-p` 指定 `fingerd` 查找 finger 程序的替代位置。

### `ftpd [-d] [-v] [-l] [-timeout] [-Tmaxtimeout] [-a] [-A][-L][-i][-o] -umask`

`ftpd` 是文件传输协议服务器。

示例：此守护进程通常通过 `tcpd` 守护进程由 `inetd` 调用（提供日志和访问控制）。要带有日志 (`-l`) 和访问控制 (`-a`) 的 `ftpd`，请向你的 `inetd.conf` 文件中添加以下行：

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -l -a
```

- `-d`, `-v` 将调试信息发送到 `syslog`。
- `-l` 将每个 ftp 会话的信息记录到 `syslog`。
- `-a` 启用使用 `ftppasssecs` 配置文件。
- `-A` 禁用使用 `ftppass` 配置文件。
- `-L` 将所有发送到 `ftpd` 服务器的命令记录到 `syslog`。
- `-i` 将所有接收的文件记录到 `xferlog`。
- `-o` 将所有传输的文件记录到 `xferlog`。
- `-u` 指定默认的 `umask`。

### `gated [ -c ] [-C] [-n] [-N] [-t trace_options ] [ -f config_file ] [ trace_file ]`

`Gated` 是一个处理各种路由协议的路由服务。它可以配置为它能够处理的部分或全部协议。

**示例：** 通过 `gdc` 调用此命令是一个好主意。但在命令行中作为后台进程 (&) 运行它，请输入：

```
gated &
```

- `-C` 告诉 `gated` 解析配置文件，报告任何语法错误并退出。
- `-C` 告诉 `gated` 解析配置文件以检查语法错误。
- `-n` 禁止 `gated` 修改内核转发表。
- `-N` 告诉 `gated` 不要作为守护进程运行。
- `-t trace_options` 允许用户在命令行上指定用逗号分隔的跟踪选项列表。
- `-f config_file` 指定非默认的配置文件。

### `gdc [ -q ] [ -n ] [-c coresize ] [ -t filesize ] [-m datasize ] [ -s stacksize ] [ -t seconds ] command`

此命令是 `gated` 控制器，用于控制 `gated` 路由守护进程的用户界面。你可以使用它停止、启动、发送信号、维护配置文件以及生成或维护核心转储。

示例：调用 `gated` 并将所有输出发送到系统日志：

```
gdc -q start
```

为了让这些控制生效，你必须使用 `gdc` 启动 `gated`。

- `-n` 不检查内核转发表。
- `-q` 静默操作。将任何输出记录到系统日志。
- `-t seconds` 允许用户指定 `gdc` 等待 `gated` 完成启动、关闭和其他操作。
- `-c coresize` 指定 `gated` 可能生成的核心转储大小的上限。通常用于当系统默认值小到无法使用时增加它。
- `-f filesize` 指定由 `gdc` 启动的 `gated` 可以产生的最大文件。
- `-m datasize` 指定由 `gdc` 启动的 `gated` 数据段大小的上限。
- `-s stacksize` 指定由 `gdc` 启动的 `gated` 栈的最大。

在命令行上可以指定以下操作：

- `checkconf /etc/gated.conf` 检查语法错误。
- `checknew /etc/gated.conf+` 检查语法错误。
- `newconf` 用 `/etc/gated.conf-` 替换 `/etc/gated.conf`。
- `backout` 将旧配置文件 (`/etc/gated.conf-`) 移回位置作为当前活跃的 `gated`。同时将当前的 `/etc/gated.conf` 轮转到 `/etc/gated.conf+`
- `BACKOUT` 与 `gated`（上述）相同，但将覆盖现有的 `/etc/gated.conf+`
- `modeconf` 将所有配置文件设置为模式 664，owner=root
- `modeconf` 将所有配置文件设置为模式 664，所有者=root。

## 命令

- `checkconf /etc/gated.conf` 检查语法错误。
- `checknew /etc/gated.conf+` 检查语法错误。
- `newconf` 用 `/etc/gated.conf-` 替换 `/etc/gated.conf`。
- `backout` 将旧配置文件 (`/etc/gated.conf-`) 移回位置作为当前活跃的 `gated`。同时将当前的 `/etc/gated.conf` 轮转到 `/etc/gated.conf+`
- `BACKOUT` 与 `gated`（上述）相同，但将覆盖现有的 `/etc/gated.conf+`
- `modeconf` 将所有配置文件设置为模式 664，owner=root
- `modeconf` 将所有配置文件设置为模式 664，所有者=root。

## 命令

- `-i` 将所有接收的文件记录到 `xferlog`。（等待，重复部分）
