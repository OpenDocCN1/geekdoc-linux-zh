
“身份验证”部分允许你为用户密码设置两种安全形式：阴影密码（Shadow Passwords），它将用户密码加密存储在`/etc/shadow`文件中，以及这些密码的加密哈希值。本节还允许你为各种协议设置身份验证信息：

- NIS 网络信息服务，用于连接到包含 Unix 和 Linux 计算机的网络上的登录身份验证数据库。
- LDAP 在此上下文中，轻量级目录访问协议（Lightweight Directory Access Protocol）是一种替代的登录身份验证数据库。
- Kerberos 5 MIT 开发的强加密系统，用于在网络中验证用户。
- Hesiod 与 Kerberos 5 相关联。
- SMB Samba (CIFS) 连接到 Microsoft Windows 风格网络以进行登录身份验证。

## 名称切换缓存

与 NIS 关联，用于查找密码和组。

## 防火墙配置

防火墙配置部分允许您为目标计算机配置默认防火墙。在大多数系统上，您希望将受信任服务的数量保持在最低限度。然而，在像 Red Hat 考试这样的情况下，您可能被要求在一台系统上设置大量服务，这将需要在防火墙上配置大量受信任服务。

在本节中，您还可以配置基本的 SELinux 设置。Active 和 Disabled 选项很直接；Warn 选项对应于 SELinux 的 Permissive 实现。更多信息请参见第 4 章。

## 显示配置

显示配置部分支持安装基本的 Linux GUI。实际安装取决于下一节中选择的那些软件包和软件包组。虽然关于 GUI 或基于文本的系统管理工具的优越性存在很多争论，但基于文本的工具更稳定。出于这个原因（以及更多原因），许多 Linux 管理员甚至不安装 GUI。然而，如果您在一系列工作站上安装 Linux，如使用一系列 Kickstart 文件所做的那样，那么大多数用户可能都不是管理员。

此外，您可以禁用或启用 Setup Agent，也称为首次启动过程。对于完全自动化的安装，应禁用 Setup Agent。

## 软件包选择

软件包选择部分允许您选择通过此 Kickstart 文件安装的软件包组。您应该将其识别为安装过程中显示的自定义安装屏幕。

如前所述，如果没有与远程存储库（如 RHN 的更新或前面描述的安装服务器）的当前连接，则相关屏幕为空。

## 安装脚本

您可以向 Kickstart 文件添加预安装和后安装脚本。后安装脚本更常见，它们可以帮助以统一的方式配置 Linux 操作系统的其他部分。例如，如果您想安装一个包含员工福利信息的目录，您可以添加一个后安装脚本，该脚本添加适当的`cp`命令以从网络服务器复制文件。

## 认证目标 2.04

## 使用安全 Shell 进行管理

Red Hat Enterprise Linux 默认安装 Secure Shell (`SSH`) 软件包。关于 SSH 的 RHCSA 要求很简单；您需要知道如何使用它来访问远程系统。因此，在本节中，您将研究如何使用`ssh`命令作为客户端访问远程系统。

如前所述，RHEL 6 标准安装上 SSH 的默认安装已经做好了准备。虽然防火墙默认启用，但标准 RHEL 6 防火墙为 SSH 访问保留端口 22 开放。相关的配置文件存储在`/etc/ssh`目录中。详细的服务器配置是 RHCE 要求的一部分。相关的客户端命令是`scp`和`sftp`，也在本节中介绍。

Secure Shell 守护进程是安全的，因为它加密消息。换句话说，监听网络的用户无法读取 SSH 客户端和服务器之间发送的消息。这在像互联网这样的公共网络上很重要。RHEL 包含 SSH 版本 2，其中包括密钥交换算法，这是相对于 SSH 版本 1 的增强。

## 配置 SSH 客户端

主要的 SSH 客户端配置文件是`/etc/ssh/ssh_config`。单个用户可以在其`~/.ssh/config`文件中拥有自定义 SSH 客户端配置。默认包含四个指令。首先，`Host *`指令将其他指令应用于所有连接。

```
Host *
```

此后是支持使用通用安全服务应用程序编程接口进行客户端/服务器身份验证的指令：

```
GSSAPIAuthentication yes
```

下一个指令支持远程访问 GUI 工具。X11 是 Linux 上使用的 X Window System 服务器的旧引用。

```
ForwardX11Trusted yes
```

下一个指令允许客户端设置多个环境变量。在两个 Red Hat Enterprise Linux 系统之间，细节通常很简单。

```
SendEnv LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
SendEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
SendEnv LC_IDENTIFICATION LC_ALL
```

这为远程系统的命令行访问做好了准备。

## 命令行访问

本节基于使用`ssh`命令的标准访问。要访问远程系统，您需要该远程系统上的用户名和密码。默认情况下，直接基于 ssh 的 root 账户访问是启用的。例如，以下命令访问所注明的 server1 系统上的该账户：

```
$ ssh root@server1.example.com
```

以下命令以相同的方式工作：

```
$ ssh -l root server1.example.com
```

如果没有用户名，`ssh`命令假定您以本地系统的用户名远程登录。例如，如果我从我的用户 michael 账户运行以下命令：

```
$ ssh server1.example.com
```

第一次在系统之间运行该命令时，它会显示类似以下的消息：

```
$ ssh server1.example.com
The authenticity of host 'server1.example.com (192.168.122.50)' can't be established.
RSA key fingerprint is b9:8a:c8:cd:c3:02:87:b3:1c:a9:a7:ed:d8:9c :28:b8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'server1.example.com,192.168.122.50' (RSA) to the list of known hosts.
michael@server1.example.com's password:
```

这种类型的 ssh 命令的一个缺陷是它如何通过网络发送密码。更安全的访问可以使用基于密码短语的 1024 位（及以上）私钥/公钥对来实现。但这种更安全的选项是 RHCE 考试的范围，在第 11 章中讨论。当连接建立时，远程密钥指纹的副本会被附加到用户的`~/.ssh/known_hosts`文件中。RSA 是指来自远程系统的公钥加密密钥的引用；该缩写基于其开发人员的姓氏 Rivest、Shamir 和 Adleman。公钥提供给远程系统；私钥保存在本地系统以匹配授权的远程请求。

一旦通过 ssh 连接，您可以在远程系统上执行任何受您在该远程系统上的用户权限支持的操作。例如，您甚至可以使用`poweroff`命令优雅地关闭远程系统。执行该命令后，您将有几秒钟时间使用`exit`命令退出远程系统。

## 更多 SSH 命令行工具

如果您更喜欢使用类似 FTP 的客户端访问远程系统，`sftp`命令适合您。虽然 `-l` 开关与该命令不兼容，但它仍可用于登录远程系统上任何用户的账户。虽然常规 FTP 通信以明文进行，但使用`sftp`命令的通信可用于以加密格式传输文件。

或者，如果您只想通过加密连接复制文件，`scp`命令可以帮助您。例如，我在第 1 章和第 2 章中配置的测试 VM 上创建了本书的一些屏幕截图。为了将该屏幕截图传输到我的笔记本电脑系统，我使用了类似以下命令，它将 F02-20.tif 文件从本地目录复制到具有所注明主机名的远程系统中的`/home/michael/RHbook/Chapter2`目录。

```
# scp F02-20.tif michael@server1:/home/michael/RHbook/Chapter2/
```

除非已建立基于密码短语的连接（如第 11 章所述），否则命令会提示输入用户 michael 在名为 server1 的系统。一旦密码确认，`scp`命令会以加密格式将 FO2-20.tif 文件复制到名为 server1 的远程系统上的指定目录。

## 图形化安全 Shell 访问

`ssh`命令可用于在网络上传输 GUI 工具。听起来很奇怪，但如果本地系统充当 GUI 服务器，同时你从远程系统调用远程 GUI 客户端应用程序，则可以工作。

默认情况下，SSH 服务器和客户端配置文件均已设置好以支持网络上的 X11 通信。你需要做的就是使用 `-X` 开关连接到远程系统。例如，你可以使用图 2-17 中所示的命令序列来管理远程系统上的用户。
