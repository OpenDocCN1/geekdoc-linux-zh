
![](img/5ced0c78d748bd190e9027e5549a3622_473_0.png)

## 第23小时

## Apache Web服务器简介

我想对于相当大比例的读者来说，这是本书的关键章节。我可能喜欢编写关于shell脚本和配额的内容，但如果你是一个21世纪的Unix系统管理员，那么你很有可能至少负责一个作为Web服务器运行的系统。

好消息是，这本书的最后两小时专门讨论Web服务器主题（更不用说之前探讨Web日志文件的访问了）。注意，不是随便什么Web服务器，而是由Apache Group出品的、为互联网上比任何其他Web服务器都更多网站提供动力的Apache。

在这第一个小时的讲解中，我们将重点确保你的系统上有Apache，将其设置为基本的单系统使用，并学习如何让它平稳运行。

我们不会涉及超文本标记语言（HTML），或任何其他与创建网站相关的技术。如果你对这些主题感兴趣，我推荐你阅读我的著作《Creating Cool HTML 4 Web Pages》(Hungry Minds) 及其续篇《Dynamic HTML Weekend Crash Course》(Hungry Minds)。

在本小时中，你将学习如何：

- 设置你的Web服务器
- 使用`httpd.conf`文件配置Apache
- 测试连接性和功能

### 设置你的Web服务器

这段旅程的第一步是看看你的Unix操作系统可能附带哪个版本的Apache。在撰写本文时，Red Hat Linux自带Apache 1.3.20，Mac OS X包含Apache 1.3.23，而Solaris包含Apache 1.3.12（位于有点奇怪的位置/usr/apache/）。

![](img/5ced0c78d748bd190e9027e5549a3622_474_0.png)

> 要确定你的版本，请找到httpd二进制文件（使用locate）并使用`-v`标志。例如：/usr/sbin/httpd -v。

Apache 2.0版本可通过Apache网站（www.apache.org）获得，而且相当稳定，但如果你只是提供基于HTML和CGI的页面，你可能希望继续使用当前发行的Apache版本。重要的是你至少有1.3版本。如果你使用的是1.2或更早版本，那么是时候升级了：1.3版本引入了重大的架构和性能变化，最明显的是配置文件布局方式的改变。

### 任务23.1：激活Apache

在我们开始之前，快速说明一点：如果你想知道为什么我们专注于Apache而不是其他可能的服务器（特别是Netscape），答案包含在Apache网站上的这段简短引文中：

> 自1996年4月以来，Apache一直是互联网上最流行的Web服务器。2002年3月的Netcraft Web服务器调查（http://netcraft.com/survey/）发现，互联网上54%的网站使用Apache，因此它的使用范围比所有其他Web服务器加起来还要广泛。

1. 第一个也是最合理的测试是：Web服务器是否在你的系统上运行？有几种方法可以测试这一点，包括明显的`ps -aux|grep httpd`，但我更喜欢尝试直接连接到服务器，看看会发生什么：

```
# telnet localhost http < /dev/null
Trying 127.0.0.1...
telnet: connect to address 127.0.0.1: Connection refused
```

它没有运行。可能有三个原因：Apache未安装，Apache已安装但未启用，或者Apache曾运行但崩溃了。希望不是最后一个原因，但你可以通过检查syslog文件（可能是/var/log/messages）来确定。如果你没有安装Apache，请翻回第8小时“Unix软件包管理”，搜索并安装apache-1.3*软件包或其等效版本（在网络连接良好的情况下，总共大约需要15分钟）。但如果是服务器根本没有运行呢？让我们详细看看这种情况。

2. 与任何服务一样，你可以手动启动Apache，也可以进行设置，使系统在进入所需运行状态时自动启动它（可能是运行状态3和运行状态5——在Red Hat Linux上分别对应多用户/无GUI和多用户+GUI）。但请记住，不同的Unix系统对运行级别的定义不同——参见第13小时“更改系统状态”。

要手动启动，可以使用Apache发行版附带的apachectl脚本，但我更喜欢使用Linux系统上位于/etc/rc.d/init.d/中的系统控制脚本（如果已安装）。

```
# /etc/rc.d/init.d/httpd status
httpd is stopped
```

这很合理。

现在，自从Apache RPM包安装到系统上以来，我们还没有碰过配置，因此启动它可能会产生意想不到的后果。那么让我们试试吧！

```
# /etc/rc.d/init.d/httpd start
Starting httpd:               [  OK  ]
```

嘿！成功了！

```
# telnet localhost http < /dev/null
Trying 127.0.0.1...
Connected to local host.
Escape character is '^]'.
Connection closed by foreign host.
```

3. 要让Apache在每次系统启动时自动启动，我们需要确保从相应的rc?.d目录到init.d中的脚本有一个链接。快速检查发现，Apache RPM确实安装了这些链接，但默认情况下是让服务器停止而不是启动：

```
# ls /etc/rc.d/rc?.d/*httpd
/etc/rc.d/rc0.d/K15httpd
/etc/rc.d/rc1.d/K15httpd
/etc/rc.d/rc2.d/K15httpd
/etc/rc.d/rc3.d/K15httpd
/etc/rc.d/rc4.d/K15httpd
/etc/rc.d/rc5.d/K15httpd
/etc/rc.d/rc6.d/K15httpd
```

改变起来很容易。进入与目标运行级别对应的适当目录，并将名称中的K改为S（有关如何使用运行级别和初始化脚本的更多详细信息，请参见第13小时）。

```
# cd /etc/rc.d/rc3.d/
# mv K15httpd S15httpd
# cd ..
# mv K15httpd S15httpd
```

就这样。对于这个Red Hat Linux系统，下次启动或切换到运行级别3或5时，它将自动启动Apache Web服务器。

4. 让Apache在Mac OS X中开始工作是一件轻而易举的事：转到“系统偏好设置”中的“共享”控制面板，然后点击“Web共享已关闭”下方的“启动”按钮，如图23.1所示。

**图23.1**  
启用Mac OS X Web服务器。

![](img/5ced0c78d748bd190e9027e5549a3622_476_0.png)

仅此而已！

5. Solaris上启用Web服务器的方法有点复杂，但也不算太复杂。Apache控制程序apachectl（apache控制）位于/usr/apache/bin中：

```
# /usr/apache/bin/apachectl
usage: /usr/apache/bin/apachectl {start|stop|restart|fullstatus|status|graceful|configtest|help}
```

- `start` — 启动httpd
- `stop` — 停止httpd
- `restart` — 如果正在运行，则通过发送SIGHUP重启httpd；如果未运行，则启动它
- `fullstatus` — 转储完整的状态屏幕；需要lynx并启用mod_status
- `status` — 转储简短的状态屏幕；需要lynx并启用mod_status
- `graceful` — 通过发送SIGUSR1进行优雅重启；如果未运行则启动它
- `configtest` — 进行配置语法测试
- `help` — 显示此屏幕

```
# /usr/apache/bin/apachectl start
fopen: No such file or directory
httpd: could not open document config file /etc/apache/httpd.conf
/usr/apache/bin/apachectl start: httpd could not be started
```

令人惊讶的是，Solaris版的Apache需要我们先指定适当的配置，然后才能启动进行测试。这就是关于无法打开配置文件错误信息的含义。

好了，我们复制一个示例配置文件，然后重试：

```
# cd /etc/apache
# ls
access.conf   jserv.conf    magic         srm.conf
httpd.conf.example  jserv.properties  mime.types    zone.properties
# cp httpd.conf.example httpd.conf
# /usr/apache/bin/apachectl configtest
Syntax OK
# /usr/apache/bin/apachectl start
/usr/apache/bin/apachectl start: httpd started
```

这次请注意，我们运行了有用的apachectl配置测试模式，没有收到任何错误。然后我们启动了服务器，一切正常。

有趣的是，Solaris自带的Apache服务器配置为在多用户运行级别启动，但在执行上述手动步骤（复制httpd.conf.example文件）之前，服务器本身无法启动。

```
# ls /etc/rc?.d/*apache
/etc/rc0.d/K16apache
/etc/rc1.d/K16apache
/etc/rc2.d/K16apache
/etc/rc3.d/S50apache
/etc/rc5.d/K16apache
```

这意味着，在你手动启动Apache之后，就可以使用了。

无论Unix的哪种变体，在你的系统上启用Web服务器都是相当容易的——当然比创建一个高质量的网站要容易得多。
