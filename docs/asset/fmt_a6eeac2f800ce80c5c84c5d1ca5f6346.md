
假设你想查看 `swapon` 的手册页。你执行 `man swapon`。你实际上会得到系统调用 `swapon(2)` 的手册页，这是你在 C 程序中用于开启交换功能的函数。除非你正在编写自己的程序来执行此操作，否则这可能不是你想要的。因此，使用上表，你可以看到你想要的可能是“系统命令”，位于第 8 部分。然后你可以执行 `man 8 swapon`。这一切都是因为 `man` 按顺序搜索 `man` 目录，找到第一个匹配项后就返回。

你也可以在手手册页中搜索字符串。你可以使用 `man -k string to_search_for` 来实现这一点。但是，除非 `makewhatis` 数据库已经创建，否则这不会起作用。在 Red Hat Linux 中，这是由一个在夜间运行的 `cron` 作业完成的。如果你没有让你的系统在夜间保持运行，数据库将不会被创建。如果是这种情况，请以 `root` 用户身份运行以下命令：

```
/etc/cron.weekly/makewhatis.cron
```

完成之后，你可以输入 `man -k swapon`。该命令将返回：

```
##### man -k swapon
swapon, swapoff (2) - start/stop swapping to file/device
swapon, swapoff (8) - enable/disable devices and files for \
paging and swapping
```

因此，你可以看到第 2 部分和第 8 部分都有关于 `swapon`（在本例中还有 `swapoff`）的页面。

### 6.1.2 软件包文档

许多软件包都有 `README` 文件和其他文档作为源软件包的一部分。Red Hat Linux 使用标准位置安装这些文档，这样你就不必安装源文件来查看文档了。所有这些文档都存储在 `/usr/doc` 的子目录中。子目录取决于软件包。每个有额外文档的软件包都会创建一个名为 `packagename-version-releasename` 的目录。例如，`tin` 软件包的版本可能是 `1.22`，发布号为 `2`。其文档的路径将是 `/usr/doc/tin-1.22-2`。

大多数情况下，此目录中的文档是 ASCII 格式的。你通常可以使用 `more filename` 或 `less filename` 来查看它们。这很好，但如果你想知道某个特定命令或文件是否有文档，却不知道它来自哪个软件包怎么办？没关系！你可以简单地输入：

```
rpm -qdf /etc/sendmail.cf
```

这将报告包含 `/etc/sendmail.cf` 文件的软件包中的所有文档。这类命令在 `RPM-HOWTO` 中有更深入的介绍，可从 `www.redhat.com` 获取。

另外，如果你需要帮助的是一个命令，而手册页写得不好怎么办？你可以做类似这样的事情：

```
rpm -qdf 'which COMMAND'
```

同样，`"COMMAND"` 是你需要帮助的实际命令。只有当该命令在你的路径中时，这才会起作用。

### 6.1.3 HOWTO 和 FAQ

Linux 文档项目（LDP）的大部分内容都可以在你的系统的 `/usr/doc` 中找到。

`/usr/doc/HOWTO` 包含我们在压制 CD-ROM 时所有可用 HOWTO 的 ASCII 版本。它们是经过 `gzip` 压缩的，因此你必须使用 `gunzip` 来解压它们，或者使用如下命令：

```
zcat HAM-HOWTO.gz | more
```

后者可以工作，但比先解压再使用 `more` 稍微缺乏灵活性。不过，解压也需要更多的磁盘空间，除非你完成后重新压缩该文档。

`/usr/doc/HOWTO/mini` 包含所有可用的 mini-HOWTO 的 ASCII 版本。它们没有压缩，可以使用 `more` 或 `less` 查看。

`/usr/doc/HTML` 包含所有 HOWTO 和 *《Linux 安装与入门》* 指南的 HTML 版本。要查看这里的内容，只需使用 WWW 浏览器，例如 Red Hat Software 的 `redbaron` 或 `arena`。你可以做类似这样的事情：

```
cd /usr/doc/HTML
arena index.html
```

`/usr/doc/FAQ` 包含一些流行 FAQ 的 ASCII 版本（以及一些 HTML 版本），包括 `RedHat-FAQ`。它们都可以使用 `more` 或 `less` 查看。

### 6.1.4 “locate” 命令

当你不知道命令或文件的完整名称，但需要找到它时，你通常可以用 `locate` 找到它。`locate` 使用数据库来查找你系统上的所有文件。通常，此数据库每晚由 `cron` 作业构建。然而，如果你的机器没有一直启动到 Linux，这种情况就不会发生。因此，如果是这种情况，你可能偶尔需要运行以下命令：

```
/etc/cron.daily/updatedb.cron
```

执行此操作时，你需要在系统上具有 `root` 权限。这将使 `locate` 能够正常工作。

因此，如果你知道你需要找到所有的 “finger” 文件，你可以运行：

```
locate finger
```

它应该返回类似以下内容：

```
/usr/bin/finger
/usr/lib/irc/script/finger
/usr/man/man1/finger.1
/usr/man/man8/in.fingerd.8
/usr/sbin/in.fingerd
```

然而，需要注意的是，`locate` 不仅基于文件名返回匹配项，也基于路径名返回。因此，如果你的系统上有一个 `/home/djb/tinger/` 目录，它将连同该目录中的所有文件一起被返回。

### 6.1.5 “info” 页

虽然 `man` 是最普遍的文档格式，但 `info` 功能强大得多。它提供超文本链接，使阅读大型文档变得更加容易，并且受到许多文档编写者的青睐。有一些非常完整的 `info` 文档涵盖了 Red Hat 的各个方面（尤其是来自 GNU 项目的部分）。

要阅读 `info` 文档，请不带任何参数使用 `info` 程序。它会向你展示可用文档的列表。如果找不到某些内容，可能是因为你没有安装包含该文档的软件包。使用 `RPM` 安装它，然后重试。

如果你习惯使用 `emacs`，你有一个内置的浏览器用于查看 `info` 文档。使用 `Ctrl-h` `Ctrl-i` 来查看它。

`info` 系统是一个基于超文本的系统。出现的任何高亮文本都是指向更多信息的链接。使用 `Tab` 将光标移动到链接处，按 `Enter` 跟随链接。按 `p` 返回上一页，按 `n` 移动到下一页，按 `u` 上一级文档层级。要退出 `info`，按 `Ctrl-x` `Ctrl-c`（先按控制-x 再按控制-c）。

学习如何使用 `info` 的最好方法是阅读关于它的 `info` 文档。如果你阅读 `info` 呈现给你的第一个屏幕，你就能够开始上手了。

## 6.2 来自互联网社区的帮助

### 6.2.1 Red Hat 邮件列表

如果你无法在线找到针对你的问题的帮助，并且你有 WWW 访问权限，你应该访问 `http://www.redhat.com/support/mailing-lists/`。

#### 6.2. 来自互联网社区的帮助

你可以搜索 `redhat-list` 的存档。许多问题在那里已经得到了解答。

每个列表的订阅地址如下：

```
redhat-list-request@redhat.com
redhat-digest-request@redhat.com
redhat-announce-list-request@redhat.com
redhat-devel-list-request@redhat.com
rpm-list-request@redhat.com
axp-list-request@redhat.com
sparc-list-request@redhat.com
```

若要订阅，请向你想订阅的列表地址发送电子邮件，并在 `Subject:` 行中包含 `subscribe`。

若要取消订阅，请向你想取消订阅的列表地址发送电子邮件，并在 `Subject:` 行中包含 `unsubscribe`。

然后，若要向列表发送邮件，只需向上述地址（去掉名称中的 `-request`）发送即可。唯一的例外是 `redhat-digest`，它仅是 `redhat-list` 的摘要版本。在这种情况下，地址为 `redhat-list@redhat.com`。

### 6.2.2 Usenet 新闻组

另一个良好的帮助来源是 USENET 上的 `comp.os.linux` 层次结构。如果你熟悉新闻组，应该去查看一下。

# 第 7 章 使用 RPM 进行包管理

Red Hat Package Manager (`RPM`) 是一个可供任何人使用的开放打包系统，它既适用于 Red Hat Linux，也适用于其他 Linux 和 UNIX 系统。Red Hat Software 鼓励其他厂商抽出时间研究 `RPM`，并用于其自己的产品。`RPM` 在 GPL 条款下可分发。
