
20. 你可以选择性点击“Copy OTP to Clipboard”。然后你就可以使用鼠标将一次性密码粘贴到防火墙服务器上的 `S/Key` 提示处。否则，你必须手动复制。无论你使用哪种方法，当你在输入一次性密码后按下 `Enter` 键时即可获得防火墙服务器的访问权限。

使用 `S/Key` 计算器会让整个系统的使用变得更加合理。如果没有它，你的用户很容易感到沮丧并放弃该系统。这个工具应该防止这种情况的发生，并提供一个卓越的安全工具。

### 总结

在本章中，我描述了如何配置一个“真实的”`Linux` 客户端-服务器网络。示例系统由八台 `Microsoft` `Windows` 95 客户端、一个基于 `Linux` 的文件和打印服务器以及一个基于 `Linux` 的防火墙组成。

本章涵盖了以下主题：

- 添加若干 `Windows` 95 客户端以创建一个“真实”的示例网络。这些客户端代表了一个中小型办公室的示例。

- 配置 `Linux/Samba` 文件和打印服务器。第 1 章中介绍的服务器被扩展以包含额外的 `Windows` 95 客户端。该过程简单，只需将用户添加到 `Linux` 密码文件和组文件中。新用户与 `Windows` 95 客户端名称匹配。`Red Hat` 将 `Samba` 配置为用户安全验证方法，因此你必须使 `Linux` 文件-打印服务器上的用户名与 `Windows` 客户端的名称匹配。这比共享安全方法要好，因为后者学习起来非常困惑。

- 将 `Samba` 用户细分为 `Linux` 组，以提供工作分工和额外的安全性。创建 `Linux` 组以匹配在网络上执行的工作类型。接下来，创建 `Samba` 共享以匹配 `Linux` 组。然后，两个或多个客户端计算机就可以访问这些组的共同工作。人们就可以轻松地合作了。

- 配置独立的防火墙网络以连接文件-打印服务器和防火墙服务器。这会将私有网络与互联网隔离。

- 配置 `Linux` `IP` 过滤防火墙服务器。防火墙服务器在私有网络和互联网之间传输 `IP` 包。因此，任何试图入侵你的私有网络的人必须首先突破防火墙服务器。为了让你的网络难以被破解，你可以从防火墙服务器上移除除核心软件以外的所有程序。

# 第十一章

## 为你的真实网络添加安全措施

本章内容

- 为你的网络添加主动安全措施

- 使用 `SATAN`、`Crack` 和 `Tripwire` 在问题发生前检测安全问题

- 为你的网络添加被动安全措施

- 增加安全性并减少互联网连接负载

- 从防火墙服务器上移除所有不必要的守护进程和应用程序

安全工作永远无法“完成”。随着你作为系统管理员/安全监控的成长，你可以根据需要添加内容。在本章中，我将引导你如何在第 10 章设置的“真实”网络中添加主动和被动安全措施。

## 为你的私有网络和防火墙网络添加主动安全措施

第 9 章介绍的 `Tripwire` 和 `SATAN` 系统是构建网络安全性的两个有用程序。记住，`Tripwire` 使用 `MD5`（消息摘要算法）对重要的系统文件（实际上是任何你想要检查的文件）计算校验和值。这些校验和值可以定期与当前文件进行比较，以查看是否有任何文件被修改以隐藏特木马。`SATAN` 使用 Web 浏览器以图形化方式配置并显示它执行的安全检查结果。在接下来的章节中，我将向你展示如何安装并启动这两个系统。

除了介绍 `Tripwire` 和 `SATAN` 之外，我在这里还引入了 `Crack` 系统。它会将你的现有密码与字典中可以找到单词进行对比。通过使用 `Crack`，你可以主动保护你的系统免受简单或易于猜测的密码的影响。

现在是时候指出，我是在文件服务器/路由器上安装这些系统的了。我这样做是因为 `SATAN` 会消耗大量资源，而我使用了一台旧 `PC` 作为防火墙服务器。我还要求你从防火墙服务器上移除所有编译器和开发库，而 `SATAN` 需要编译。如果你愿意，也可以选择在另一台 `Linux` 机器上安装 `SATAN` 和 `Tripwire`，但在我的示例中，我只有一台机器。

# 安装和配置 Tripwire

`Tripwire` 以 `RPM` 包的形式提供本书的 CD-ROM 中。通常情况下，安装二进制文件（特别是用于安全本身的代码）而不是编译源代码不被认为是良好的安全实践。这种担心在于，二进制文件比源代码更容易隐藏病毒和后门（只有可执行代码设计者才知道的固定密码或其他入口）。然而，请认为 `Red Hat` 是一个可靠的来源，并信任他们采取了所有合理的预防措施。因此，我已将其安装在我的系统上，但留由你决定是否要获取源代码。我在文件服务器/路由器上使用 `Tripwire`。在我的网络中，这是最重要的，因此我想让它尽可能安全。只要有访问权限，就可以在其他计算机上配置（例如防火墙服务器）。以下指令详细介绍了安装过程：

1. 以 `root` 身份登录到你的 `Linux` 服务器。

2. 如果尚未挂载 CD-ROM，请输入以下命令进行挂载：

3. 输入以下命令安装 `Tripwire`：

```
mount /mnt/cdrom
rpm -ivh /mnt/cdrom/tripwire-1.2.1386.rpm
```

`Tripwire` 安装在 11-1 所示的目录中。

# 列表 11-1：Tripwire 分发

```
/etc/cron.daily/tripwire.verify
/etc/tw.config
/usr/doc/tripwire-1.2-1
/usr/doc/tripwire-1.2-1/Changelog
/usr/doc/tripwire-1.2-1/FAQ
/usr/doc/tripwire-1.2-1/INTERN
/usr/doc/tripwire-1.2-1/README
/usr/doc/tripwire-1.2-1/TODO
/usr/doc/tripwire-1.2-1/WHATSNEW
/usr/doc/tripwire-1.2-1/docs
/usr/doc/tripwire-1.2-1/docs/README
/usr/doc/tripwire-1.2-1/docs/appdev.txt
/usr/doc/tripwire-1.2-1/docs/desigdoc.ps
/usr/doc/tripwire-1.2-1/docs/sans.txt
/usr/man/5/tw.config
/usr/man/8/siggen.8
/usr/man/8/tripwire.8
/usr/sbin/siggen
/usr/sbin/tripwire
/var/spool/tripwire
```

# 第十一章：为你的真实网络添加安全措施

```
/usr/doc/tripwire-1.2-1/README
/usr/doc/tripwire-1.2-1/README.FIRST
/usr/doc/tripwire-1.2-1/Readme
/usr/doc/tripwire-1.2-1
```

4. 查看列表 11-2 所示的 `Tripwire` 配置 `/etc/tw.config`。

# 列表 11-2：Tripwire 配置 /etc/tw.config

```
# $ Id: tw.config.v 1.4 1993/11/22 06:38:06 genek Exp$
#
# tw.config

# 此文件包含 System Preener 将扫描的文件和目录列表。从这些文件中收集的信息
# 将被存储在 tripwire.database 文件中。
#
# 格式: [!=] entry [ignore-flags]
#
# 其中：'!' 表示该条目从待扫描文件列表中被剪裁（包含）。
#
# 其中 '=' 表示该条目将被添加，但如果它是目录，则其所有内容都将被剪裁（适用于 /tmp）。
#
# 其中：entry 是文件或目录的绝对路径。
#
# 其中：ignore-flags 的格式如下：
[template][+][[pinugsam12] ... ]
#
# : 忽略以下属性
# + : 不忽略以下属性
```

# 权限和文件模式位 a：访问时间

# p：权限 m：修改时间

# i：inode 节点

# n：链接数（引用计数） c：inode 节点创建时间

# u：所有者用户 ID 1：签名 1

# g：所有者组 ID 2：签名 2

# s：文件大小

# 我们需要的模式：

# 日志文件

```
@@@define LOGFILE E+pugn
```

# 配置文件

```
@@@define CONFM E+pinuc
```

# 二进制文件

```
@@@define BINM E+pugscil12
```

# 目录

```
@@@define DIRM E+pnug
```

# 数据文件（当前与 BIN_M 相同）

```
@@@define DATAM E+pugscil12
```

# 设备文件

```
@@@define DEVM E+pnugsci
```

#

# 例：以下项目将扫描 /etc 中的所有文件，并报告

# 位、inode 号、引用计数、uid、

# gid、修改和创建时间以及签名的更改。

# 然而，它将忽略访问时间的任何更改。

#

```
# /etc +pinugsm12-a
```

#

# 预定义了以下模板，使得这些冗长的忽略

# 描述不再必要。

# 模板：（默认） R：[R]只读 (+pinugsm12-a)

# L：[L]日志文件 (+pinug-sam12)
