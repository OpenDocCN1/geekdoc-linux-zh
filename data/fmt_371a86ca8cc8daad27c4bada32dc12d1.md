
`<service_name> <socket_type> <proto> <flags> <user> <server_path> <args>`

`/etc/inetd.conf` 中条目的顺序随操作系统而异，某些操作系统具有其他系统不具备的条目，但我将涵盖许多常见的 `/etc/inetd.conf` 项目。你将按照你的 SunOS 版本中它们出现的顺序来熟悉这个基础文件。

`/etc/inetd.conf` 以 FTP 和 Telnet 的条目开始。此时，你可能出于个人目的需要这些服务，因此你应该保持这些服务开启。不过到今天结束时，你将会关闭 Telnet。

如果你在 `inetd.conf` 中有 `gopher` 条目，在行前放置 `#` 来关闭该服务。现在已经没有人使用 `gopher` 了。

我的 `/etc/inetd.conf` 有一个名称服务器协议的条目，它已经将其描述为过时。如果你运行的是更更新的操作系统，你可能没有那个条目。如果你有，将其注释掉是安全的。

接下来，我有描述 BSD 协议的 `inetd.conf` 条目：

```
# shell stream tcp    nowait root    /usr/inetd/rshd      in.rshd

# login stream tcp    nowait root    /usr/inetd/rlogind   in.rlogind

# exec stream tcp      nowait root    /usr/inetd/rexced      in.rexced

# comsat dgram udp     wait   root    /usr/inetd/in.comsat   in.comsat

# talk dgram udp       wait   root    /usr/inetd/in.talked    in.talked
```

以下是代码的拆解：

- `shell` `exec` 允许用户在不需要实际登录的情况下远程访问你的机器。
- `login` 支持一种比 Telnet 稍微安全一点、但仍然完全不安全的 `login` 协议。
- `comsat` 通知想要知道新邮件何时送到的的用户。
- `talk` 允许用户之间进行实时对话，而不是发送电子邮件并来回回复。

## 防御你的机器和加密流量

虽然这些功能大部分都非常方便，但它们都是安全风险且并非必要的。除非你绝对需要它们，否则你应该注释掉所有这些条目。

`inetd.conf` 中紧跟在 BSD 协议之后的是 `uucp`（UNIX-to-UNIX 拷贝）条目以及 `tftp` 的条目：

- `uucp` 协议曾在黑暗时代用于连接 UNIX 机器，现在已很大程度上被废弃。
- `tftp` 是“简易文件传输协议”，一种用于启动无盘或近无盘机器的服务。

你可以安全地注释掉 `uucp` 行，除非你正尝试为临时连接的节点提供虚拟网络服务——这不是核心系统要做的事！

注释掉 `tftp` 服务，除非你的机器是其他机器的启动服务器。

接下来，我有 `finger`、`netstat` 和 `sysstat` 的条目：

```
# finger stream tcp nowait nobody /usr/etc/in.finger in.fingered

# sysstat tcp nowait root /usr/bin/ps ps -auwwxx

# netstat streams tcp nowait root /usr/ucbd/netstat -f inet
```

这些服务可以提供关于你的系统信息，这些信息对黑客来说可能更有用。其中某些项可能已经在你的文件中被禁用了：

- `sysstat` 向远程用户提供你机器上运行的进程信息。
- `netstat` 向远程用户提供你机器的网络信息。
- `finger` 向远程用户提供关于你机器的用户信息。

`sysstat` 和 `netstat` 都应该被禁用。如果 `finger` 没有被禁用，请禁用它。`finger` 对于那些与你的某个用户通信并希望双重检查有关该用户信息的人可能很有帮助。另一方面，它也不必要地提供了关于你的用户是谁的信息，而这些人可能正在尝试猜测他们可以在你的系统中使用的潜在用户名。

我的 `inetd.conf` 后面包含几个关于时钟同步的条目，以及 `echo`、`discard`、`daytime` 和 `charge` 的条目，这些被描述用于测试目的。注释掉所有这些服务是可以的。

如果你的 `inetd.conf` 有 `pop` 或 `imap` 的条目（两者都提供读取服务），请禁用它们。在现在这些无疑是不必要的服务。IMAP 在黑客之间变得越来越流行。

## 282 天第 10 天

接下来我的 `inetd.conf` 列出了 RPC（远程过程调用）服务。它们以基本形式列出：

```
<rpc_prog>/<vers><socket_type>/<proto> <flags> <user> <path> <args>
```

总来说，它们在 `/etc/inetd.conf` 中的出现与 TCP 服务没有太大区别。你在这里看到的某些服务有 `mount`, `rexd`, `ypupdated`, `ruserd`, `spayd`, `walld` 和 `rquotad`。

- `mount` 被 NFS 服务器机器使用。

如果你的机器不会将任何文件系统保存到其他机器，请禁用此服务。虽然你可能会在这里看到出此服务，但在某些操作系统（如 SunOS）上，它可能会列出并注明它实际上是从别处启动的。在其他系统（如 IRIX）上，它确实是从 `inetd.conf` 启动的。在其他系统（如 Linux）上，它可能根本不会出现在 `inetd.conf` 中。如果不需要它，请查找并禁用它。

- `ypupdated` 用于 NIS 更新。

直到最近，我在办公室的 SunOS 机器上一直运行此服务，在一次安全扫描后，我收到了禁用它的建议。因为 SunOS 机器目前是 NIS 主服务器，我有点不舍这样做，但在调查之后，我发现它似乎并没有实际在做任何事情。它有一个 Bug，Sun 建议禁用它。

- `rexd` 为用户提供极简形式身份验证。
- `ruserd` 向远程用户提供用户信息。

`ruserd` 和 `rexd` 都是安全风险，应该被禁用。

- `rquotad` 用于为 `nfs` 挂载机器强制本地用户配额。

你是否需要此服务取决于你是否需要对用户执行限制。

- `spray` 用于网络测试。它接受来自网络的数据包，更多信息见第 21 章。

如果你不需要此服务，请禁用它。它并不产生安全风险，但可以被拒绝服务攻击。

- `walld` 允许远程用户向机器上的控制台写入消息。

你可以安全地禁用此服务。`inetd.conf` 描述了允许网络上的所有人。

### 防御你的机器和加密流量

在 `inetd.conf` 的 RPC 服务部分中包含了一些厂商特定的服务。禁用你确定不需要的项。

如果你使用的是 SGI 或 Sun 并且有 ToolTalk 数据库的条目，请禁用它。SGI 和 Sun 都建议禁用此服务。

你的 `inetd.conf` 到此结束。然而，IRIX 的版本也列出了 TCP。在 IRIX 6.5 下，这些服务仅用于打印和扫描。再次，禁用你不需要的。

完成你的更新并保存更改。编辑文件并不足以让更改生效。你现在需要告诉 `inetd` 重新读取配置文件。你有两种方法可以实现。如果你的 `/etc/inetd.conf` 列出了推荐的方法，请使用那一个。如果没有，使用 `ps` 找到 `inetd` 的 PID 并向 `inetd` 发送挂起信号。当下次监控的服务有请求时，它将重新读取配置文件。这种第二种方法对于任何操作系统都有效。

这是我在我的机器上需要做的：

```
Barracuda# ps -aux | grep inetd

root      197 0.0 0.6 32 196 co S    11:50 0:00 grep inetd

root      149 0.0 0.0 52  0 ? IW    03:29 0:00 inetd
```

```
Barracuda# kill -HUP 149
```
