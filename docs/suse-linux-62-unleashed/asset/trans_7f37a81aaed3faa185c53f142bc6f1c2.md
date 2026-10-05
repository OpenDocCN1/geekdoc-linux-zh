
# 自动化任务
第 22 章
649

# Emacs

Emacs 是计算机用户中引发宗教性争议的最具极化的风极针话题之一。Emacs 拥有许多智能且狂热的用户，他们认为它是所有自动化尝试的理想平台。它的追随者已将其最初的一个屏幕编辑器开发成一个具有新闻组讨论、Web 浏览、应用程序开发、通用脚本编写等功能的工具。对于本章而言，你需要了解关于 Emacs 的信息如下：

- 它是一款你在这职业生涯中某个时刻应该尝试的编辑器。
- 如果你偏好集成开发环境，Emacs 可以完成你想象的几乎任何事情。作为一个编辑器，它可以模拟任何其他编辑器，而且它的开发者确保了它在语言引导的格式化、应用程序集成和开发自动化方面始终提供最先进的功能。

即使 Emacs 的“重量”（它在启动时可能看起来慢，并且需要大量的学习和配置）让你对其日常使用望而却步，也请记住它是如何通过复杂的编程让常用操作变得更高效的典范。

![](img/cbac72550c7126a22162e94d91a0c360_684_0.png)

> 注意
SuSE Linux 包含了 Emacs 编辑器。你可以在不使用 X Window 系统的情况下使用 Emacs。在控制台的命令行或 X11 终端窗口中输入单词 emacs 并按回车键。按下 Ctrl+H 和 T 键运行其内置教程。

# procmail

在互联网时代，计算机的使用呈爆炸式增长。最不可或缺、经常使用的互联网功能是电子邮件。电子邮件可以自动化吗？

是的——自动化电子邮件可能是你投资回报最高的单项。除了别名、分发列表、启动配置以及具有各种功能的邮件代理或客户端之外，你还会想学习 procmail。假设你每天收到的一百封邮件，其中五分之一可以完全自动处理，而处理单封邮件至少需要你花费三秒时间；这些都是保守估计。一点 procmail 自动化每天就能为你节省至少一分钟，或者每年节省六小时。即使是保守的估计也清楚，花一小时设置 procmail 就能多倍地回本。

# SuSE 系统管理
第三部分

有了 procmail 的 man 页面，对 procmail 的认真研究从页面 http://www.faqs.org/faqs/mail/filtering-faq，Nancy McGough 的 Filtering Mail FAQ 开始。它提供了详细的安装和调试指南。你还会在 /usr/doc/howto/en 目录下的 Mail-HOWTO 中找到关于 procmail 的信息。

由于你的 SuSE Linux 机器几乎已经正确配置了 procmail，你可以立即开始编写个人使用的程序。作为第一个实验，创建这些文件： ~/.procmailrc，内容如下：

```bash
VERBOSE=on
MAILDIR=$HOME/mail
SPAMDIR=$HOME/.procmail
LOGFILE=$SPAMDIR/log
INCLUDER=$SPAMDIR/rc.testing
```

~/.procmail/rc.testing，包含以下代码：

```bash
:0:
* Subject:.*HOT
SPAM.HOT
```

~./forward，内容如下：

```bash
"!IFS=" & -& exec /usr/bin/procmail -f !! exec 75 #YOUR_EMAIL_NAME
```

在创建这三个文件后，使用以下命令设置必要的权限：

```bash
# chmod 644 ./forward
# chmod ax ./.
```

现在使用以下命令测试你的过滤器：

```bash
# echo "This message 1." ! mail -s "Example of HOT SPAM." YOUR_EMAIL_NAME
# echo "This message 2." ! mail -s "Desired message." YOUR_EMAIL_NAME
```

你现在在邮箱中看到的只有一个新条目：主题为 Desired message 的那一个。你还在家目录下有一个新文件 SPAM.HOT，保存了第一封邮件。

procmail 是一个健壮、灵活的工具，你可以通过编写它来实现比这更有用的自动化。当你熟悉它后，构建规则将变得自然而然，例如：自动丢弃明显的垃圾邮件、对入站邮件列表流量排序，甚至可能实现转发、远程系统监控或 FAQ 回应。这每天可以为你节省大量时间。

# 内部脚本

你所拥有的最有效工具之一是在你的应用程序内部寻找机会。脚本编写已成为一个普遍的主题，几乎所有工具都可以编写脚本。你所拥有的最有效工具之一是在你的应用程序内部寻找机会。脚本编写已成为一个普遍的主题，几乎所有工具都可以编写脚本。

# 自动化爱好者的总结挑战

在本章中，你学习了各种使用计算机使其为你服务的方法。你现在知道如何提高你的技能，并已准备好迎接下一个挑战：如何将你的技能提升到下一个水平？

