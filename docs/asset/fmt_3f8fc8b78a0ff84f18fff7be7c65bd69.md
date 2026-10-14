
所有者权限设置中的 `s`（`rws`）告诉你已设置了 setuid 权限。

## 加固网络安全

为了确保你的 SUSE Linux 系统的安全，你必须同时关注主机安全和网络安全。这两种安全之间的区别某种程度上是任意的，因为保护网络涉及到修复主机上与你系统提供的 Internet 服务相关的问题。在本节中，我将解释你如何加固网络（主要通过不提供不必要的服务）、你如何使用防火墙阻止未指定的网络数据包到达你的网络，以及如何使用 Secure Shell（SSH）进行安全的远程登录。

## 加固 Internet 服务

对于连接互联网的 Linux 系统（即使是未连接互联网的局域网），一个重大威胁是有人可能利用许多 Internet 服务之一获取你系统的访问权限。每种服务（如邮件、Web 或 FTP）都需要一个服务器程序，在 TCP/IP 网络上响应客户端的请求。其中某些服务器程序存在漏洞，可能允许外部人员登录你的系统——可能还拥有 root 权限。幸运的是，Linux 自带了你可以利用的设施来使 Internet 服务更加安全。

![](img/6a2cbfe493abd0ba9453aa49df7301b4_322_0.png)

潜在的入侵者可以采用扫描工具——一种尝试与某个端口建立 TCP/IP 连接并寻找响应的程序——来检查你的系统上运行了哪些互联网服务器（Internet servers）。然后，入侵者可能会利用其中一个或多个服务的任何已知漏洞。

## 关闭独立服务

为了提供 Web、邮件和 FTP 等服务，你的 Linux 系统必须运行监听入站 TCP/IP 网络请求的服务器程序。其中某些服务器在系统启动时就会启动，并且会一直运行。这些服务器被称为独立服务器（stand-alone servers）。Web 服务器和邮件服务器就是独立服务器的示例。

另一个服务器 `xinetd` 会启动其他配置为在 `xinetd` 下运行的服务器。某些服务器可以配置为独立运行，也可以在像 `xinetd` 这样的超级服务器运行。例如，`vsftpd` FTP 服务器可以配置为独立运行，也可以在 `xinetd` 的控制下运行。

![](img/6a2cbfe493abd0ba9453aa49df7301b4_322_1.png)

你可以使用 `chkconfig` 命令开启或关闭服务器。例如，要关闭 FTP 服务，使用 `chkconfig vsftpd off`。

## 配置 Internet 超级服务器

除了 Web 服务器或邮件服务器等独立服务器外，另一个服务器——`xinetd` 需要你单独配置。`xinetd` 服务器被称为 Internet 超级服务器（superserver），因为它根据需要启动其他服务器。

`xinetd` 服务器在启动时会读取配置文件 `/etc/xinetd.conf`。该文件反过来引用存储在 `/etc/xinetd.d` 目录中的配置文件。`/etc/xinetd.d` 中的配置文件告诉 `xinetd` 应该监听哪些端口，以及为每个端口启动哪种服务器。输入 `ls /etc/xinetd.d` 查看你系统上 `/etc/xinetd.d` 目录下的文件列表。每个文件代表一个 `xinetd` 可以启动的服务。要关闭这些任何服务，请使用 `chkconfig filename off`，其中 `filename` 是 `/etc/xinetd.d` 目录下的配置文件名。在你开启或关闭任何服务后，必须重启 `xinetd` 服务器；要重启 `xinetd` 服务器，使用 `/etc/init.d/xinetd restart`。该命令会停止 `xinetd` 服务器然后重新启动它。当它重启时，会读取配置文件，更改随之生效。

## 配置 TCP wrapper 安全

系统的一个安全特性是使用 TCP wrapper。TCP wrapper 是一个为服务提供访问控制的包。TCP wrapper 是一段过滤网络访问的代码块。如果两个文件为空，TCP wrapper 将拒绝所有访问。以下是加强安全性的步骤：

- 1. 使用文本编辑器编辑 `/etc/deny` 文件，添加以下行：`ALL:ALL`
- 2. 如果你想允许来自特定主机访问，编辑 `/etc/allow` 文件并添加以下内容：`ALL:hosts`
- 3. 如果你想允许访问特定服务，可以在 `/etc/allow` 中使用以下语法：`服务名:主机`（IP 地址或域名）

## 使用 Secure Shell (SSH) 进行远程登录

SUSE Linux 自带 OpenSSH 软件，它使用公钥加密验证用户并加密主机之间的通信。SSH 使用公钥加密，发送方和接收方都有一对密钥——公钥和私钥。公钥分发的，双方都知道对方的公钥。发送方使用接收方的公钥加密数据。只有接收方的私钥才能解密数据。

要使用 OpenSSH，你首先需要启动 ssh 服务器并生成主机密钥。如下：

- 如果你想在主机上支持 SSH 远程登录，请在系统上启动 ssh。执行 `ps ax grep ssh` 检查服务器是否已运行。如果没有，在终端窗口输入 `su -` 成为 root，并开启 SSH 服务。
```bash
/etc/init.d/start service 立即启动。要确保下次重启系统时服务器正常工作，输入 `chkconfig sshd`。
```

- 使用以下命令生成主机密钥：
```bash
ssh-keygen d /etc/ssh/ssh_host_key
```
`d` 参数导致 sshkeygen 程序生成 DSA 密钥，SSH 协议使用这种密钥。如果你看到消息说文件 `/etc/ssh/ssh_host_key` 已存在，这意味着密钥在 SUSE Linux 安装期间已经生成。在这种情况下，按 `n` 避免覆盖密钥并继续使用现有文件。

用户可以使用 `ssh` 命令从远程系统登录（假设远程系统也运行 Linux）。在 Windows 系统上，用户可以运行支持 SSH 的程序，如 putty。

# 304 第四部分：成为 SUSE 专家

例如，为了从网络上的另一台 Linux 系统登录到我在 SUSE Linux 系统上的账户，我输入：

```
ssh 192.168.0.6 -i naba
```
