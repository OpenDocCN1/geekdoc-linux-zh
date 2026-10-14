
# 348 第 16 章 通过 ssh (安全外壳) 进行隧道传输

关于可以在 `/etc/sshd_config` 文件中提供的其他关键字（例如与通过 `.hosts` 和 `/etc/hosts.equiv` 文件进行身份验证相关的关键字），请参阅 `sshd` 手册页。注意，默认的 `/etc/sshd_config` 是相当新的，因此用户应尽可能编辑它，而不是从头开始。

## 配置 ssh

`ssh` 配置通常存储在 `/etc/ssh_config` 文件中。`/etc/ssh_config` 文件分为若干节，每个节以 `Host` 关键字开头，后跟一个匹配并应用于该节的主机的模式。在每个节内有多个关键字和值对，每个对单独一行。在 `/etc/ssh_config` 中可能出现的常用关键字见表 16.2。

### 表 16.2 `ssh` 已知的常用关键字

| 关键字 | 描述 |
| --- | --- |
| Cipher type | 指定用于连接连接上数据加密的算法类型。有效的方法有 idea, des, 3des, blowfish, arcfour，或者默认不进行加密。默认使用 idea，并应注意并非所有方法在所有系统上都可用。 |
| Compression yes\|no | 指定默认是否使用压缩。 |
| CompressionLevel n | 指定 `ssh` 应使用 `gzip` 连接压缩数据流。压缩级别 1 是最不消耗处理器资源的方法，但压缩率最低。压缩级别 9 产生更好的压缩效果，但更消耗主机资源。 |
| ConnectionAttempts n | 指定在 `ssh` 回退到 `rsh`（见下一个关键字）或放弃之前的最大连接尝试次数 n。 |
| FallBackToRsh yes\|no | 指定如果 `ssh` 在 `ConnectionAttempts` 指定的次数后无法连接到远程主机，是否将使用 `rsh`。 |
| ForwardX11 yes\|no | 如果为 yes，`ssh` 将通过隧道服务器自动重定向 X11。 |
| NumberAndPassword n | 指定 `ssh` 在放弃之前应尝试身份验证 n 次。 |
| PasswordPrompt yes\|no | 指定在提示密码时是否显示用户名。 |
| PasswordLogin yes\|no | 指定在提示密码时是否显示。 |
| Port n | 指定 `ssh` 在端口 n 上尝试连接。默认值是 22。 |
| XauthLocation path | 指定 `xauth` 程序的路径。 |

注意，尽管全局 `ssh` 配置存储在 `/etc/ssh_config`，但每个用户可以有一个格式相同的个性化 `ssh` 文件。有关 `ssh` 支持的关键字的完整细节，请参考 `ssh`。

## 与 X 使用 ssh

使用 X 时有两种主要数据需要加密：一种是基于 cookie 的传输；另一种是 X 数据流本身。注意 `ssh` 在隧道 X 数据流时会自动交换 cookie，因此实际上在安装 `ssh` 后，你很少手动交换 cookie。

在完成任何形式的安全传输之前，必须在机器上运行 `ssh` 守护进程。

## 启动 ssh 守护进程

`ssh` 可以从命令行启动。只需变为 root 并执行以下命令：

```
/usr/local/sbin/sshd
```

由于 `ssh` 自认为是一个守护进程，它会将自己放入后台。对于持续使用 X 的系统，在初始化过程中插入对 `sshd` 的调用将帮助。此过程将在 `/etc/rc.d/rc.local` 文件或更早阶段进行。`etc/rc.d/rc.local` 的可能添加内容为

```
/bin/echo -n 'Starting sshd: '
if [ -x /usr/local/sbin/sshd ]; then
  /usr/local/sbin/sshd
  /bin/echo done
else
  /bin/echo not found
fi
```

某些用户可能反对每次请求连接都通过 `inetd` 启动 `ssh` 的想法。当命令行提供了 `-i` 选项时，`ssh` 守护进程可能希望 `inetd` 启动 `ssh` 以允许这种功能。要让 `inetd` 在每次入站连接启动时启动 `ssh`，编辑 `/etc/services` 文件以包含以下行：

```
ssh 22/tcp secure shell
```

然后，编辑 `/etc/inetd.conf` 文件以包含以下行：

```
ssh stream tcp nowait root /usr/sbin/tcp /opt/bin/sshd -i
```

进行更改后，使用挂起信号重启 `inetd` 服务器，使其重新读取配置文件：

```
killall -HUP inetd
```

现在，每当有传入的 `ssh` 连接时，`ssh` 服务器都应该自动启动。请注意，动态启动 `sshd` 仅在较快的系统上有效；在较慢的系统上，每次启动时生成服务器密钥所需可能会导致连接超时。

关于 `/etc/services` 和 `/etc/inetd.conf` 文件的格式的更多信息，请分别查看 `services` 和 `inetd` 的手册页。

## 使用 ssh 传输魔术 Cookie (Magic Cookies)

回想第 15 章，我们引入了以下命令来方便将魔术 Cookie（magic cookie）从一个主机传输到另一个主机：

```
xauth extract :0 | rsh foobar xauth merge -
```

该命令的作用是将本地显示器的 magic cookie 传输到主机，以便 `foobar` 的客户端可以连接到本地 X 服务器。这种技术唯一的问题是 magic cookie 是通过 `rsh` 以明文形式在网络上传输的，因此整个过程很容易受到不法第三方的破解。

如果用 `ssh` 命令代替 `rsh`，由于数据是加密的，该过程就会自愈：

```
xauth extract :0 | ssh foobar xauth merge -
```

如果你是第一次运行 `ssh` 命令，可能需要等待一会儿来生成随机种子，并且你可能会看到几行状态文本。系统还会提示你输入远程系统的密码；在提示处输入密码后，cookie 就会通过加密通道进行传输，并安全地合并到远程主机 `foobar` 的 `$HOME/.xauthority` 文件中。

## 使用 ssh 建立 X 会话隧道

由于 `ssh` 采用了一种自动为 X 会话建立隧道机制，启动远程客户端的过程非常简单。在大多数情况下，你只需执行类似下面的命令即可：

```
ssh foobar /usr/X11R6/bin/xterm
```

在请求密码后，一个新的 `xterm` 窗口出现在 `foobar` 主机的显示器上。要查看加密连接的证据，可以尝试在新 `xterm` 窗口中使用 `netstat` 命令，或者在新的 `xterm` 窗口中检查 `DISPLAY` 变量：

```
user@foobar echo $DISPLAY
foobar:10.0
User@foobar$
```

## 更多关于 ssh

注意，显示数字不是 0 或其他已存在的显示，而是一个比任何现有显示数字都大的数字（通常是 10）。这就是 `ssh` X 协议运行的证据；X 数据流正通过加密通道传输。在通过网络接口连接客户端到 X 服务器时，始终使用 `ssh` 是一项良好的策略，并指示用户也这样做。

任何可以通过其他方式在网络上启动的 X 客户端，也可以通过安全的 `ssh` 通道进行网络连接。当与基于令牌的认证结合时，`ssh` 提供了可用于保护 X 服务的最佳方法之一，而且比管理 Kerberos 等备用服务要容易得多。

## 接受传入的加密 X 连接

在 `sshd` 服务器运行或配置为在本地显示器上运行之后，为了安全地接收和管理传入的 X 客户端请求，实际上不需要做更多事情。

`sshd` 守护进程与现有的访问控制机制（基于主机和基于令牌的）共同工作，并在 `/etc/sshd_config` 文件中实现了了自己的若干种访问控制机制。

## 更多关于 ssh

本章暗示了 `ssh` 跨加密通道隧道其他类型网络协议的能力。`ssh` 还有其他用法，例如使用类似于 `$HOME/.hosts` 的访问，避免了用户为每次连接提供密码的需求。

关于多主机环境下的 `ssh` 配置以及 `ssh` 的许多用处的完整讨论超出了本书的范畴。然而，互联网上有许多良好的资源，旨在帮助系统管理员安装和充分使用 `ssh`。一些帮助你熟悉 `ssh` 的信息可以在以下链接中找到：

- http://www.ssh.org/
- http://www.tac.ny.us/
- http://www.csu.berkeley.edu/
- http://www.employees.org/

接受传入的加密 X 连接

在 `sshd` 服务器运行或配置为在本地显示器上运行之后，为了安全地接收和管理传入的 X 客户端请求，实际上不需要做更多事情。

`sshd` 守护进程与现有的访问控制机制（基于主机和基于令牌的）共同工作，并在 `/etc/sshd_config` 文件中实现了了自己的若干种访问控制机制。

## 更多关于 ssh
