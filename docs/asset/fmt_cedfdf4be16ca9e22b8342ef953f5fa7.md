
| `.R` | 对作为参数提供的文本使用罗马字体。 |
| `.SH` | 章节标题（按照惯例名称大写）。 |
| `.TH` | 标题头部（参数为命令名和章节）。 |
| `.TP` | 标记段落（使用悬挂缩进）。 |
| `.TP n` | `n` 指定缩进量。 |

通过测试帮助页，你可以使用以下命令模拟对文件的实际帮助页调用：

```
$ nroff <file> ; more
```

帮助页并不是机智的系统管理员寻求答案的唯一途径。还有互联网。在互联网中，有电子邮件、描述如何操作的网页以及新闻组（newsgroups）。

# 电子邮件

通过电子邮件，你可以向那些你正在从事相似工作的人提问。例如，当我开始编写 Perl 脚本时，会给 Rich 发封便条。他会放下手头工作立即回答我的问题（呵呵，得吧！）。要点是，你结识的人中有人可以帮助解决问题，或指引你通向成功。如果你不知道有谁在用 Red Hat Linux，你可以做两件事：首先，寻找新朋友——显然是那些你一直疏远的朋友；其次，你可以使用电子邮件新闻组。

![](img/421e47878893966b6e8fcf1c1c761441_357_0.png)

# Red Hat 邮件列表和新闻组

许多邮件列表和新闻组可以帮助你解决问题。在使用 Linux 了一段时间后，可能会产生一些你可以回答的问题。新闻组是极佳的信息来源。在我列出你可以使用的的新闻组之前，我想提一下 Red Hat 邮件列表 (`http://www.redhat.com/support/mailing-lists`)。

> 新闻组是一个发布帖子和获取帖子的地方。当你加入邮件列表时，你会以批量形式或在帖子产生时接收到它们。

这些列表由 Red Hat 维护，并受到 Red Hat 的监控。目前有十三个不同的列表，直接来自 Red Hat 网页，它们是：

- `redhat-list`

用于与 Red Hat Linux 相关的主题讨论。

- `redhat-digest`

这是 `redhat-list` 的摘要版本。与其接收 `redhat-list` 的逐条邮件，此列表的订阅者收到的是定期汇总。

- `redhat-announce-list`

这是最重要的列表。所有 Red Hat 用户都应该订阅。这里会发布安全更新和新的 RPM。它的流量很低，为了方便你的使用。

- `redhat-install-list`

仅用于与安装相关的主题讨论。这包括专有硬件、硬件问题、软件包选择等。

- `redhat-ppp-list`

用于 Red Hat 下 PPP 的通用讨论。包括配置、安装、更改等。

- `redhat-devel-list`

用于 Red Hat 下的软件开发讨论。

- `sparc-list`

用于 SPARC 架构特定问题。这包括内核开发等。

- `axp-list`

用于 Alpha 架构特定问题。这包括内核开发等。

- `rpm-list`

用于 RPM 相关问题的讨论。这包括通用 RPM 使用、使用 shell 脚本开发、将 RPM 移植到非 Linux 架构等。

- `applware-list`

用于应用程序讨论。主要涉及安装和使用。

- `cde-list`

用于 CDE 讨论。主要涉及安装和使用。

- `forsale-list`

该列表用于发布计算机类物品的出售和求购信息。这包括软件和硬件，且应仅限于适用于 Linux 的物品。

- `post-only`

这是一个虚拟列表。它没有发布地址，只有一个请求地址 (`post-only-request@redhat.com`)。你可以订阅此列表，之后就可以向任何 Hat 列表发布内容，而不会接收这些列表的邮件。

那么，如何订阅呢？上述每个列表都有订阅地址。该地址是在列表名称后面加上 `-request` 构成的。例如，对于 `redhat-list`，你应该向 `redhat-list-request@redhat.com` 发送订阅或取消订阅请求。对于 `rpm` 列表，你将使用 `rpm-list-request@redhat.com`。你只需要在邮件主题行中写 `subscribe` 即可订阅，在主题行中写 `unsubscribe` 即可取消订阅。正文可以留空。

# 注意

要从 `redhat-digest` 取消订阅，请将你的请求发送到 `redhat-digest-request@redhat.com`，而不是 `redhat-list-request`。

# 其他新闻组

其他新闻组需要新闻阅读器才能阅读。大多数目前的浏览器都提供了某种新闻阅读器。目前大约有一万到两万个新闻组。以下是一些 Linux 用户感兴趣的组列表：

- `alt.os.caldera`
- `alt.fido.linux`
- `comp.os.linux.announce`
- `comp.os.linux.development.apps`
- `comp.os.linux.hardware`
- `comp.os.linux.misc`
- `comp.os.linux.setup`
- `linux.act.680x0`
- `linux.act.apps`
- `linux.act.chaos_digest`
- `linux.act.configs`
- `linux.act.debian`
- `linux.act.doc`
- `linux.act.fsf`
- `linux.act.fsstnd`
- `linux.act.ibcs2`
- `linux.act.kernel`
- `linux.act.linuxnews`
- `linux.act.mca`
- `linux.act.mumail`
- `linux.act.normal`
- `linux.act.hams`
- `linux.act.japanese`
- `linux.act.linuxbsd`
- `linux.act.lugnuts`
- `linux.act.msdos`
- `linux.act.new-channels`
- `linux.act.oastr-linux`
- `linux.act.pkg`
- `linux.act.ppp`
- `alt.os.linux`
- `alt.uu.comp.os.linux.questions`
- `comp.os.linux.advocacy`
- `comp.os.linux.answers`
- `comp.os.linux.development.systems`
- `comp.os.linux.m68k`
- `comp.os.linux.networking`
- `comp.os.linux.x`
- `linux.act.admin`
- `linux.act.bbsdev`
- `linux.act.compression`
- `linux.act.c-programming`
- `linux.act.dec_alpha`
- `linux.act.findo`
- `linux.act.gcc`
- `linux.act.interviews`
- `linux.act.linux-bbs`
- `linux.act.localbus`
- `linux.act.mips`
- `linux.act.newbie`
- `linux.act.ftp`
- `linux.act.ibsc2`
- `linux.act.laptops`
- `linux.act.linuxss`
- `linux.act.mgr`
- `linux.act.net`
- `linux.act.nys`
- `linux.act.oi`
- `linux.act.postgres`
- `linux.act.promotion`
- `linux.act.qag`
- `linux.admin.isp`
- `linux.act.serial`
- `linux.act.scsi`
- `linux.act.sound`
- `linux.act.seyon`
- `linux.act.sysvpkg-project`
- `linux.act.svgalib`
- `linux.act.term`
- `linux.act.tape`
- `linux.act.userfs`
- `linux.act.ktools`
- `linux.act.wabi`
- `linux.act.uucp`
- `linux.act.x11`
- `linux.act.word`

上述列表仅包含处理 Linux 的实际新闻组的三分之一。其他大多数组与列出的相似。最好的办法可能是扫描你所权限的 Linux 新闻组。

除了新闻组之外，还有无数致力于 Linux（特别是红帽 Red Hat）的 Web 页面。当我在 WebCrawler (`www.webcrawler.com`) 上搜索 Linux 时，返回了 9107 份文档；而在 Linux And Redhat 上搜索时，返回了 294 份文档。考虑到有这么多选择以及 Web 的易变性，如果我指出并简要描述几个我认为会持续一段时间的 Web 资源，可能会有所帮助。

第一个是显而易见的，即红帽的主页。它位于 `http://www.redhat.com`。当然，这里是查找任何关于红帽 Linux 信息的首选之地。
