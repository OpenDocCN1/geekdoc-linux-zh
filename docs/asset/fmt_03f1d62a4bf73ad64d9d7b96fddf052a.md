
```
$ where fdisk
fisk: /sbin/fdisk /usr/share/man/man8/fdisk.8
```

### 使用 man 页面

要学习某个命令或程序，请使用 `man` 命令，X Window 窗口后跟的是命令名称。Linux 和 X 的 man 页位于 `/usr/share/man`、`/usr/local/share/man` 和 `/usr/X11R/man` 目录；例如，要读取 `rm` 命令的页面，可以这样使用 `man` 命令：

```
$ man rm
```

按下回车键后，`less`（一种 Linux 分页器命令）会显示 man 页。`less` 命令是一个文本浏览器，你可以向前或向后（甚至是横向）滚动文档以了解更多关于该命令的信息。输入字母 `h` 获取帮助，使用正斜杠 `/` 输入搜索字符串，或按 `q` 退出。

注意

虽然 Linux 包含的数百个 GNU 命令中每个命令都有一个 man 页，但你必须使用 `info` 命令来阅读有关使用 GNU 命令的详细信息。例如，要了解更多关于 `bash`（它有一个相当详尽的手册页），请使用 `info` 命令查找：

```
$ info bash
```

按 `n` 和 `p` 键在文档中导航，或向下滚动到屏幕上的菜单项并按回车键读取特定功能。按 `q` 退出阅读。

### 相关 Fedora 和 Linux 命令

以下是在命令行命令行工作时常用的程序和内置命令。这些命令按类别组织，帮助你理解命令的作用。如果你需要查找使用该命令的信息，可以在该命令的 man 手中找到。

- 管理用户和组—`chage`, `cfn`, `chsh`, `equdata`, `gpasswd`, `groupadd`, `groupdel`, `usermod`, `mkpasswd`, `newgrp`, `passers`, `umask`, `useradd`, `usermod`

- 管理文件和系统—`cat`, `cd`, `chattr`, `chmod`, `compress`, `cp`, `dd`, `fdisk`, `find`, `gzip`, `in`, `mkdir`, `mkfs`, `mount`, `mv`, `rm`, `rdir`, `rpm`, `sort`, `swapon`, `tar`, `touch`, `ummount`, `uncompress`, `unzip`, `zip`

- 管理运行程序—`bg`, `fg`, `killall`, `nice`, `ps`, `ptrace`, `renice`, `top`, `watch`

- 获取信息—`apropos`, `cal`, `cat`, `cmp`, `date`, `diff`, `df`, `dir`, `dmesg`, `du`, `env`, `file`, `free`, `grep`, `head`, `info`, `last`, `less`, `ls`, `lattr`, `man`, `minefo`, `ps`, `stat`, `strac`, `tac`, `tail`, `top`, `uptime`, `vdmat`, `w`, `wcat`, `whis`, `which`, `whoami`

- 控制台编辑器—`ed`, `jed`, `joe`, `mcedit`, `nano`, `red`, `sed`, `vim`

- 控制台互联网和网络命令—`bind`, `elm`, `ftp`, `host`, `hostname`, `ifconfig`, `links`, `lyn`, `mail`, `multicast`, `nctop`, `netconfig`, `netstat`, `ping`, `pump`, `rd`, `route`, `scp`, `sftp`, `ssh`, `tcpdump`, `traceroute`, `whois`, `wiretest`

### 参考

迁移到新的操作系统对于管理层和用户来说不必是痛苦的。提供易于懂的指导、一些背景信息以及已安装系统的预配置可以处理这种过渡。

本节列出了一些额外的参考点，带有本章中讨论的标准和命令的背景信息。浏览这些列表以学习更多关于本章讨论的概念，并扩展你对新 Linux 社区的知识。

- http://www.mint.com/Articles/Index.cfm?Article=7420—一篇由 Windows NT 用户写的文章，他在尝试 Linux 时，盲目地承认在不知道如何在 Linux 控制台读取文件后，盲目地重启了系统。

- http://standards.ieee.org/regauth/posix/—IEEE POSIX 信息页。

- http://www.itworld.com/Comp/2362/lw-01-government/#sidebar—关于 Linux 和 POSIX 兼容性的讨论。

- http://www.pathname.com/fhs/—Linux FHS（Linux 文件系统）主页。

- http://www.pathname.com/fhs/—Linux FHS（Linux 文件系统）主页。

- http://www.gnu.org/software/emacs/—emacs 主页。

- http://www.gnu.org/software/sudo/—sudo 主页

- http://www.vim.org/—vim 主页

## 第二部分

## 桌面

## 第 5 章 互联网

互联网已经永远改变了我们访问和共享的方式。我们查看互联网的方式不断改进。

- 浏览互联网

- 选择邮件客户端

- RSS 阅读器

- 使用 Pidgin 进行即时消息

- Usenet 群

- 使用 Ekika 进行视频会议

互联网的简要介绍

互联网本身由美国国防部于 1969 年首次带来。它以国防部的高级计划署命名为 ARPANet。设计目标是建立一个可以抵御重大灾难的网络（这是冷战的高峰），它很快扩展到更多领域。随后，1991 年 CERN 的 Tim Berners-Lee 开发了万网的想法，包括超文本传输协议 `HTTP` 和超文本标记语言 `HTML`。这带给了我们熟悉的互联网。

### Mozilla Firefox

最流行的网络浏览器之一，事实上也是 Fedora 的默认网络浏览器，Mozilla Firefox（见图 5.1）。它基于自 Mozilla Suite 的可靠代码库，与 Internet Explorer（仅限 Windows）相比带来了清新的空气。Firefox 提供了一个安全的浏览环境，并可以通过插件和扩展增强浏览体验，我们稍会在本节中简要介绍。自 2004 年底发布以来，Firefox 的下载量已超过 2.6 亿次，它从 Internet Explorer 手中夺得了大量的市场份额。

在 Fedora 中，你可以在屏幕顶部的应用程序、互联网菜单找到 Firefox。另一种简单的启动 Firefox 的方法是点击操作菜单的小图标。无论哪种方式，Firefox 都会打开。

![](img/4473647b35365e8747aa8fb2cf969fd5_142_0.png)

图 5.1 Firefox—重新发现 Web。Firefox 扩展允许许多升级，进一步增强你的体验。

除了基础程序，还有丰富的插件和扩展可以增加 Firefox 的功能。插件如 Shockwave Flash 和 Java 可以可用，还有查看视频内容的媒体解码器，而扩展为浏览体验提供了有用且有趣的补充。例如，ForecastFirefox 是提供本地天气状况的扩展，Bandwidth Tester 是计算当前带宽的工具。也许度过闲下午最好的方法是下载 StUpon 扩展，它提供了一个著名的按钮，根据你选择的某些预设条件点击即可跳转到网页。你可能经常会遇到一些 Calvin and Hobbes 连环，正当你需要时它让你微笑。

### 浏览互联网

你需要的它。然而，你可以通过 StumbleUpon 发现真正的宝藏。随着 Firefox 的发展，会有越来越多的扩展和插件供你使用，以增强你的浏览体验。

寻找和获取这些插件和扩展并不容易，因为 Mozilla 开发者们乐意地创建了一个专用网站，旨在帮助你从 Firefox 中获得更多收益。特别受欢迎的是 Adblock Plus 和 StumbleUpon 插件。Adblock 允许你在浏览时杀掉所有占用大量带宽的烦人横幅和动画。StumbleUpon 是一个非常棒的插件，你可能会对此上瘾，并最终在点击“惊喜（stumble）”按钮上浪费好几个小时！

我们非常推荐的另一个插件是 Google BrowserSync。如果你在多台电脑之间工作，那么你就不必在每台电脑上重新创建书签并尝试保持它们一致。Google 让这个过程变得简单得多，它允许你在多个浏览器之间同步不仅是书签，还有 Cookie、浏览器历史和任何保存的密码。请记住，你可以选择想要同步的内容，只需复制你的书签就非常简单。

### Konqueror

KDE 用户可以选择使用 Konqueror，它是 KDE 的默认浏览器（图 5.2）。除了处理文件系统导航，Konqueror 还可以用于浏览网页。它同样基于 Firefox 使用的 Gecko 渲染引擎。

![](img/4473647b35365e8747aa8fb2cf969fd5_143_0.png)

图 5.2 Konqueror，标准的 KDE 和文件系统浏览器。

### 选择邮件客户端
