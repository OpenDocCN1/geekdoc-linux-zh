
在继续之前，简单要说明一点：没有什么可以阻止你在除标准已知端口以外的任何端口上运行服务器程序。然而，这些是客户端软件将使用的默认端口。所以例如，如果我们在网络浏览器中输入此 URL：

`www.mysupplier.com`

# TELNET 与端口配置

... 浏览器将使用 DNS 查找名为 `www.mysupplier` 的机器的 IP 地址，并尝试通过 `80` 端口与其建立连接，因为它知道那是 Web 服务器的常用端口。如果 Web 服务器运行在不同的端口上，你可以通过不同的方式访问它。例如，在同一台服务器上通过不同端口（如 `8080`）运行测试版本是常见的的，在这种情况下，用户必须在 URL 中指定端口：

```
www.mysupplier.com:8080
```

# 注册端口

端口 `1,024` 到 `49,151` 被称为注册端口。这些端口已在中央机构注册，正式分配给特定厂商的特定应用程序。例如，IBM 的 Notes 邮件服务器使用 `1,352` 端口，而 Windows Live Messenger 在微软停止支持它之前使用的是 `1,503` 端口。使用这些端口并不需要超用户权限。

> 小贴士
>
> 并没有人真正关乎 `49,151` 的分界线——我们真正关乎的是它是特权端口（`1,024` 以下）还是非特权端口（`1,024` 及以上）。

# 剩余部分

`49,151` 以上的端口供任何人根据需要使用。

![](img/c00dda504be4d70c6e7dd488ae0af42a_208_0.png)

# 获取应用程序

当然，你的 Linux 机器在没有运行 Web 服务器程序的情况下，不可能神奇地变成（比如）一台 Web 服务器。将浏览器指向一台新安装的 Linux 机器，它将无法连接。

你需要做两件事来实现它：获取一个 Web 服务器程序，并确保任何内置防火墙软件已配置为允许连接。

下方：Web 服务器连接被拒绝。

![](img/c00dda504be4d70c6e7dd488ae0af42a_209_0.png)

![](img/c00dda504be4d70c6e7dd488ae0af42a_209_1.png)

最流行的 Web 服务器程序是 Apache，通过 `dnf install HTTPD` 可以很容易地为我们的 Fedora 服务器获取。顺便注意，`HTTPD` 代表超文本传输协议守护进程；在 Unix/Linux 术语中，守护进程基本上是一个持续在后台运行并响应请求的程序。

一旦获取了它，我们需要启动它。我们将使用 `systemctl` 来执行。

```
[root@dc-linux ~]# systemctl start httpd
```

现在，如果我们再次从客户端机器尝试连接到 Web 服务器，会有好运吗……或者呢？下方：一条错误消息表明我们仍然无法连接。

![](img/c00dda504be4d70c6e7dd488ae0af42a_210_0.png)

等一下。怎么了？我们已经启动了 Web 服务器，可以使用 `ps` 命令检查它是否正在运行：

```
[root@dc-linux ~]# ps ax | grep httpd
6050 Ss 0:00 /usr/sbin/httpd -DFGROUND
6109 S 0:00 /usr/sbin/httpd -DFGROUND
6111 S 0:00 /usr/sbin/httpd -DFGROUND
6112 S 0:00 /usr/sbin/httpd -DFGROUND
6113 S 0:00 /usr/sbin/httpd -DFGROUND
6114 S 0:00 /usr/sbin/httpd -DFGROUND
```

# IPTABLES

我们已经提到过 Linux 是相当安全的，这也是 `IPTables` 成为默认安装部分的原因之一。防火墙是一种软件，充当入站和出站连接的屏障，并确保无论系统上运行哪些程序，只有系统允许的连接才被允许发生。开箱即用的方法是让系统允许一组最小的连接。让我们运行一个 `IPTables` 命令：

```
iptables -I INPUT 1 -p tcp -m state NEW --dport 80 -j ACCEPT
```

此命令基本上是告诉 `IPTables` 添加一条“输入”规则（即：对于目标为此机器、使用 TCP 协议、目标端口为 `80`（Web 服务器端口）的新连接，应该接受这些连接）。再次尝试使用我们的浏览器（见右侧）。这样才一样了——机器已经响应了我们的请求并向我们发送了测试。所以我们要让机器保存设置。`IPTables` 在我们告诉它之前是不会保存的，因此重启会导致规则丢失，所以：

```
root@dc-linux ~# iptables-save > /etc/sysconfig/iptables
```

`IPTables` 并不是给胆小的人准备的。幸运的是，如果你对网络工作原理并不感到困惑，那么在网上有足够的信息可以帮助你完成大部分工作，我们通过试错来证明它是可行的。下方：Web 服务器现在正常工作。

![](img/c00dda504be4d70c6e7dd488ae0af42a_212_0.png)

![](img/c00dda504be4d70c6e7dd488ae0af42a_212_1.png)

# Linux 作为服务器

# 配置 NAS（网络附加存储）服务器

Linux 作为服务器非常受欢迎——即托管某种服务如文件存储、打印机协调、数据库、邮件传输系统或 Web 服务器的机器。

对于面向互联网的服务器（例如企业 Web 服务器），数量是巨大的：根据 2015 年 Netcraft Web 服务器调查（`http://news.netcraft.com/archives/2015/07/22/July-2015-web-server-survey.html`），全球有超过 `3.25` 亿运行 Apache Web 服务器的服务器，可以肯定，其中绝大多数基于 Linux。数据非常惊人。

# 共享文件

Linux 服务器并不一定要面向公众。例如，人们通常想在家里有一个系统可以存储文件，这样既可以保留备份，更常见的是家庭成员之间共享。那些在互联网上托管自己网站的人通常会在家里有一台机器进行开发，这样他们可以在上传代码到互联网之前确保一切万无一失。我们将查看一些常见的操作。

# 网络文件系统

首先，我们将查看如何使用 Linux 机器运行文件服务器。现在我们可以使用名为 `NFS`（网络文件系统）的东西，因为这是 Unix 风格系统（如 Linux）的原生文件共享协议。问题是，并没有许多机器支持 `NFS`——我们都是 Windows 或 Mac 用户。由于连接到我们服务器的大多数机器是 Windows PC，我们将采用 Windows 标准，它也被统称为 `SMB`（服务器消息块）或 `CIFS`（通用互联网文件系统）——通过这样做我们不会疏远 Mac 或 Linux 客户端，因为它们都可以访问 `SMB` 文件共享。

# 运行 SAMBA

在 Linux 上，`SMB` 是使用 Samba 软件包实现的，它源于 `1992` 年，并且从一开始就大获成功。这是我们测试机器上 Fedora 安装的标准部分，尽管我们之前已经展示了一些使用命令行指令的示例，但我们将通过图形化配置界面来展示其中的一些内容。嗯，它比输入命令要友好得多，为什么不试试呢？

# 在开始之前

为了运行配置过程，我们必须能够运行管理员级别的功能。有两种方法可以实现：

- 在开始配置过程之前，在 Linux 机器上以 '`root`' 用户身份登录。
- 以你创建的 '`Administrator`' 管理员用户身份登录。

对于这个示例，我们以 '`root`' 身份登录了。

![](img/c00dda504be4d70c6e7dd488ae0af42a_217_0.png)

![](img/c00dda504be4d70c6e7dd488ae0af42a_218_0.png)

# 我们的共享设置

我们将采用的是非常基本的设置：我们将创建用户 '`max`'，他将拥有一个属于他自己的私有目录。一旦你让基础 Samba 设置运行起来，战斗就赢了 `95%` 百比——如果你接着想开始玩转共享目录之类的内容，你不会发现它非常困难。

# 创建用户

一种不那么笨拙的创建用户的方法是直接使用 `user add` 命令通过几条命令完成上述所有操作。首先是创建用户：

```
[root@fileserver-local ~]# useradd -c 'Max Cooter' max
```

现在我们设置密码：

```
[root@fileserver-local ~]# passwd max
Changing password for user max.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

# 设置 SAMBA
