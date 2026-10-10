
# 加固终端设施 (SSH)

终端流量通常来自 `Telnet` 或 `rlogin` 应用，是远程用户与 UNIX 系统交互的结果；他们可能习惯于远程连接到你的 FreeBSD，既为了使用它也为了执行管理职责。然而，使用终端是风险最高的明文流量类型——而且它最容易修复。FreeBSD 自带了一个完整的 SSH（安全外壳）软件包，设计用于补充 Telnet 和 rlogin，并最初是为 OpenBSD 开发的。OpenSSH 允许用户到你的服务器建立加密隧道，保护他们的登录密码和命令行活动免受嗅探。

SSH 服务器 `sshd` 在端口 22 上作为一个独立的守护进程运行，它像 Apache 一样，当有新连接进入时派生进程。要启用 SSH 服务器，请向 `/etc/rc.conf` 添加以下行（如果尚未添加）并重启（或直接输入 `/etc/rc.d/sshd start`）：

```
sshd_enable=YES
```

SSH 客户端是 Telnet 的替代品。要用它代替命令行 telnet 程序，请使用 `ssh` 命令：与其让服务器发出自己的 `Login:` 和 `Password:` 提示，不如由 SSH 客户端本身提示你的密码，假设用户名与本地相同。

```
ssh user@example.com
```

连接成功后，你将看到一个与 Telnet 类似的提示符。你可以指定不同的用户名，使用 `ssh 用户名@主机名`：

```
ssh myuser@example.com
```

如果你想使用非标准端口，可以使用 `-p` 选项：

```
ssh -p 2222 user@example.com
```

SSH 还允许你使用密钥对进行身份，这比密码更安全。首先，在本地上生成密钥对：

```
ssh-keygen -t rsa
```

然后使用 `ssh-copy-id` 将公钥复制到服务器的 `~/.ssh/authorized_keys` 中：

```bash
ssh-copy-id user@example.com
```

之后你登录时就不再需要输入密码了。你还可以通过修改 `/etc/ssh/sshd_config` 来配置 SSH 服务，例如禁用 root 登录：

```
PermitRootLogin no
```

修改配置后，需要重启 SSH 服务以生效：

```
/etc/rc.d/sshd restart
```

SSH 还支持端口转发（Port Forwarding），这允许你通过加密隧道访问远程服务器的服务。例如，将本地的 8080 端口转发到服务器的 80 端口：

```bash
ssh -L 8080:localhost:80 user@example.com
```

现在，你可以通过访问本地的 `http://localhost:8080` 来安全地访问服务器上的 Web 服务。

`/etc/inetd.conf`。 如果你想实施“仅允许安全连接”策略，将需要使用 IPFW（你将在本章稍后看到）禁止来自 localhost 以外的任何主机连接这些端口。

## 加固 FTP

正如你在第 27 章“配置 FTP 服务器”中所学习的，FTP 是另一种明文服务，它具有固有的密码验证机制，因此存在被监听线路的攻击者破解的风险。用户经常使用 FTP 执行上传网页等操作，但它不会像 POP3 或 IMAP 那样以预测的定期间隔使用。这使得 FTP 对你的系统的风险比 Telnet 小一些，但仍然值得加固。

幸运的是，FTP 的实现与 SSH 一样简单。如果你已经启用了 SSH（如你在本章前面的“加固终端设施 (SSH)”中所学会的那样），那么你的系统就可以提供安全 FTP。加密的 FTP 会话实际上通过 SSH 通道运行，由 SSH 客户端建立终端连接，在服务器端启动 `/usr/lib/libexec/sftp-server`，并通过加密通道向客户端打开连接。随后安全 FTP 对用户来说是透明的，就像普通的 FTP 程序一样。

在 FreeBSD 上，作为 OpenSSH 一部分的内置 sftp 服务用于处理安全 FTP 会话的客户端。在 Windows 上，SSH 通信安全包提供了一个与 FreeBSD 配合的安全 FTP 客户端。之前提到的 Mac OS (iTTYTelnet 和 MacOS) 也都具有安全 FTP 功能，且 Mac OS 拥有命令行 `sftp`。

安全 FTP 不像 FTP 那样可配置，它没有使用内置 FTP 服务器使用的任何标准配置文件。相反，你将为安全 FTP 使用与 SSH 相同的配置文件：`/etc/ssh/sshd_config`（详情请参见 `man ssh_config`）。例如，如果你想拒绝某些用户访问 FTP，必须使用 `DenyUsers` 语句，它会阻止指定的用户通过 FTP 或 SSH 访问系统：

```
DenyUsers frank joe
```

> 注意
> 安全 FTP 模型中不支持匿名 FTP。然而，由于加密的主要目的是防止系统登录用户的密码以明文形式暴露，因此对于匿名 FTP 实际上没有多少加密内容，因为它没有密码，也不与你的本地用户关联。

> 注意
> 安全 FTP (SFTP) 与 FTPS 完全不同，FTPS 是另一种加固 FTP 流量的类似解决方案。有关差异的细节，请参考 `http://www.ford-hutchinson.com/~fh-1-pfh/ftps-ext.html`。

通过安全通道执行文件传输的另一种方法是使用 `scp`。这允许你通过登录认证从远程服务器复制文件，与 `rcp` 的工作方式类似（详情参见 `man rcp` 和 `man scp`），但 `scp` 是通过加密的 SSH 隧道运行的。

使用 `scp` 从本地机器向远程 SSH 服务器传输文件，可以使用如下命令：

```bash
# file.txt stripes:
frank@stripes: password: 100% |*************************| 511 00:00
```

带有尾冒号 (:) 的远程主机名可以是源或目标参数。这两个参数中的任何一个都可以包含文件位置完整路径（例如 `scp file.txt stripes:public/html/textfiles`）。如果你不需要完整 FTP 的所有功能，使用 `scp` 是安全传输文件的快速方法。你甚至可以执行递归获取，使 `scp` 成为传输目录结构的得手工具。

## 加固 Apache

HTTP 是 Web 传输的协议，可能是今天互联网上最可见的协议，而且每天都有更敏感的信息通过 Web 传输。安全 HTTP 对电子商务至关重要，因为它保护了客户的信用卡号和账单信息——特别是对于家庭互联网用户来说，这更为关键。如果你的业务依赖于用户对处理信息时隐私性的信任，那么安全 HTTP 特别为重要。如果你打算将 FreeBSD 的旗舰 HTTP 服务器用于任何商业或隐私敏感的用途，那么加固 HTTP 是必不可少的。

加固 HTTP 是 SSL 最早的广泛用途之一。直到最近，将 Apache 与 SSL 集成一直是基于 Apache 开发产品的商业软件供应商要做的事情，而且有类似的竞争性的启用 SSL 的 Apache 版本可用。然而，自 Apache 2.0 发布以来，SSL 已经集成到默认安装的软件中，启用它的方法变得简单得多。不过，为了那些可能仍在使用 Apache 1.3 或更早版本的用户，我们涵盖了为该版本设计的 SSL 实现。

> 安全和明文 HTTP 旨在并排运行。通过 SSL 提供的所有服务并不是一个好主意，而且也很少这样做。高流量网站会因为解密每个页面（无论其是否包含敏感信息）而受到速度影响，而且便利性可能会阻碍这种做法。大多数公共 Web 数据不需要加密——毕竟，它是公开的。当客户进入在线购买页面或信息收集表单时切换到安全模式，有助于为你的用户提供保证，让他们知道现在处于一个受保护程度更高的区域。记住，你服务的不仅是用户的数据，还包括用户的预期和信任。

### Apache-SSL

Apache-SSL 是在 2.0 之前的之前 Apache 的“官方”安全实现。Apache-SSL 的功能集比 `mod_ssl` 更有限，主要关注稳定性和性能，而不是高级功能。如今 Apache-SSL 的开发已不再活跃，很大程度上是因为功能集受到严格控制且缺乏已知漏洞。

Apache-SSL 二进制文件名为 `https` 而不是 `http`；其理念是让你在 80 端口运行普通的 `httpd`，在 443 端口运行加密的 `httpsd`。你可以从端口 `/usr/ports/www/apache13` 安装带有 SSL 的 Apache，其官方网站为 `http://www.apache.org.org`。

### Apache with mod_ssl

`mod_ssl` 是比 Apache-SSL 更完整的 Apache 的 SSL 实现，它将 OpenSSL 链接到 Apache 中，利用了 Apache 的现代架构。`mod_ssl` 比 Apache-SSL 更精简，并集成了许多功能。`apache13-modssl` 端口安装单个可执行文件，类似于普通的 `apache13` 端口，其配置文件允许启用 SSL 连接：
