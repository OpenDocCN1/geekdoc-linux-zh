
阅读，然后按 Q 键退出阅读。您可以在第 5 章“Ubuntu 初步使用”中了解更多关于使用命令行 的信息。

许多软件包还包含单独的文档，称为 HOWTO，其中包含有关特定主题或软件的信息。

如果 HOWTO 文档是压缩形式的简单文本文件（文件名以 .gz 结尾），您可以使用 zless 命令轻松阅读该文档，zless 是一个文本分页器，可让您在文档中前后滚动。（使用 less 命令阅读纯文本文件。）您可以使用 less 启动该命令，后跟完整的目录规范和文件名，或路径名，如下所示：

```
$ less /usr/share/doc/httpd-2.0.50/README
```

要阅读此文件的压缩版本，请以相同的方式使用 zless 命令：

```
$ zless /usr/share/doc/attr-2.4.1/CHANGES.gz
```

按 Enter 后，您可以使用光标键滚动浏览文档。按 Q 键退出。

如果 HOWTO 文档采用 HTML 格式，您只需使用 Firefox 等网页浏览器阅读信息即可。或者如果您从控制台阅读，可以使用 links 或 lynx 文本专用网页浏览器，如下所示：

```
$ links /usr/share/doc/stunnel-4.0.5/stunnel.html
```

links 浏览器提供下拉菜单，可通过点击屏幕顶部访问。您也可以按 Q 键退出。

如果文档采用 PostScript 格式（文件名以 .ps 结尾），您可以使用 gv 客户端阅读或查看文档，如下所示：

```
$ gv /usr/share/doc/iproute-2.4.7/ip-crefs.ps
```

最后，如果您想阅读便携式文档格式的文档（文件名以 .pdf 结尾），请使用 evince 客户端，如下所示：

```
$ evince /usr/share/doc/xfig/xfig-howto.pdf
```

## NOTE

本书使用标准桌面 CD 开发和编写。您可以使用随书附带的磁盘进行安装，或下载自己的副本，可作为 ISO9660 映像（文件名以 .iso 结尾）提供，并将其刻录到 700MB CD-R 或 DVD 上。您也可以直接从 Ubuntu 在 http://shipit.ubuntu.com 上订购预压 CD。

除了完整发行版之外，您还将获得对 Linux 内核的完整源代码以及发行版中所有软件的源代码的访问权限——超过 5500 万行 C 代码和近 500 万行 C++ 代码。浏览 http://www.ubuntu.com/download/ 开始使用。

## Ubuntu Developers and Documentation

如果您有兴趣帮助 Ubuntu，您可以通过测试 beta 版本（也称为预览版本，通常以发行版名称选择的动物命名）、编写文档以及为核心或贡献软件仓库贡献软件来协助工作。您应该具有安装 Linux 发行版的经验，渴望帮助将文档翻译成不同语言，或能够使用各种软件项目管理系统，例如 CVS。

邮件列表也可用作讨论 Ubuntu 的出口或论坛。列表已分类。例如，Ubuntu 的普通用户在 ubuntu-users 邮件列表上讨论问题。Beta 测试人员和开发人员通过 ubuntu-devel，而文档贡献者通过 ubuntu-doc 邮件列表。您可以通过在 http://lists.ubuntu.com/mailman/listinfo/ 选择感兴趣的列表来订阅邮件列表。请注意，其中一些邮件列表每天有超过 200 到 300 封电子邮件！

## Reference

本书的每一章都包括一个“Reference”部分，其中列出了文本中涵盖的附加或相关信息的链接。您可以使用这些链接了解更多关于 Ubuntu、Linux 和相关技术的信息。您也可以使用“Reference”部分的材料构建自定义书签集，以便在浏览或研究有关 Linux 的更多信息时使用。

- http://www-1.ibm.com/linux/—IBM 有关其 Linux 硬件、软件和服务工作及提供的 信息。
- http://www.dwheeler.com/sloc—David A. Wheeler 的精彩白皮书，涵盖 GNU/Linux 的当前状态、其规模、价值、组件和市场渗透率。
- http://www.ubuntu.com/—Ubuntu 的主页，由 Canonical Software 赞助，是了解更多关于 Ubuntu 的起点。
- http://help.ubuntu.com/md/ 网页，提供指向当前 Ubuntu 文档和发行说明的链接。
- http://www.tldp.org/—通往最新通用 Linux FAQ、指南和 HOWTO 文档更新的权威起点。

