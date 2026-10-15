
如果用户只需要 POP 或 IMAP 访问，创建一个没有有效 shell 的用户账户。该账户的用户名密码将提供 IMAP 或 POP 访问，但由于没有有效 shell，用户将无法获得登录。`/bin/false` 通常用于此类账户的 shell。对于那些也需要登录访问权限的用户，你可能需要提供安全的登录软件。

安全 shell (`ssh`) 程序是最安全的远程登录软件。它支持安全登录甚至 X Windows 访问。Linux 系统包含 `openssh`，这是一个不使用任何专利加密技术的 ssh 版本。如果你的 Linux 发行版未提供安全 shell，则可以通过网络获取。访问 `www.ssh.org` 了解有关安全 shell 的更多信息并下载最新源码。

POP 和 IMAP 服务可以使用 `stunnel` 在安全连接中运行。`stunnel` 是一个使用套接层 (SSL) 为不加密流量的守护进程加密流量的程序。在 `stunnel` 上运行时，pop 被调用并分配 TCP 端口 `995`，IMAP 被调用 `imaps` 并分配 TCP 端口 `993`。例如，同一系统可以通过 `inetd` 使用 `inetd.conf` 文件中的以下条目在 `stunnel` 中运行 `pops`：

```
pops stream tcp nowait root /usr/sbin/stunnel -l /usr/sbin/ipop3d
```

列表 12.1 显示了 Red Hat 7 系统上 `imaps` 的 `xinetd.conf` 条目。

## 列表 12.1 从 xinetd 运行 imaps 服务

```
service imaps
{
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/stunnel
    server_args = -l /usr/sbin/imapd --imapad
    log_on_failure += USERID
}
```

然而，`stunnel` 针对 POP、IMAP 或电子邮件并没有特定的特殊之处。它可以被用于保护各种守护进程。`stunnel.map` 提供了关于 `stunnel` 的更多详细信息。有关保护各种服务的更多信息，可以参考 Ramon Hontañón 编写的《Linux Security》（Syex, 2001）。

通过 `stunnel` 运行 POP 或 IMAP 的主要原因是为了确保用户的密码不会从 POP 或 IMAP 会话中被窃取，并防止被小偷用于登录服务器。`stunnel` 会加密所有内容：包括登录和邮件下载。这保证了在下载过程中，邮件内容不会被窃听者秘密查看，但从系统管理员的角度来看，保护邮件内容通常并不重要。极有可能，邮件已经通过互联网传输到了服务器。在邮件已经过全球范围暴露之后，再对其从服务器到读取器的传输过程进行加密有点愚蠢。密码实际上是你唯一想要保护的信息。使用比简单的明文密码更强形式的身份验证可以保护它。POP 通过 POP3 协议中可选的 `APOP` 命令提供了强身份验证。

为了你的 POP3 客户端提供 `APOP` 命令，你必须安装一个守护进程，例如 Qualcomm 的 `Qpopper`，它实现了该命令。`Qpopper` 可以从许多 Linux 发行版以 RPM 形式获取，并通过 `rpmfind.net` 找到。一旦安装完成，请确保 `inetd.conf` 或 `xinetd.conf` 中的 `pop` 条目指向新的 `in.qpopper` 程序。`Qpopper` 软件包添加了一个名为 `popauth` 的程序，用于为 `APOP` 命令创建密码。列表 12.2 显示了管理员如何为用户 `craig` 添加一个 `APOP` 密码。

## 列表 12.2 使用 popauth 命令

```
[root]# popauth -user craig
Changing only APOP password for craig.
New password: SecretPassword
Retype password: SecretPassword
```

## 第 12 章 Sendmail 安全

上述描述的所有内容——移除 `logind` 和 `telnetd`、将登录限制在安全 shell (`secure shell`)、创建没有登录 shell 的 POP 和 IMAP 用户、通过加密或强身份验证保护 POP 和 IMAP 密码——这些都是为了防止未经授权的登录访问。当然，登录访问可能不是你想要在 `Sendmail` 服务器上保护的唯一网络服务。要控制所有由 `inetd` 启动的服务，请使用 `wrapper`。

## 使用 Wrapper 控制网络访问

`wrapper` 守护进程名为 `tcpd`，由 `inetd` 执行。它是大多数 Linux 发行版中不可或缺的一部分。在 Linux 系统上使用 `wrapper` 比在任何其他系统上都要简单，因为 `inetd.conf` 文件中的条目已经指向了 `tcpd` 程序。列表 12.3 是 Caldera 系统 `inetd.conf` 文件的几行内容。

### 列表 12.3 Linux 预配置了 Wrapper

```
ftp stream tcp nowait root /usr/sbin/tcpd -l -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
shell stream tcp nowait root /usr/sbin/tcpd in.rshd
login stream tcp nowait root /usr/sbin/tcpd in.logind
imap stream tcp nowait root /usr/sbin/tcpd imapd
```

在 12.3 中，加粗文本被用于高亮 `inetd.conf` 文件中每一行对 `tcpd` 的引用。`tcpd` 的路径被用来代替服务守护进程的路径。因此，当 `inetd` 接收到服务请求时，它会启动 `tcpd`。

`wrapper` 具有两个基本功能：它在 `inetd` 接收到服务请求时启动 `tcpd`。`tcpd` 记录访问请求，检查控制信息，如果允许，则启动服务。`wrapper` 使用 `authpriv` 设施记录消息。在 `syslog.conf` 中查看这些消息（在 Caldera 系统上，这些消息记录在 `/var/log/secure` 中）。

## 基础安全 33

## tcpd 访问控制文件

两个文件定义了 `tcpd` 的访问控制。`hosts.allow` 文件列出允许访问的主机，`hosts.deny` 文件列出拒绝访问的主机。这两个文件的格式如下：

```
services : [shell-command]:
```

`services` 是网络服务的逗号分隔列表，也可以是关键字 `ALL`。在 `inetd.conf` 文件中，每个服务通过其紧随其后的名称来标识。`ALL` 匹配所有主机，也可以通过地址掩码匹配一个范围。域名以 `.` 开头匹配该域名内的所有主机。网络以 `.` 结尾匹配网络内的 IP 地址。

`shell-command` 是 `tcpd` 在发生匹配时执行的可选 shell 命令。如果发生匹配，`tcpd` 记录并授予或拒绝访问，然后传递 shell 命令进行执行。该功能允许你定义由匹配触发的额外处理。为了获取有关入侵者的更多信息或向系统管理员发送攻击通知，可以在 `hosts.deny` 文件中使用。

`tcpd` 首先读取 `hosts.allow` 文件，然后是 `hosts.deny` 文件。一旦发现目标主机和服务的匹配项，它就会停止。因此，通过 `hosts.allow` 授予的无法被 `hosts.deny` 覆盖。我通常在 `hosts.deny` 中插入一个条目来阻止所有系统的访问，并使用 `hosts.allow` 允许你真正想要通过封锁访问的计算机。

## 基本安全 333

列表 12.4 中的 `log_on_success` 和 `log_on_failure` 语句在连接成功或连接尝试失败时，允许将远程用户的 ID 添加到标准日志条目。`+=` 语法意味着此值被添加到已记录的其他值中。除了记录远程用户的 ID 外，`log_on_success` 和 `log_on_failure` 还允许你记录以下内容：

- `HOST`：远程主机的地址。与 `USERID` 类似，此值可用于成功和失败情况。
- `PID`：启动处理连接的服务器的进程 ID。`PID` 应用于 `log_on_success`。
- `DURATION`：记录处理此连接的服务器运行的时间长度。`DURATION` 仅适用于 `log_on_success`。
- `EXIT`：记录连接终止时服务器的退出状态。`EXIT` 仅适用于 `log_on_success`。
- `ATTEMPT`：记录失败的连接尝试。`ATTEMPT` 仅适用于 `log_on_failure`。
