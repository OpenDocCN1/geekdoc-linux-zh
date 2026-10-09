

这可能足以建立加密连接，但为了实现安全身份验证，你需要购买真正的证书！

请在通用名称（CN）提示符处输入你的邮件传输代理（MTA）的主机名！

正在生成 1024 位 RSA 私钥

```
...++++++
...+++++
writing new private key to '/etc/exim4/exim.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there may be a default value,
If you enter '.', the field will be left blank.
-----
Country Code (2 letters) [US]: 
State or Province Name (full name) []: California
Locality Name (eg, city) []: San Francisco
Organization Name (eg, company; recommended) []: Sobell Associates Inc.
Organizational Unit Name (eg, section) []:
Server name (eg. ssl.domain.tld; required!!!) []: sobell.com
Email Address []: mgs@sobell.com
[*] Done generating self signed certificates for exim!
Refer to the documentation and example configuration files
over at /usr/share/doc/exim4-base/ for an idea on how to enable TLS
support in your mail transfer agent.
```

你可以在证书中填入任何你想要的信息。

## 在 exim4 中启用 SSL

一旦你拥有证书，请在 `/etc/exim4` 目录下创建一个名为 **exim4.conf.localmacros** 的文件（你需要以 **root** 权限操作）。使用以下内容，该文件将指示 **exim4** 使用 SSL 证书：

```bash
$ cat /etc/exim4/exim4.conf.localmacros
MAIN_TLS_ENABLE = 1
```

由于 **exim4** 将用于中继邮件，你需要将发送邮件的系统的名称添加到 `dc_relay_nets` 变量中（第 726 页）。重启 **exim4**（第 716 页）。

## 在邮件客户端中启用 SSL

在邮件客户端中启用 SSL 通常很简单。例如，Evolution 提供了 **编辑->首选项->邮件账户->发送邮件->安全性->使用安全连接** 的组合框，允许你选择想要使用的加密类型：**无加密**、**SSL 加密** 或 **TLS 加密**。点击 **检查支持类型** 按钮（位于此组合框正下方）会查询服务器，并设置 Evolution 使用服务器支持的安全和认证类型。

# 章节摘要

**exim4** 守护进程是一个 MTA（邮件传输代理）。当你发送消息时，**exim4** 与其他软件协作将邮件发送给正确的收件人。你可以设置 **exim4** 将邮件发送到 SMTP 服务器，然后由该服务器中继邮件到目的地；或者你可以让 **exim4** 直接将邮件发送到接收邮件的域的 SMTP 服务器。默认情况下，**exim4** 将传入消息存储在邮件池目录 `/var/mail` 中。

`/etc/exim4/update-exim4.conf.conf` 文件控制 **exim4** 工作的许多方面。编辑此文件后，你必须使用 **exim4** 初始化脚本来重启 **exim4**，以便其重新读取配置文件。系统管理员可以使用 `/etc/aliases` 文件，普通用户可以使用 `~/.forward` 文件将邮件重新路由到一个或多个本地或远程地址、文件，或作为程序的输入。

你可以使用 SpamAssassin 等程序来评估和标记邮件，以判断其成为垃圾邮件的可能性。然后你可以决定如何处理标记的邮件：你可以查看每个潜在的垃圾邮件并决定将其放在哪里，或者你可以让你的 MUA（邮件用户代理）自动将潜在的垃圾邮件放入专门的垃圾邮件箱中。

其他可以帮助处理邮件的程序包括 SquirrelMail（提供 Web 邮件服务）和 Mailman（提供邮件列表支持）。IMAP（互联网消息访问协议）和 POP（邮局协议）允许用户远程检索和操作邮件。Dovecot 系统提供 IMAP 和 POP 服务器。

## 练习题

- 1. 默认情况下，发送给 **system** 的邮件会转到 **root**。你如何也保存一份副本到 `/var/log/systemmail`？

- 2. Max 如何存储他的邮件副本到 `~/mbox` 并发送一份副本到 `max@example.com`？

- 3. 如果你的防火墙只允许 IP 地址为 192.168.1.1 的机器向网络外部发送邮件，你如何指示本地的 **exim4** 副本使用此服务器作为中继？

- 4. 描述在 `/etc/exim4/update-exim4.conf.conf` 中将 `dc_eximconfig_configtype` 变量设置为 `smarthost` 如何影响 **exim4** 的行为。当你将此变量设置为 `internet` 时会发生什么？

- 5. SpamAssassin 安装在你的邮件服务器上，阈值设置为异常低的值 3，导致大量误报。你能给邮件客户端提供什么规则，以便它能识别得分 5 或更高的垃圾邮件？

- 6. 描述当 Max 向远程 Linux 系统上的 Sam 发送邮件时所使用的软件和协议。

## 高级练习题

- 7. 解释配置 **exim4** 使用拆分配置与配置其使用未拆分配置之间的区别。你要修改哪些文件来设置每种类型的配置？名称两个被两种配置都读取的文件。

- 8. 假设脚本将某些信息存储在名为 **RESULT** 的变量中。你可以在脚本中放入哪一行代码，将 **RESULT** 的内容发送到命令行第一个参数指定的电子邮件地址？

- 9. 给出一种阅读邮件的简单方法，而不使用 MUA。

- 10. 描述 **spamassassin**、**spamd** 和 **spamec** 之间的关系。它们各自如何工作？为什么不单独使用 **spamassassin** 实用程序？

# NIS 和 LDAP

- **本章内容**
- * NIS 的工作原理 . . . . . . . . . . . . . . . . 742
- * 运行 NIS 客户端 . . . . . . . . . . . . . . . . . . 744
- * yppasswd: 更改 NIS 密码 . . . . . . . . . . . . . . . . 748
- * 设置 NIS 服务器 . . . . . . . . . . . . . . . . . . 750
- * yppasswd: NIS 密码更新守护进程 . . . . . . . . . . . . . . . . . 757
- * LDAP . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 758
- * 设置 LDAP 服务器 . . . . . . . . . . . . . . . . . . 760
- * 其他用于处理 LDAP 的工具 . . . . . . . . . . . . . . . . . . . . 767

NIS（网络信息服务器）通过将这些文件存储在中央数据库中，并让客户端联系数据库服务器从数据库中检索信息，从而简化了通用管理文件的维护。由 Sun Microsystems 开发的 NIS 是客户端/服务器范式的示例。

就像 DNS 解决了保持多个 /etc/hosts 文件副本最新的问题一样，NIS 也解决了保持与系统无关的配置文件（如 /etc/passwd）最新的问题。如今大多数网络都是*异构*的（第 1151 页）；尽管它们运行不同版本的 UNIX 或 Linux，但它们具有某些共同属性，例如 passwd 文件。

LDAP（轻量级目录访问协议）目录可以保存许多类型的信息，包括姓名和地址、网络服务列表以及认证数据。LDAP 也是客户端/服务器设置的另一种示例，适用于任何相对静态、结构化且需要快速查找的信息。许多类型的客户端被设置为与 LDAP 服务器通信，包括邮件客户端、浏览器和认证服务器。

# NIS 简介

局域网（LAN）管理员的一个主要目标是使网络对用户保持透明。这种透明度的一个方面是，当用户在不同的机器上登录时，向他们提供相似的环境，包括用户名和密码。从管理员的角度来看，支持用户环境的信息不应该被复制，而应该保存在中心位置并按需分发。NIS 简化了这一任务。

与 DNS 一样，用户无需知道 NIS 正在管理系统配置文件。设置和维护 NIS 数据库是系统管理员的任务；个别用户和单用户 Linux 系统的用户很少需要直接操作 NIS。

NIS 过去被称为 **黄页**（Yellow Pages），有些人仍以此名称称呼它。Sun 重命名了该服务，因为另一家公司拥有“黄页”名称的商标。然而，NIS 实用程序和文件的名称仍让人想起旧名称：ypcat 显示，ypmatch 搜索 NIS 文件，而服务器守护进程名为 ypserv。

## NIS 的工作原理

- **无加密** NIS 不加密其在网络上传输的数据——它以明文形式传输数据。

- **NIS 域** NIS 使网络上系统中的公共信息集可用。该网络被称为 NIS 域，其特征是每个系统具有相同的 NIS 域名（不同于 DNS 域名 [第 1146 页]）。从技术上讲，NIS 域是一组 NIS 映射（数据库文件）。

- **主服务器和从服务器** 每个 NIS 域必须恰好有一个主服务器；较大的网络可以有从服务器。每个从服务器都持有来自主服务器的 NIS 数据库副本。对从服务器的需求基于 NIS 域的大小以及系统和网络的可靠性。一个系统在同一时间只能属于一个 NIS 域。

- **nsswitch.conf** 系统是否使用 NIS、DNS、本地文件或这些的组合作为特定信息的来源，以及顺序如何，由 /etc/nsswitch.conf 文件决定（第 475 页）。当需要从 NIS 数据库获取信息时，客户端向 NIS 服务器请求信息。例如，当用户尝试登录时，客户端系统可能会使用来自 NIS 服务器的用户名和密码信息来验证用户。

- 你可以配置 nsswitch.conf，使本地系统的 /etc/passwd 覆盖 NIS 密码信息。当你不将 root 账户导出到 NIS（你也不应该！）时，这种设置允许每个系统拥有唯一的 root 密码（或者如果 root 账户被锁定，则没有 root 密码）。

- **源文件** 在 Ubuntu Linux 下，NIS 提供的信息——如用户名、密码以及本地系统名称和 IP 地址——源自本地的 ASCII 配置文件，例如 /etc/passwd 和 /etc/hosts。这些文件被称为源文件或主文件。（一些管理员通过持有不同的文件来避免混淆

