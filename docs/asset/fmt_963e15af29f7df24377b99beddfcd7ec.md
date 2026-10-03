
其他可能具有`suid`或`guid`权限的文件包括`at`、`rcp`、`login`、`rsh`、`chase`、`csh`、`ssh`、`crontab`、`sudo`、`sendmail`、`ping`、`mount`以及几个UUCP工具。许多程序（如游戏）也可能具有访问设备的这种权限。

具有`suid`或`guid`权限的文件或程序有时会产生安全漏洞，因为它们绕过了普通权限。如果权限扩展到具有固有安全缺陷的可执行二进制文件（命令），问题会更加严重，因为它可能导致任何系统错误或获取root权限。在漏洞中，这种情况发生在用户向有漏洞的命令提供意外输入（例如长路径名或选项）时；命令将失败，用户将看到root提示符。尽管Linux开发者一直在密切关注糟糕的编程习惯，但新的漏洞不断被发现，并可能在意之外出现，特别是在尚未经过同行开发者评审的新软件包中。

精明的Linux管理员会将系统上的`suid`或`guid`文件的数量减少到最低。可以使用`find`命令显示系统上的所有此类文件：

```
# find -type f -perm +6000 exec ls -l {} \
```

# 第4章 命令行快速上手

> 注意

`find`命令非常有用，可以用于许多目的，例如在备份操作之前。请参见第13章“备份”中的“使用备份软件”章节。

请注意，程序并不非要从你的系统中移除。如果你的用户确实不使用该程序，你可以移除所有人的该程序执行权限。作为root操作员，你必须决定是否允许用户（例如）在你的系统上挂载和卸载CD-ROM或其他介质。虽然基于Linux的操作系统可以配置为易于使用和方便，但允许`mount`等程序可能不是最佳的安全策略。更改`suid`权限的其他候选对象可能包括`chsh`、`at`或`charge`命令。

## 以root身份工作

root或超级用户账户是一个特殊账户，在Unix和Linux系统中。超级用户权限是必要的，因为对重要的配置文件具有限制性权限。以root身份登录并使用Linux是危险的，因为你对系统拥有完全控制权。当你以root身份工作时，简单的`rm -fr /`就可以删除系统。

> 注意

了解如何在不以root身份登录的情况下以root运行命令可以帮助配置系统时的失误。Linux自带一个`su`命令，允许你以root身份执行命令并快速返回普通用户状态。例如，如果你想编辑文件系统表（描述本地或远程存储设备及其类型、位置的简单文件），可以这样使用`su`命令：

```
$ su -c "nano /etc/fstab"
```

> 注意

在编辑任何系统或软件配置文件之前，创建一个备份。确保在禁用换行的情况下启动文本编辑器。如果你在禁用换行的情况下编辑配置文件，可能会向内容插入多余的回车和换行符，导致服务在重启时失败。按照习惯，几乎所有的配置文件都格式化为80字符宽，但并非如此。默认情况下，`vi`和`emacs`编辑器不使用换行。

你可以使用相同的方法允许你执行一次性命令。上面的示例使用`sudo`如下：

```
$ sudo nano -w /etc/fstab
```

## 创建用户

当Linux系统管理员创建一个用户时，会在`/etc/passwd`中为该用户创建一个条目。系统还在`/home`目录下创建一个以用户名命名的目录。例如，如果你创建一个名为`bernice`的用户，用户的家目录就是`/home/bernice`。

> 注意

在本章中，你将学习如何从命令行管理用户。参见第10章“管理用户”，获取有关使用Ubuntu图形化管理工具（如图形用户管理客户端）进行用户管理的更多信息。

使用`useradd`命令结合用户名可以快速创建用户：

```
$ sudo useradd andrew
```

创建用户后，你必须使用`passwd`命令为用户创建初始密码：

```
$ sudo passwd andrew
```

更改用户andrew的密码。

新密码：

再次输入新密码：

pass:所有身份验证令牌已更新。

输入两次新密码。如果你没有为新用户创建初始密码，该用户将无法登录。

你可以通过使用命令及其`-D`选项查看`useradd`的默认用户设置，如下所示：

```
$ useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

这些选项显示了默认组ID、主目录、账户和密码策略（永久有效且无密码过期时间）、默认shell以及该shell的默认目录。

`useradd`命令有许多不同的命令行选项。该命令可用于设置新用户的密码策略和日期、分配登录shell、分配组成员关系以及用户账户的其他方面。

## 删除用户

使用`userdel`命令从你的系统中删除用户。该命令会删除系统`/etc/passwd`文件中的用户条目。你还应该使用该命令的`-r`选项来删除用户所有的文件和目录（例如用户的邮件池文件`/var/spool/mail`）：

```
$ userdel -r andrew
```

如果你不使用`-r`选项，则必须手动删除`/home`下的用户目录以及用户的`/var/spool/mail`队列。

## 关机

使用`shutdown`命令关闭你的系统。`shutdown`命令有许多不同的命令行选项（例如在预定时间关闭），但关闭Linux最快的方法是使用`-h`或`halt`选项，并配合单词`now`或数字零`(0)`，如下所示：

```
$ sudo shutdown -h now
```

## $ sudo shutdown -h 0

要结合定时关机并向所有活动用户发送相关消息，请使用`shutdown`的`time`和`message`选项，如下：

```bash
$ sudo shutdown -h 18:30 "System is going down for maintenance this evening"
```

此示例将在系统关机（或重启）前15分钟向所有活动用户提供警告信息。关闭正在运行的服务器可能是剧烈的，特别是当有活动用户或正在进行重要数据交换（例如正在备份）时。一种很好的方法是提前警告用户。这可以通过编辑系统的今日消息（MOTD）文件来实现，该文件会在用户登录后显示消息。要创建自定义的MOTD，请使用文本编辑器并更改`/etc/motd`的内容。你也可以将停机作为定期计划的一部分，或许与安全审计、软件更新或硬件维护同步。

你只应该在少数特定原因下关闭Ubuntu：

- 你没有在使用电脑，并希望节省电力。
- 你需要进行系统维护，需要停止任何或所有系统服务。
- 你需要更换核心硬件。

> 如果你怀疑一个或多个入侵者进入了你的系统，请勿关闭计算机；而是将机器与任何或所有网络断开，并对硬盘进行备份。你可能还希望保持机器运行，以便检查内存的内容和系统日志。

## 重启系统

你也应该使用`shutdown`命令重启你的系统。干净重启Linux最快的方法是使用`-r`选项以及单词`now`或数字零`(0)`：

```
$ sudo shutdown -r now
```

或者

```
$ sudo shutdown -r 0
```

如果在错误的时间执行（例如在备份或关键文件传输期间，这会引起用户系统的极满愤怒），重启和关机都可能导致严重后果。然而，基于Linux的操作系统设计为以有序的方式妥善停止活动系统服务。你可以用于关闭和重启Linux的其他命令是`halt`和`reboot`命令，但`shutdown`命令更加灵活。

## 阅读文档

尽管你在书中学习了使用Ubuntu的基础知识，但你仍然需要时间和实践来精通并解决Linux操作系统及其发行版中更复杂方面的问题。对于任何操作系统，当你继续使用Linux时，可以预计会遇到一些问题或困惑的问题。解决这些问题的首选地方是系统自带的文档；如果你找不到所需的信息，请检查Ubuntu网站。

Linux像Unix一样是一个自文档化系统，可以通过`man`命令访问man页。你可以使用`apropos`命令——例如使用如`partition`之类的关键字来查找与分区相关的命令：

- `apropos` - 分区
- `dump` - 格式化
- `fdisk` - 分区
- `group` - 组信息
- `probe` - 探测
- `whereis` - 查找

要了解Linux的详细信息，请使用`man`命令：

```
$ man rm
```

## 使用man页

要查看命令的man页，请使用`man`命令。你可以使用`apropos`命令——例如使用如`partition`之类的关键字来查找与分区相关的命令：

```
$ apropos partition
```

要了解Linux的详细信息，请使用`man`命令：

```
$ man less
```

要查看`less`的man页，你可以按`n`键向下翻页。要了解关于bash的更多信息，请使用`info`命令：

```
$ info bash
```

## Ubuntu和Linux命令

以下程序在命令行中非常常用，按类别组织以帮助你理解：

**管理用户和组**：`chage`、`fish`、`edquota`、`groupadd`、`groupmod`、`groups`、`mkpasswd`、`useradd`、`userdel`、`usermod`

**管理文件和文件系统**：`cat`、`cd`、`chattr`、`chmod`、`chown`、`compress`、`cp`、`dd`、`fdisk`、`find`、`in`、`mkdir`、`mksfs`、`mount`、`mv`、`rm`、`rpm`、`sort`、`swapon`、`swapoff`、`tar`、`touch`、`ummount`、`uncompress`、`uniq`

**管理运行程序**：`bg`、`fg`、`kill`、`killall`、`nice`、`ps`、`pstree`、`renice`、`top`、`watch`

**获取信息**：`apropos`、`cal`、`cmp`、`date`、`diff`、`dir`、`dmesg`、`du`、`env`、`free`、`grep`、`head`、`info`、`last`、`locate`、`ls`、`lsattr`、`man`、`more`、`pinfo`、`ps`、`pwd`、`stat`、`strings`、`tail`、`toc`、`top`、`uptime`、`vdir`、`stat`

**控制文本编辑器**：`ed`、`joe`、`mcedit`、`nano`、`sed`、`vim`

**控制互联网和网络命令**：`bind`、`ftp`、`host`、`hostname`、`ifconfig`、`links`、`lynx`、`mail`、`netconfig`、`netstat`、`ping`、`pump`、`route`、`scp`、`sftp`、`ssh`、`tcpdump`、`traceroute`、`whos`、`wire-test`

## 参考

- http://www.winntmag.com/Articles/Index.cfm?ArticleID=7420——由Windows NT用户编写的文章，他在尝试Linux时，轻率地承认在知道如何在控制台读取文本文件后重启了系统。
- http://standards.ieee.org/regauth/posix/——IEEE POSIX信息页。
- http://www.pathname.com/Comp/2362/lw-01/#sidebar——关于Linux和POSIX性的讨论。
- http://www.tldp.org/fhs/——Linux FHS（文件系统层次结构标准）主页。
- http://www.tldp.org/——浏览HOWTO章节查找并阅读《Linux Keyboard and Console HOWTO》——一份关于使用Linux键盘和控制台的过时指南。
- http://www.gnu.org/software/emacs/emacs.html——FSF GNU emacs编辑环境的主页，你可以在这里找到更多文档以及最新版本的源码链接。
- http://www.vim.org/——Linux发行版自带的vim（vi克隆）编辑器的主页。在此处查看该编辑器的更新、错误修复和新闻。
- http://www.courtesan.com/sudo/——sudo命令的主页。在此处查看最新更新、安全功能和错误修复。

# 第二部分 桌面Ubuntu

在本部分

- 第5章 互联网
- 第6章 生产力应用
- 第7章 多媒体应用
- 第8章 在Ubuntu上进行打印
- 第9章 游戏

# 第5章

## 本章内容

## 互联网

- 开始使用Firefox
- 选择电子邮件客户端
- RSS阅读器
- 使用Pidgin进行即时通讯
- 互联网中继聊天(IRC)
- Usenet网络新闻组
- Pan News客户端新闻阅读器
- 使用Ekika进行视频会议
- 参考文献

在现代世界中，互联网无处不在。从手机到办公室，从游戏机到iPad，我们被多条访问在线信息和通信的途径所包围。在通过互联网访问信息方面，Ubuntu并非局外之徒，它配备了网络浏览器、电子邮件客户端和其他工具，你可以利用这些工具与全球各地的人建立联系。

在本章中，我们将查看Ubuntu提供的一些互联网应用程序。你将了解到Firefox及其它的KDE替代方案Konqueror。我们将研究你使用Ubuntu安装的一些电子邮件客户端。其他主题还包括RSS订阅器、即时通讯（通过IRC和其他网络）以及阅读新闻组。最后，我们将快速查看Ekika，它是一个适用于Ubuntu的视频会议程序。

# 互联网简述

互联网本身由美国国防部于1969年创立。它被称为ARPANet，是以国防部高级研究计划局命名的。它的设计目的是建立一个能够抵御重大灾难（如冷战高峰）的网络，它很快扩展到包含越来越多的网络以构建互联网。然后，在1991年，欧洲核研究组织（CERN）的蒂姆·伯纳斯-李开发了万维网的概念，包括了超文本传输协议（HTTP）和超文本标记语言（HTML）。这带给了我们现在所知的互联网。

## 开始使用Firefox

Mozilla Firefox是最流行的浏览器之一，事实上也是Ubuntu的默认网络浏览器（见图5.1）。Firefox构建在源自Mozilla Suite的坚实代码基础上，为使用Internet Explorer浏览网页提供了一种替代方案。自2004年发布以来，Firefox的下载量已超过2.65亿次，并从Internet Explorer手中夺夺了巨大的市场份额。

![](img/10660b76df3ff0bf16a3b9e3a30edd9d_142_0.png)

图5.1 Firefox——重新发现网络。Firefox允许你添加许多升级，进一步提升你的体验。

在Ubuntu中，你可以在屏幕顶部的“应用程序-互联网”菜单中找到Firefox。更简单的启动Firefox的方法是点击系统菜单旁Firefox图标。无论哪种方式，Firefox都会打开。

除了基础程序外，还有丰富的插件和扩展，它们可以增强Firefox超越网页浏览的能力。像Shockwave Flash和Java这样的插件可以立即使用，因为它们是视频内容的多媒体解码器，而扩展则为浏览体验提供了有用的补充。例如，ForecastFirefox是一个可以提供本地天气状况的扩展，而Bandwidth Tester是一个计算你当前带宽的工具。随着Firefox的增长，会有更多的扩展和插件供你用来增强浏览乐趣。

## 选择电子邮件客户端

> 注意

Ubuntu允许访问Firefox 3，但仅作为预览。如果你好奇，可以使用synaptic下载它。

寻找和获取这些插件和扩展变得非常简单，因为Mozilla开发者们乐意创建了一个列表……

## 选择邮件客户端

![](img/10660b76df3ff0bf16a3b9e3a30edd9d_147_0.png)

图5.6 标准Evolution显示界面。在左侧你可以看到选择邮件、日历、备忘录和任务窗口的按钮。

![](img/10660b76df3ff0bf16a3b9e3a30edd9d_147_1.png)

图5.7 日历程序的“工具”界面是可以与其他共享信息的地方。在这里，可以配置时间和日期。

## 第5章 在互联网上

![](img/10660b76df3ff0bf16a3b9e3a30edd9d_148_0.png)

图5.8 Firefox的自然伴侣，Mozilla的轻量级邮件客户端Thunderbird可以在范围内使用。

## KMail

如果你使用的是KDE桌面环境而不是Ubuntu默认的GNOME桌面，你也将安装KMail。和它一样，Outlook或Mozilla Mail的用户很快就能适应KMail界面。KMail中发现的一些实用功能包括选择mbox或maildir格式、改进的过滤器创建、将邮件按线程排序的能力，以及在MTA中应用过滤的能力。图5.9显示了KMail邮件程序。KMail提供IMAP访问、广泛的过滤、mbox和maildir格式，以及轻松集成如Procmail、Spassassin或自定义处理脚本等MTA的功能。
