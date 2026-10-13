
变量 `$ftp` 实际上是一个对象，封装了 FTP 连接的所有繁琐工作，让你只需关注手头任务的具体细节。

![](img/5ced0c78d748bd190e9027e5549a3622_469_0.png)

> 在 www.cpan.org（CPAN 开发组的官方网站）可以找到大量关于 Perl 模块的有趣信息。另外，当你在网上寻找更多 Perl 信息时，也不要错过 www.theperljournal.com 和 www.perl.org！！

和本书中的许多章节一样，这一章只是冰山一角；关于强大的 Perl 编程语言，还有更多内容等待你学习。当然，在恰当的时候使用恰当的工具，可以把一个令人头疼的大麻烦变成令人愉快的胜利。说到底，谁是老板？是你，还是你的 Unix 系统？

#### 小结

这一章简要讨论了 awk 和 Perl 编程环境中一些最强大的功能。这就引出一个问题：你应该在什么时候用哪一个？我的回答是：

- 对于非常简单的操作，或需要运行许多不同程序时，使用 shell。
- 需要自动遍历输入文本各行时，使用 awk。
- 需要大量使用数组和哈希，或需要 CPAN 强大能力时，使用 Perl。

#### 问与答

问：那么 Perl 和 awk 哪个更酷？
答：毫无疑问是 Perl。你只要去 BN.com 之类的网站搜索 Perl，再搜索 awk，就会明白我的意思。

问：对于 Unix 系统管理员来说，除了 Perl、awk 和 shell 脚本之外，还有哪些选择？
答：还有其他一些选择，包括 Tcl 和 Python；你随时也可以使用 C、C++ 或其他正式编译型语言。不过请记住，合适的工具能让一切进行得更顺利。

#### 实战练习

##### 小测验

1. 你在 awk 中能做的一切，在 Perl 中也能做到，这是真的吗？
2. Perl 和 awk 之间最令人沮丧的差异之一是什么（想想数组）？
3. 在 awk 中，位置变量以某个特殊字符开头来引用，但非位置变量（如一行中的字段数）没有这个特殊字符前缀。这个字符是什么？
4. 在脚本中可以用哪两个字符作为前缀，来指定由哪个程序解释脚本内容？
5. 在 Perl 中使用 `-w` 和 `use strict` 的最大好处是什么？
6. 以 `$list` 和 `@list` 形式引用的变量有什么区别？

##### 答案

1. 确实如此。这是你选择学习哪种语言时值得考虑的一点。
2. Perl 的索引从 0 开始，而 awk 以 1 作为索引基准，因此 `$1` 在 awk 中是第一个值，而 `$list[1]` 在 Perl 中是第二个值。
3. 这个特殊字符是 `$`。
4. 这个神奇的两字符前缀是 `#!`，而且只有在文件被设置为可执行时才会生效。
5. 你大部分输入错误会在程序开始运行前就被 Perl 解释器捕获。
6. 以 `@` 引用的 Perl 变量是值的数组，而以 `$` 开头的变量则被视为数组中的一个特定值。请注意，同一个变量可以根据你要实现的目标以这两种方式引用！

本书的最后两章将探讨几乎每个 Unix 版本都会附带的 Apache Web 服务器。下一章介绍基本配置和设置，最后一章则深入讨论虚拟主机。

![](img/5ced0c78d748bd190e9027e5549a3622_473_0.png)

### 第23小时

### Apache Web服务器简介

我想对于相当大比例的读者来说，这是本书的关键章节。我可能喜欢编写关于shell脚本和配额的内容，但如果你是一个21世纪的Unix系统管理员，那么你很有可能至少负责一个作为Web服务器运行的系统。

好消息是，这本书的最后两小时专门讨论Web服务器主题（更不用说之前探讨Web日志文件的访问了）。注意，不是随便什么Web服务器，而是由Apache Group出品的、为互联网上比任何其他Web服务器都更多网站提供动力的Apache。

在这第一个小时的讲解中，我们将重点确保你的系统上有Apache，将其设置为基本的单系统使用，并学习如何让它平稳运行。

我们不会涉及超文本标记语言（HTML），或任何其他与创建网站相关的技术。如果你对这些主题感兴趣，我推荐你阅读我的著作《Creating Cool HTML 4 Web Pages》(Hungry Minds) 及其续篇《Dynamic HTML Weekend Crash Course》(Hungry Minds)。

在本小时中，你将学习如何：

- 设置你的Web服务器
- 使用 `httpd.conf` 文件配置Apache
- 测试连接性和功能

#### 设置你的Web服务器

这段旅程的第一步是看看你的Unix操作系统可能附带哪个版本的Apache。在撰写本文时，Red Hat Linux自带Apache 1.3.20，Mac OS X包含Apache 1.3.23，而Solaris包含Apache 1.3.12（位于有点奇怪的位置`/usr/apache/`）。

![](img/5ced0c78d748bd190e9027e5549a3622_474_0.png)

> 要确定你的版本，请找到`httpd`二进制文件（使用`locate`）并使用`-v`标志。例如：`/usr/sbin/httpd -v`。

Apache 2.0版本可通过Apache网站（www.apache.org）获得，而且相当稳定，但如果你只是提供基于HTML和CGI的页面，你可能希望继续使用当前发行的Apache版本。重要的是你至少有1.3版本。如果你使用的是1.2或更早版本，那么是时候升级了：1.3版本引入了重大的架构和性能变化，最明显的是配置文件布局方式的改变。

##### 任务23.1：激活Apache

在我们开始之前，快速说明一点：如果你想知道为什么我们专注于Apache而不是其他可能的服务器（特别是Netscape），答案包含在Apache网站上的这段简短引文中：

> 自1996年4月以来，Apache一直是互联网上最流行的Web服务器。2002年3月的Netcraft Web服务器调查（http://netcraft.com/survey/）发现，互联网上54%的网站使用Apache，因此它的使用范围比所有其他Web服务器加起来还要广泛。

1. 第一个也是最合理的测试是：Web服务器是否在你的系统上运行？有几种方法可以测试这一点，包括明显的 `ps -aux|grep httpd`，但我更喜欢尝试直接连接到服务器，看看会发生什么：

```
# telnet localhost http < /dev/null

Trying 127.0.0.1...

telnet: connect to address 127.0.0.1: Connection refused
```

它没有运行。可能有三个原因：Apache未安装，Apache已安装但未启用，或者Apache曾运行但崩溃了。希望不是最后一个原因，但你可以通过检查syslog文件（可能是`/var/log/messages`）来确定。如果你没有安装Apache，请翻回第8小时“Unix软件包管理”，搜索并安装`apache-1.3*`软件包或其等效版本（在网络连接良好的情况下，总共大约需要15分钟）。但如果是服务器根本没有运行呢？让我们详细看看这种情况。

2. 与任何服务一样，你可以手动启动Apache，也可以进行设置，使系统在进入所需运行状态时自动启动它（可能是运行状态3和运行状态5——在Red Hat Linux上分别对应多用户/无GUI和多用户+GUI）。但请记住，不同的Unix系统对运行级别的定义不同——参见第13小时“更改系统状态”。

要手动启动，可以使用Apache发行版附带的`apachectl`脚本，但我更喜欢使用Linux系统上位于`/etc/rc.d/init.d/`中的系统控制脚本（如果已安装）。

```
/etc/rc.d/init.d/httpd status
httpd is stopped
```

这很合理。

现在，自从Apache RPM包安装到系统上以来，我们还没有碰过配置，因此启动它可能会产生意想不到的后果。那么让我们试试吧！

```
/etc/rc.d/init.d/httpd start
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

3. 要让Apache在每次系统启动时自动启动，我们需要确保从相应的`rc?.d`目录到`init.d`中的脚本有一个链接。快速检查发现，Apache RPM确实安装了这些链接，但默认情况下是让服务器停止而不是启动：

```
# ls /etc/rc.d/rc?.d/*httpd
/etc/rc.d/rc0.d/K15httpd
/etc/rc.d/rc1.d/K15httpd
/etc/rc.d/rc2.d/K15httpd
/etc/rc.d/rc3.d/K15httpd
/etc/rc.d/rc4.d/K15httpd
```
