
```
[mary@pluto]$ ssh -L 9011:leghorn:23 underdog sleep 60
Enter passphrase for RSA key `mary@pluto':
`fwd` connect from 127.0.0.1 to local port `sshd'fwd-9011
Waiting for forwarded connections to terminate...
The following connections are open:
port 9011, connection from localhost port 1695
```

**注意**

如果 `sshFwd` 指定的端口号列在 `/etc/services` 中，则您**必须**使用名称而不是数字。例如，如果您想要转发 `http` 请求，您必须指定 `sshFwd-www` 而不能指定 `sshFwd-80`。

在我们的示例中，我们在 `pluto` 上使用了两个交互式 shell 或窗口。我们可以实现 RSA 认证并使用脚本完全自动化转发端口的构建。

事实证明，一旦执行了示例 11-34 中显示的命令，`pluto` 上的任何用户都可以执行如示例 11-35 所示的 `telnet` 命令。如果我们不信任 `pluto` 上的所有用户，这可能是一个问题。另一方面，这也意味着我们可以创建一个专门用于处理转发的用户，并通过配置该用户的 `/home/.ssh/config` 文件中的 `BatchMode` 和 `LocalForward` 关键字（见 277 页的表 11.7）并适当设置，然后脚本化该过程来自动化此过程。

**警告！**

如果您在示例 11-34 和示例 11-36 中给出的命令中添加 `-g` 选项，那么任何系统上的任何用户都能够在以下命令中使用配置的转发端口：

```
$ telnet pluto 9011
```

因此，不建议使用 `-g` 选项，因为它会创建重大漏洞。有关限制或禁用端口转发的信息，请参见下文中的*限制和禁用转发*。

## 远程转发

远程转发与本地转发非常相似。主要区别在于，我们图 11.5 中的 `underdog` 上执行转发命令。例如

```
$ ssh -R 9345:leghorn:23 pluto
```

这将导致端口 `9345` 被转发到 `leghorn` 的端口 `23`。连接建立后，Mary 随后会在 `pluto` 上执行

```
$ telnet localhost 9345
```

此机制的其他方面如第 308 页中*本地转发*所述。

### 限制和禁用转发

通过 SSH 控制端口转发的最灵活方法是使用 `/etc/hosts.allow` 和 `/etc/hosts.deny`。例如，如果我们希望只允许主机 `pluto` 在 `underdog` 上建立转发端口，我们需要在 `/etc/hosts.allow` 文件中放置条目

```
sshd:pluto:underdog
```

然后在 `/etc/hosts.deny` 文件中放置条目

```
ALL:ALL
```

将产生预期的结果。

您可以通过在服务器的 `/etc/ssh/ssh_config` 文件中将 `AllowTcpForwarding` 关键字设置为 `no` 来禁用端口转发。这将禁用服务器的所有端口转发。它并不禁用发起端口转发尝试的行为。例如，如果我们禁用了图 11.5 中 `pluto` 上的端口转发，我们仍然可以使用 `-R` 标志从 `pluto` 通过 `ssh` 在 `underdog` 上设置一个转发端口。

完全消除端口转发的唯一方法是使用编译时选项 `--disable-client-port-forwardings` 和 `--disable-client-server-forwardings`，分别用于客户端和服务器端。

> **警告！**
>
> 虽然可以通过 SSH 完全禁用端口转发，但端口转发和代理可以通过其他方式实现。例如，*第 247 页的“使用重定向属性”描述了如何使用 Xinetd 实现代理。*

# Secure Shell 的替代方案

SSH 在有限的情况下是免费的（参见第 263 页的 *SSH 的可用版本*）。有一个 GNU 项目旨在产生一个完全不受限制的 SSH，在 GPL 下分发。目前处于测试版阶段，您可以在以下网址获取有关此产品的更多信息：

`http://www.net.ut.ac.uk/psst/`

尽管 SSH 非常有用且功能强大，但它无法做到许多事情。例如，它无法通过 SSH 加密隧道转发基于 UDP 的通信，如 NIS 和 DNS 查询。为了普遍地加密任意通信，我们必须做其他事情。最简单的替代方案是在 TCP/IP 堆栈的较低层进行加密。SSH 在 TCP/IP 堆栈的应用层运行；主要的替代方案在传输层和网络层运行。

例如，`stelnet` 程序（可从 `http://www.quick.com.au/ftp/pub/sjg/` 获取）需要安全套接字层（SSL）进行加密；SSL 在传输层运行。由 Eric A. Young（SSLey）编写的 SSL 公开版本可从以下网址获取：

`http://www.psy.uq.edu.au:8080/~ftp/Crypto/`

SSLey 及相关应用程序的优势在于可以免费用于商业和非商业用途，因此比 SSH 提供更少的限制。您还将在该网站找到利用 SSL 的其他程序的列表。

另一种替代方案是互联网协议安全（IPsec），由多个互联网 RFC 标准化（关于 RFC 的更多信息，请参见第 24 页的“Request for Comment”）。它在 TCP/IP 堆栈的网络层实现加密，这增强了性能并使其对用户透明。主要的 Linux IPsec 实现项目是 Linux 免费安全广域网（FreeSwan）[1]。您可以在以下网址找到有关 Linux FreeSwan 的更多信息：

`http://www.cs4all.nl/~freeswan/index.html`

如其名称所示，该软件是免费的，并且可以从该网站下载。与许多密码学项目一样，它是在美国境外开发的，因此可以全球可用。

另一个进行中的项目是 Crypto IP Encapsulation（CIPE）。CIPE 的目的是提供 IPsec 的简单替代方案。它提供在 IP 路由器之间加密连接，包括 Linux。要了解 CIPE 的更多信息，请访问：

`http://sites.inka.de/sites/bigred/devel/cipe.html`

最终，SSH 将被 FreeSwan 或 CIPE 或类似的东西所超越，但在那之前，它为远程登录、远程执行、X 窗口系统和文件复制提供强大的加密方式。

> [1] RSA Data Security, Inc. 有一个类似的商业项目，称为 S/WAN。FreeSwan 也被称为 FreeS/WAN。

# 总结

在本章中，我们详细说明了 SSH 的实现和配置。我们展示了它可用于建立加密隧道，用于各种远程连接，包括远程登录、远程执行和复制，以及 X 窗口系统会话。它还包含多种认证机制，包括强大的 RSA 认证。我们强调使用 SSH 进行所有远程 root 访问。

# 延伸阅读

SSH 有大量的可用文档。在 SSH 发行版中，您将找到以下文档（假设 `/usr/src/ssh` 是源代码树的顶层）：

- `/usr/src/ssh/INSTALL`
- `/usr/src/ssh/OVERVIEW`
- `/usr/src/ssh/README`
- `/usr/src/ssh/README_CIPHERS`
- `/usr/src/ssh/README.DEATTACK`
- `/usr/src/ssh/README.SECURERPC`
- `/usr/src/ssh/README.SECURID`
- `/usr/src/ssh/README.TIS`

还有以下 man 手册页：

- `make-ssh-known-hosts(1)`
- `scp(1)`
- `ssh-add(1)`
- `ssh-agent(1)`
- `ssh-keygen(1)`
- `ssh(1)`
- `sshd(8)`

欲了解更多信息，请查看以下网络资源：

- `http://www.employees.org/~satch/ssh/faq/`
- `http://www.datafellows.com/`
- `http://www.ssh.fi/`
- `ftp://ftp.cs.hut.fi/pub/ssh/`

最后，您可以通过将 `subscribe ssh` 放入发送给 `majordomo@clinet.fi` 的电子邮件正文中来订阅 SSH 邮件列表。

## 你以为你有一个好密码！

# 破解

![](img/7933c44717ab0711177ea7153f959fc5_354_0.png)

您可能正在疑惑，为什么白帽黑客[2]会想要运行 `Crack`。毕竟，好人为什么想要猜测密码？不幸的是，答案是：因为坏人在这样做。所以，你必须运行 `Crack` 来找出你的用户是否选择了容易破解的密码。
