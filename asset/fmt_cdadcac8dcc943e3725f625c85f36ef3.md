
```
$ sftp.handshistory.com
Connecting to ftp.handshistory.com
jake@ftp.handshistory.com's password: ********
sftp
```

此时，你可以开始交互式 FTP 会话。你可以像使用任何 FTP 客户端一样对文件使用并放置命令，但可以知道你正在一个安全连接上工作。

> TIP: `sftp` 命令配合 `ssh` 和 `scp` 要求服务器上运行 SSH 服务。如果你无法使用 `sftp` 连接到 FTP 服务器，则 SSH 服务可能不可用。

# 无需密码使用 ssh, scp 和 sftp

对于你经常使用的机器，将其配置为登录时无需使用密码，通常非常有帮助。下面的步骤显示了如何操作。

这些步骤将引导你完成从一台机器到另一台机器的无密码认证。在本示例中，本地用户名为 `chester`，位于名为 `host1` 的计算机。远程用户也是名为 `host2` 的计算机上的 `chester`。

- 1. 登录本地计算机（在本示例中，我以 `chester` 身份登录 `host1`）。

> NOTE：仅在本地工作站上作为本地用户运行步骤 2。除非你丢失了 ssh 密钥，否则不要再次运行。配置远程服务器时，请跳到步骤 4。

- 2. 指定生成 ssh 密钥的类型：

```
$ ssh-keygen -t dsa
```

Generating public/dsa key pair.

Enter enter file in which to save the key

(/home/chester/.ssh/id_dsa): <Enter>

Enter passphrase (empty for no passphrase): <Enter>

Your identification has been saved in /home/chester/.ssh/id_dsa.

Your public key has been saved in /home/chester/.ssh/id_dsa.pub.

The key fingerprint is:

3b:0c2f:63:a5:70:b4:f0:2a:c14:24:47:69 chester@host1

- 3. 按回车接受默认密钥文件位置。然后再次按回车（两次）以分配空密码。（如果你输入了密码，系统将提示输入该密码，且没有它将无法登录。）

- 4. 你必须通过关闭家目录、`.ssh` 目录和认证文件的权限来确保你的认证密钥的安全：

```
$ chmod go-w $HOME
$ chmod 700 $HOME/.ssh
$ chmod go-rwx $HOME/.ssh/*
```

- 5. 输入以下将密钥复制到远程服务器（将 `chester` 替换为远程用户名，将 `host2` 替换为远程主机名）：

```
$ cd ~/.ssh
$ scp id_dsa.pub chester@host2:/tmp
chester@host2's password: ***
```

- 6. 输入以下内容将 ssh 密钥添加到远程用户的授权密钥中（代码应单行，不要换行）：

```
$ ssh chester@host2 'cat /tmp/id_dsa.pub >> /home/chester/.ssh/authorized_keys'
```

> NOTE：之前的两个步骤都需要密码。这是正常的。

- 7. 为了让 sshd 守护进程接受你创建的 `authorized_keys` 文件，你的 `authorized_keys` 文件必须具有正确的权限。为了确保这一点，输入以下内容：

```
$ chmod 600 ~/.ssh/authorized_keys
```

- 8. 如果你需要移除密钥，可以使用文本编辑器从 `authorized_keys` 文件中删除该行：

```
$ vi ~/.ssh/authorized_keys
```

# 610 第三部分：管理 Fedora 和 RHEL

……让他获得系统的特权访问。通常，这是通过一个称为利用程序（exploit）的程序来实现。

虽然 DOS 攻击具有破坏性，但侵入型攻击的危害性最大。原因有多种，但结果总是是一样的：一个不速之客现在正安家住在你的机器上，并以一种你无法控制的方式使用它。

## 防御拒绝服务攻击

如前所述，拒绝服务攻击试图使你的计算机崩溃，或者至少将其性能降低到无法使用的程度。有多种拒绝服务利用程序。大多数程序试图过载系统资源，例如你的可用磁盘空间或互联网连接。后续章节将讨论一些常见的攻击和防御措施。

邮件炸弹（Mailbombing）是指向特定用户或系统发送大量电子邮件，导致计算机硬盘满。有几种方法可以保护自己免受邮件炸弹。你可以使用 Procmail 邮件过滤工具或配置你的 sendmail 守护进程。

> 交叉引用：参见第 19 章获取关于 sendmail 更完整的描述。

## 使用 Procmail 阻塞邮件

Procmail 邮件过滤工具在 Fedora 和 RHEL 中默认安装，并与 sendmail 邮件守护进程紧密集成；因此，它可以用于选择性地阻塞或过滤特定类型的电子邮件。你可以在 Procmail 网站 www.procmail.org 学习关于 Procmail 的信息。

要为你的用户账户启用 Procmail，请在主目录下创建一个 `.procmail` 文件。该文件的模式应为 0600（你可读，其他人不可读）。输入以下内容，将 `evilmailer` 替换为向你发送邮件炸弹的实际地址：

```
# 删除来自 evilmailer 的邮件
:0
* ^.evilmailer
/dev/null
```

Procmail 脚本会查找每封邮件开头的 From 行，查看其是否包含字符串 `evilmailer`。如果包含，该消息将被发送到 `/dev/null`（实际上等于将其丢弃）。

## 使用 sendmail 阻塞邮件

当只有一个用户遭受邮件炸弹攻击时，Procmail 邮件工具效果很好。然而，如果邮件炸弹影响了许多用户，你应该正确配置你的 sendmail 守护进程，以阻塞来自邮件炸弹的所有邮件。通过向 `/etc/mail` 目录下的访问文件（access file）中添加邮件炸弹的电子邮件地址或系统名称来实现此。

访问文件的每行包含一个电子邮件地址、主机名、域名或 IP 地址，后面跟着一个制表符和一个关键字，指定当该实体向你发送消息时要执行的操作。有效的关键字有 `OK`、`RELAY`、`REJECT`、`DISCARD` 和 `ERROR`。使用 `REJECT` 关键字将导致发送者的邮件退回并带有错误消息。`DISCARD` 关键字将导致消息被静默丢弃而不返回错误。你甚至可以使用 `ERROR` 关键字返回自定义的错误消息。

因此，一个示例 `/etc/mail/access` 文件可能如下：

```
# 查看 /usr/share/doc/sendmail/README.cf 可获取此文件格式的描述。
# (在该文件中搜索 access_db)
# /usr/share/doc/sendmail/README.cf 是 sendmail-doc
# 包的一部分。

# 默认情况下，我们允许来自 localhost 的转发...
localhost.localdomain RELAY
localhost RELAY
127.0.0.1 RELAY

# 我们想要阻止的发送者
evilmailer@yahoo.com REJECT
stimpy.glaci.com REJECT
cyberpromo.com DISCARD
199.170.176.99 ERROR:550 Die Spammer Scum!
199.170.177 ERROR:550 Email Refused
```

与 Linux 配置文件一样，以井号（`#`）开头的行是注释。我们的屏蔽垃圾邮件发送者列表位于示例文件的末尾。注意，要阻塞的地址可以是完整的电子邮件地址、完整的主机名、域名、IP 地址或子网。

要阻塞来自邮件炸弹的特定电子邮件地址或主机，请以 root 身份登录系统，编辑 `/etc/mail/access` 文件，并添加一行来 `DISCARD` 来自违规发送者的邮件。

在保存文件并退出编辑器后，你必须将访问文件转换为名为 `access.db` 的哈希索引数据库。该数据库在下次 sendmail 启动时会自动更新。或者你也可以如下所示立即转换数据库：

```
# cd /etc/mail
# make
```

sendmail 现在应该丢弃来自你列出的地址的邮件。

## 垃圾邮件转发

你的邮件服务被滥用的另一种方式是让你的系统被用作垃圾邮件中继（spam relay）。*Spam*（垃圾邮件）是指互联网上常见的现象，即未经请求的垃圾邮件。垃圾邮件发送者通常从普通的拨号上网账户发送信息。他们需要某种高容量的邮件服务器来接收和缓冲消息负载。他们一次性将大批量的垃圾邮件发送到服务器，然后注销，让服务器完成将消息传递给许多受害者的工作。
