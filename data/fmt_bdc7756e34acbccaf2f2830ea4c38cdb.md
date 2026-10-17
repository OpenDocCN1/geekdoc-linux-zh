
```
mysurfboard.com ERROR:"Domain does not exist"
justin@lizard.mytrek.com "Moved to Hawaii"
secretproject@rabbit.mytrek.com REJECT
cyberspammer.com REJECT
```

你的发行版的 `smb.conf` 可能配置 `Sendmail` 使用 `access_db`（如 Red Hat 的情况）。仅允许本地主机上的用户访问。如果你的系统用作网络的邮件服务器，并且你未启用 `relay_entire_domain` 功能，则需要允许网络上的其他主机访问。在 `access` 文件中，你可以为你的网络放置一条 `RELAY` 规则。`RELAY` 规则将允许其他主机使用你的邮件服务器向其他主机发送消息。这通常是为需要将本地网络的消息中继到互联网的网关主机所做的。以下示例允许来自 `mytrek.com` 网络的访问：

```
mytrek.com RELAY
```

对于特定主机，将其条目放在 `access` 文件中，如下所示：

```
rabbit.mytrek.com RELAY
```

为了进一步保护 `Sendmail`，你应该禁用 `VRFY` 的使用。此选项允许远程用户尝试验证用户地址是否存在。这可用于猜测系统上的有效用户。此选项可通过 `noverify` 功能禁用：

```
FEATURE('noverify')dnl
```

另一个潜在的安全漏洞是 `EXPN` 选项，它会将邮件列表和别名扩展为其实际地址。使用 `noexpn` 功能将其关闭：

```
FEATURE('noexpn')dnl
```

默认情况下，`Sendmail` 将拒绝来自无法解析的任何域的邮件。你可以使用 `accept_unresolvable_domains` 功能覆盖此限制。`Sendmail` 还会拒绝地址不具有完全限定域名的邮件。你可以使用 `accept_unqualified_senders` 覆盖此功能。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_575_0.png)

## ABC Amber CHM 转换器试用版

请注册以移除此横幅。

http://www.processestext.com/abcchm.html

### POP 服务器

邮局协议（`POP`）允许远程服务器为用户保存邮件，以便用户在准备好时从中获取邮件。与直接将邮件消息传递到 Linux 系统上的用户账户的 `Sendmail` 和 `procmail` 不同，`POP` 协议会保留邮件，直到用户访问 `POP` 服务器上的账户。然后 `POP` 服务器将收到的任何消息传输到用户的本地邮箱。服务器通常由 ISP 用于为用户提供互联网邮件服务。不是直接将邮件发送到用户的机器，邮件会保留在 `POP` 服务器中直到被检索。Linux 发行版通常安装华盛顿大学的 `POP` 服务器。其他流行的 `POP` 服务器有 `Qpopper`、`Qmail POP` 服务器和 `Courier POP` 服务器。

你可以从不同的主机访问 `POP` 服务器；然而，当你这样做时，所有消息都会传输到该主机。它们不会保留在 `POP` 服务器上（尽管你可以设置选项来保留它们）。`POP` 服务器只是将你的消息转发到请求的主机上。当你从某台计算机访问你的消息时，它们将被传输到该计算机并从 `POP` 服务器中删除。如果你再次从不同的计算机访问你的 `POP` 服务器，那些之前的消息将不复存在。

`POP` 协议提供了一组命令，你可以使用它们直接测试 `POP` 服务器。你可以使用 `Telnet` 通过 110 端口访问 `POP` 服务器，然后输入一系列 `POP` 命令来检查服务器的性能。以下示例使用 `Telnet` 通过 110 端口连接到 `turtle.mytrek.com` `POP` 服务器：

```
telnet turtle.mytrek.com 110
```

然后你可以使用 `USER` 和 `PASSWORD` 命令登录账户。`LIST` 命令将列出消息，`RETR` 命令将显示一条消息。使用 `DELE` 删除消息。使用 `QUIT` 命令结束会话。

注：`POP` 协议的当前版本称为 `POP3`，而 `POP2` 是较早的版本，在某些地方仍可能在使用。

注：Red Hat 包含的 `IMAP` 和 `POP` 服务器都提供 `SSL` 加密以实现安全的电子邮件传输。你也可以使用 `stunnel` 运行 `IMAP` 和 `POP` 服务器以提供类似的安全性。`stunnel` 是 `imapd`、`popd` 甚至 `pppd`（调制解调器连接）等守护进程的 `SSL` 包装器。在服务的 `xinetd` 脚本中，你可以使用 `stunnel` 命令调用服务器，而不是直接运行服务器。

#### 华盛顿 POP 服务器

Linux 发行版包含华盛顿大学的 `POP` 服务器（`ftp.cac.washington.edu/imap`），它是华盛顿大学 `imap` `RPM` 包的一部分。只需安装该包，它已作为标准安装的一部分完成（`POP2` 和 `POP3` 服务器均已安装）。服务器守护进程称为 `ipop2d` 和 `ipop3d`。然后你的 Linux 系统作为网络的 `POP2` 和 `POP3` 服务器运行。这些服务器通过 `xinetd` 运行。`POP3` 服务器使用 `/etc/xinetd.d` 中的 `ipop3` 文件。

以下命令将打开服务器：

```
chkconfig ipop3 on
```

```
chkconfig pop3s on
```

此外，你还必须将相应的 `SSL POP` 和 `IMAP` 证书安装到 `ssl/certs` 目录下，文件名分别为 `ipop3d.pem` 和 `imapd.pem`。

#### Qpopper

`Qpopper` 是当前版本的 Berkeley `POP` 服务器（`popper`）。`Qpopper` 由 Eudora 邮件软件开发商高通公司（`Qualcomm`）提供支持。`Qpopper` 的网页是 `www.eudora.com/qpopper`。你可以从 `ftp.qualcomm.com/eudora/servers/unix` 获取当前的源代码版本。`RPM` 包版本位于发行版站点，或包含在发行版中。

一旦你安装了 `Qpopper` 并且 `POP` 服务器正在运行，你就可以添加用户账户。然后，远程系统上的用户可以通过各种邮件客户端或 `Fetchmail` 访问 `POP` 服务器。`Fetchmail`（如第 13 章所述）将从用户账户获取邮件，并将其放置在用户本地主机上的邮箱中。以下示例从运行在 `turtle.mytrek.com` 上的 `POP` 服务器获取邮件：

```
fetchmail -p POP3 -u chris turtle.mytrek.com
```

你可以在 Linux 系统上安装 `Qpopper` 软件，并让它作为你网络的 `POP` 服务器运行。它由 `qpopper` 守护程序和 `popauth` 程序组成，后者管理带有密码加密的认证数据库，以提供安全用户访问。`popauth` 创建一个名为 `/etc/pop.auth` 的数据库文件。要添加用户，请输入 `popauth` 命令，并加上 `--user` 选项和用户名。然后，系统会提示输入密码，该密码用于让用户访问其 `POP` 账户。

如果你下载的是源代码版本，你需要使用 `./configure`、`make` 和 `make install` 序列来配置、编译和安装服务器。在 `configure` 阶段，你可能需要输入几个选项以使 `Qpopper` 与你的系统兼容。例如，如果你的系统使用影子密码（大多数系统都是这样），你需要使用 `--enable-specialauth` 选项。`--enable-apop` 选项启用 `APOP`（认证 `POP`）扩展，提供由 `popauth` 命令管理的加密：

```
./configure --enable-specialauth --enable-apop
```

`Qpopper` 通常通过 `xinetd` 运行。你需要在 `/etc/xinetd.d` 目录下创建一个类似以下所示的 `popper` 文件：

```
service pop-3
{
    socket_type = stream
    wait        = no
    user        = root
    server      = /usr/bin/popper
    disable     = no
}
```

你可以使用 `chkconfig` 命令开启或关闭服务器：

```
chkconfig pop-3 on
```

请确保 `/etc/services` 中列出了 `pop-3` 服务及其端口 110：

```
pop-3 110/tcp
```

![](img/32a48d8db4c23e6e2eb70d1e5034c976_578_0.png)

## ABC Amber CHM Converter 试用版

请注册以移除此横幅。

http://www.processestext.com/abcchm.html

### IMAP
