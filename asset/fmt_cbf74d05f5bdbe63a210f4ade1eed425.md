
```
mail from: joseph@cheek.com
250 joseph@cheek.com... Sender ok
rcpt to: joseph
250 joseph... Recipient ok
data
354 Enter mail, end with "." on a line itself
this is an e-mail test.
250 OK 3182 Message accepted for delivery
quit
221 sanfrancisco.cheek.com closing connection
Connection closed by foreign host.
```

你刚刚发送了一个正文为“this is an e-mail test.”的邮件给用户 `joseph`。`quit` 命令告诉 `sendmail` 你已完成操作并想要关闭连接。

## 排除 procmail 故障

尽管 `procmail` 提供的调试信息远没有 `sendmail` 那么多，但仍然有测试方法。设置一个规则将所有消息复制到特定位置是简单的。你可以从命令行手动运行 `procmail`，并通过键盘或通过文件管道（带有头信息）提供邮件消息。

当 `procmail` 错误路由消息时（可能是由于配方文件问题），追踪非常困难。很多时候，邮件会丢失；在这些情况下，人们很容易怀疑邮件是否生成过。在这种情况下，在 `procmailrc` 文件开头生成一个规则将所有消息保存到文件中是明智的。在你的 `procmailrc` 文件开头添加这三行：

```
:0:c
*
all-mail-goes-here
```

这会将所有邮件保存到 `all-mail-goes-here` 文件夹（如果 `procmail` 可以写入该目录），并继续处理消息的副本。所有邮件都会匹配此空规则，因为在第二行的星号后面没有条件。通过检查 `all-mail-goes-here` 文件，你可以看到 `procmail` 视角下的消息。如果该文件不存在，你可能遇到了文件系统问题。

以下文件虽然没有被 `WU-FTPD` 使用，但它们与 FTP 服务器相关：

| 文件 | 用途 |
| --- | --- |
| `/etc/services` | 纯 ASCII 文件，列出了互联网服务到其端口号的映射 |
| `/etc/aliases` | 用于虚拟托管的纯 ASCII 文件 |
| `/etc/passwd` | 用于验证身份的纯 ASCII 文件 |
| `/etc/shells` | 用于验证有效 shell 的纯 ASCII 文件 |
| `/etc/hosts.allow` | 允许指定主机名访问的纯 ASCII 文件 |
| `/etc/hosts.deny` | 拒绝指定主机名访问的纯 ASCII 文件 |

## WU-FTPD 概述

`WU-FTPD` 是在华盛顿大学（Washington University）开发的，它是旧版本 UNIX 自带的 `FTPD` 的替代品。`WU-FTPD` 具有许多额外功能。实际上，几乎所有的 Linux 发行版都使用 `WU-FTPD`，但也有其他类似的软件包供选择。你的 OpenLinux 安装将对 `WU-FTPD` 守护进程、FTP 客户端以及所有必要的配置文件进行标准安装。

> 在希腊神话中，daemon（守护灵）是神与人之间的侍从或守护灵。在 UNIX/Linux 中，daemon 指在后台持续运行、直到被调用的无值守程序。

![](img/9102b40bb114da6b158a518630807d57_164_0.png)

`WU-FTPD` 的一些额外功能包括：

- 所有传输和执行命令的日志记录
- 即时压缩和归档
- 分类限制
- 按目录上传权限
- 受限制的访客账户
- 系统级和目录消息
- 目录别名和虚拟主机支持
- Cdpath 和文件名过滤器

访问网站 `www.wu-ftpd.org` 获取最新更新。

![](img/9102b40bb114da6b158a518630807d57_164_1.png)

## FTP 客户端

有许多 FTP 客户端可以选择，包括名为 `ftp` 的 FTP 客户端。你的 OpenLinux 中可用的其他 FTP 客户端还有 `neftp` 和 `pfpt`。此外，对于喜欢点点点击的用户，还有许多为 X Window 系统编写的 FTP 客户端。`Netscape Communicator`、`gFTP` 和 `IglooFTP` 是 X Window 系统上一些常用的 FTP 客户端。访问 `www.linuxberg.com` 或 `www.freshmeat.net` 获取最新的替代 FTP 客户端。

要查看你安装的是哪个版本，只需在 Linux 命令行中输入 `ftp localhost`；FTP 客户端将显示版本号。

![](img/9102b40bb114da6b158a518630807d57_165_0.png)

## FTP 账户类型

访问 FTP 服务器有三种类型的用户账户：访客（guest）、真实（real）和匿名（anonymous）。访客账户基本上就是你的 OpenLinux 账户；你可以直接在该 FTP 服务器上使用你的用户账户（Linux 登录账户和密码），但在登录后，你只能访问你的家目录。真实账户与访客账户的区别在于，使用此账户你可以访问整个文件系统。

最后，如果你在那个 FTP 服务器上没有账户，则使用匿名账户。事实上，匿名账户实际上是你名为 `"ftp"` 的 OpenLinux 账户（你可以通过检查 `/etc/passwd` 文件，或在访问 FTP 服务器时使用用户名 `ftp` 来确认）。该账户没有密码，因此你可以使用任何密码。通常，你的电子邮件地址被用作匿名 FTP 的密码；使用匿名账户后，你会被放入 `/home/ftp` 目录，该目录成为你的根目录。这与访客账户类似，不同的是任何人都可以这个没有密码保护的匿名 FTP 账户。

以下是 FTP 账户类型的总结：

| 账户类型 | 描述 |
| --- | --- |
| 匿名 | 账户名为 `anonymous` 或 `ftp`。密码可以是任何内容，因为没有密码验证。此账户的用户可以访问公共 FTP 目录和文件。大多数 FTP 站点提供此账户以促进文件共享。 |
| 访客 | FTP 账户名为该服务器上的用户名；密码与用户账户密码相同。用户名和密码指定在 `/etc/passwd` 中（因此可以使用它们登录 Linux 服务器）。默认情况下，OpenLinux 服务器上的账户持有者都有 FTP 账户，因为它们取决于 `/etc/passwd`。 |
| 真实 | 与访客账户类似，但用户拥有导航整个文件系统。此类账户应谨慎授予，因为它们存在安全风险。 |

## set FTP 会话

现在让我们仔细观察这三种不同的 FTP 账户，看看它们是如何访问 FTP 服务器的。

### 真实或访客 FTP 会话

以下是在 FTP 服务器上使用真实或账户的示例会话。

```
[tho@mydomain.com]$ ftp yourdomain.com
Connected to yourdomain.com
220 yourdomain.com FTP server (Version wu-2.5.0(1)) Sat Apr 3 15:11:49 MST 1999) ready.
Name (yourdomain.com:tho): tho
331 Password required for tho.
230 logged in.
Remote system is UNIX.
Using binary mode.
ftp>
```

### 匿名会话

以下使用匿名账户的示例会话。

```
[tho@mydomain.com]$ ftp yourdomain.com
Connected to yourdomain.com
220 yourdomain.com FTP server (Version wu-2.5.0(1)) Sat Apr 3 15:11:49 MST 1999) ready.
Name (yourdomain.com:tho): anonymous
331 Password required for tho.
230 logged in.
Remote system is UNIX.
Using binary mode.
ftp>
```

在此会话中，用户名是匿名，你可以输入任何字符字符串。匿名账户是 `"ftp"`，你会被放入 `/home/ftp` 目录。

安装后，将创建以下文件：

- `/etc/ftpaccess`
- `/etc/ftpconversions`
- `/etc/ftpgroups`
- `/etc/ftphosts`
- `/etc/ftpusers`
- `/etc/logrotate.d/ftpd`
- `/etc/pam.d/ftp`
- `/usr/bin/ftpcount`
- `/usr/bin/ftpshut`
- `/usr/bin/ftpwho`
- `/usr/doc/wu-ftpd-2.5.0`
- `/usr/doc/wu-ftpd-2.5.0/ANNOUNCE-RELEASE`
- `/usr/doc/wu-ftpd-2.5.0/README`
