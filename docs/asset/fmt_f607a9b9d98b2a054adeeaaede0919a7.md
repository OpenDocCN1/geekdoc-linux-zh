
| `sendmail` | 邮件传输代理。 |
| `smbd` | 兼容 SMB 的服务器。 |
| `snmpd` | 网络管理服务。 |
| `squid` | HTTP (Web) 缓存。 |
| `sshd` | 安全 shell。 |
| `syslog` | 系统日志。 |
| `xfs` | 为 X 提供字体。 |
| `xntpd` | 提供时间服务。 |
| `ybind` | 绑定 NIS 客户端。 |
| `ypassword` | 允许用户更改密码。 |
| `ypserv` | 提供 NIS 服务。 |

### 表 4.3 使用 inetd 的重要 Linux 守护进程

| 守护进程 | 描述 |
|---|---|
| `auth` | 识别用户 (ident)。 |
| `bootps` | 提供 IP 地址和其他信息。 |
| `comsat` | 通知传入邮件。 |
| `exec` | 远程执行命令。 |
| `finger` | 提供 finger 命令访问。 |
| `ftp` | 在主机间传输文件。 |
| `imap` | 提供交互式邮件访问。 |
| `linuxconf` | Linux 管理工具。 |
| `login` | 提供远程登录。 |
| `netbios-ns` | NetBIOS 名称服务。 |
| `netbios-ssn` | NetBIOS 会话服务。 |
| `netstat` | 网络性能数据。 |
| `ntalk` | 远程用户通信。 |
| `pop-2` | 提供远程邮件访问。 |
| `pop-3` | 提供远程邮件访问。 |
| `shell` | 提供远程 shell 服务。 |
| `swat` | 基于 Web 的 Samba 管理。 |
| `systat` | 提供进程性能数据。 |
| `talk` | 远程用户通信。 |
| `telnet` | 提供远程登录。 |
| `tftp` | 以最小认证和开销在主机间传输文件。 |

你可以通过执行命令 `ps ax` 来确定当前运行的守护进程。

该命令的输出包含了每个守护进程关联的进程 ID (`PID`)：

| PID | TTY | STAT | TIME | COMMAND |
|---|---|---|---|---|
| 1 ? | S | 0:03 | init |
| 391 ? | S | 0:17 | syslog -m 0 |
| 402 ? | S | 0:00 | klogd |
| 430 ? | S | 0:00 | crond |
| 444 ? | S | 2:37 | apachewatch -i eth0 |
| 458 ? | S | 0:18 | named |
| 472 ? | S | 0:28 | /usr/sbin/sshd -p 23 |
| 478 ? | S | 0:14 | xntpd -A |
| 491 ? | SL | 0:00 | lpd -l |
| 506 ? | S | 0:06 | /usr/sbin/dhcpd |
| 521 ? | S | 0:00 | sendmail: accepting connections |
| 556 ? | S | 0:00 | -1 |
| on port 25 571 ttyS0 | S | 0:00 | gpm -t MouseMan |
| 585 ? | S | 0:00 | httpd |
| 602 ? | S | 0:00 | logger |

# 第 4 章 • 网络基础

685 tty3 SW 0:00 [mingetty]

686 tty4 SW 0:00 [mingetty]

688 tty6 S 0:00 /sbin/minetty tty6

690 ? S 0:04 update (bdflush)

723 tty2 S 0:00 /sbin/minetty tty2

726 tty1 S 0:00 /sbin/minetty tty1

1110 ? S 0:00 [smbd]

1121 ? S 0:09 nmbd -D

1124 ? S 0:00 [nmbd]

2803 ? SW 0:00 [rpcid]

2804 ? SW 0:00 [locked]

5873 tty5 S 0:00 /sbin/minetty tty5

15739 pts/1 R 0:00 ps x

要确定当前运行哪些守护进程正在运行，或者 inet 将启动哪些守护进程，请执行以下命令：

```
netstat -ap --inet | grep LISTEN
```

该命令报告了关联服务的端口号或名称，以及当前在端口上监听的进程 ID 和名称。如果监听进程是 `inet`，则表示该服务将在需要时由 `inet` 启动，在下方的 `netstat` 输出中所示：

```
tcp 0 0 *:1047 **: LISTEN
tcp 0 0 *:netbios-ssn **: LISTEN 1110/
tcp 0 0 *:www **: LISTEN 585/httpd
tcp 0 0 *:smtp **: LISTEN 556/-
sendmail: accep **: LISTEN 506/lpd
tcp 0 0 *:printer **: LISTEN 478/sshd
tcp 0 0 *:telnet **: LISTEN 472/named
tcp 0 0 *:domain **: LISTEN 472/named
tcp 0 0 *:localhost:domain **: LISTEN 472/named
tcp 0 0 *:linuxconf **: LISTEN 444/inetd
tcp 0 0 *:imap2 **: LISTEN 444/inetd
tcp 0 0 *:pop-3 **: LISTEN 444/inetd
tcp 0 0 *:ftp **: LISTEN 444/inetd
tcp 0 0 *:sunrpc **: LISTEN 344/mapport
```

现在完成练习 4.1，以获得运行守护进程的经验。

### 练习 4.1

#### 列出守护进程

要查看你的系统中运行了哪些守护进程，请执行以下步骤：

- 1. 在 Linux 系统上运行 `ps` 命令，识别正在运行的守护进程。
- 2. 在 Linux 系统上运行 `netstat` 命令，识别正在运行的守护进程以及将由 `inetd` 启动的守护进程。

大多数服务都可以配置为持续运行，或仅在由 `inetd` 启动时运行。然而，从性能考虑，服务应该持续运行。例如，安全外壳服务（SSH）在启动时必须计算加密密钥。在 `inetd` 的控制下运行 SSH 意味着每次客户端连接都要进行这种耗长的计算。最好持续运行 SSH，这样客户端就可以获得快速的服务。

### 控制守护进程

Red Hat Linux 为每个安装的守护进程提供了一个脚本。该脚本可以执行以下操作：

- 启动守护进程
- 停止守护进程
- 重启守护进程
- 显示与守护进程相关的状态信息

执行这些功能的脚本存储在 `/etc/rc.d/init.d` 目录下。该目录下并不是所有脚本都与守护进程有关。例如，某些由 `inetd` 启动的守护进程在该目录下可能有脚本。同样，目录中的某些脚本属于系统设置任务而非守护进程。你可以通过名称区分控制守护进程的脚本，这些名称与表 4.2 和 4.3 列出的守护进程名称相似。你也可以检查脚本以解释其用途。

### 启动守护进程

要启动守护进程，请采取以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令

```
xxx start
```

其中 `xxx` 是与守护进程关联的文件名。
- 3. 检查系统日志 `/var/log/messages` 中的错误信息。

### 停止守护进程

要停止守护进程，请采取以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令

```
xxx stop
```

其中 `xxx` 是与守护进程关联的文件名。
- 3. 检查系统日志 `/var/log/messages` 中的错误信息。

### 重启守护进程

要重启守护进程，请采取以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令

```
xxx restart
```

其中 `xxx` 是与守护进程关联的文件名。
- 3. 检查系统日志 `/var/log/messages` 中的错误信息。

某些守护进程（如 `nfsd`）有时可能无法正常重启。在这种情况下，你可能倾向于停止然后启动守护进程。

### 显示守护进程的状态

要显示守护进程的状态信息，请采取以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令

```
xxx status
```

其中 `xxx` 是与守护进程关联的文件名。

总结 101

现在完成练习 4.2，以获得运行守护进程的经验。

### 控制守护进程

要控制守护进程，请采取以下步骤：

- 1. 查看系统中运行了哪些守护进程。
- 2. 在 `/etc/rc.d/init.d` 目录下执行命令：
