

## man: 阅读手册页

man title 会格式化特定的手册页并通过 more、less 或您在 PAGER 环境变量中指定的程序将其发送到您的终端。title 通常是一个命令、设备、文件名或库例程的名称。手册的各节按大致的数字顺序进行搜索，尽管描述命令的各节（第 1、8 和 6 节）通常会优先搜索。

形式为 man section title 可以让您从特定章节获取手册页。因此，在大多数系统上，man sync 会为您提供 sync 命令的手册页，而 man 2 sync 会为您提供 sync 系统调用的手册页。

在 Solaris 下，您必须用 -s 标志前缀章节号，例如，man -s 2 sync。

man -k keyword 或 apropos keyword 会打印出在单行摘要中包含 keyword 的手册页列表。例如：

```
$ man -k translate
objcopy (1)      - copy and translate object files
dcgettext (3)     - translate message
tr (1)            - translate or delete characters
snmptranslate (1) - translate SNMP OID values into more useful information
tr (1p)           - translate characters
...
```

关键字数据库可能会过时。如果您向系统添加了额外的手册页，您可能需要使用 mandb（Ubuntu、SUSE）、makewhatis（Red Hat）或 catman -w（Solaris、HP-UX、AIX）重建此文件。

### 手册页的存储

用于手册页的 nroff 输入通常保存在 /usr/share/man 下的目录中。Linux 系统使用 gzip 对其进行压缩以节省空间。（man 命令知道如何在运行时解压缩它们。）man 命令会在 /var/cache/man 或 /usr/share/man 中维护已格式化的页面的缓存，前提是相应的目录可写，但这是一个安全风险。大多数系统在安装时一次性预格式化手册页（参见 catman）或根本不格式化。

Solaris 除了传统的 nroff 之外，还理解使用 SGML 格式化的手册页。SGML 页面在其自己的位于 /usr/share/man 下的章节目录中。

man 命令可以搜索多个手册页存储库以查找您请求的手册页。在 Linux 系统上，您可以使用 manpath 命令查找当前默认搜索路径。此路径（来自 Ubuntu）是典型的：

```
ubuntu$ manpath
/usr/local/man:/usr/local/share/man:/usr/share/man
```

如果需要，您可以设置 MANPATH 环境变量以覆盖默认路径：

```sh
export MANPATH=/home/share/localman:/usr/share/man
```

一些系统允许您为手册页设置自定义系统范围的默认搜索路径，如果您需要维护由 OpenPKG 等生成的并行手册页树，这会很有用。但是，如果您想以手册页的形式分发本地文档，使用系统的标准打包机制并将手册页放在标准手册目录中会更简单。有关更多详细信息，请参阅第 12 章，*软件安装与管理*。

### GNU Texinfo

Linux 系统包含一种称为 Texinfo 的补充在线手册页系统。它很久以前由 GNU 团队发明，是对格式化手册页的 *nroff* 命令是 AT&T 专有的这一事实的反应。如今我们有 GNU 自己的 *groff* 来完成这项工作，*nroff* 问题已不再重要，但 Texinfo 仍然像僵尸一样在寻找人类大脑一样蹒跚前行。

尽管使用 Texinfo 似乎在逐渐减少，但仍有一些 GNU 软件包坚持使用 Texinfo 文件而不是手册页来记录自己。您可以将 Texinfo 阅读器 *info* 的输出通过管道传输到 *less*，以规避 *info* 的内置导航系统。

幸运的是，使用 Texinfo 记录的软件包通常会安装手册页存根，告诉您使用 *info* 命令阅读有关这些特定软件包的信息。您可以安全地坚持使用 *man* 命令进行手册搜索，只有在被指示时才深入 *info* 领域。*info info* 会让您入门 Texinfo 的黑暗奥秘。

## 1.10 其他权威文档

手册页只是官方文档的一小部分。不幸的是，其余大部分文档散布在网络上。

### 系统特定指南

主要厂商都有自己的专用文档项目，并且许多厂商继续生产有用的书长手册。如今，手册通常在线找到，而不是印刷书籍的形式。文档的范围和质量差异很大，但大多数厂商至少会提供一份管理指南和一份安装指南。表 1.4 显示了我们示例系统的查找位置。

![](img/14d78e3cecac4581d37024baf1e94cca_66_0.png)

在这群人中脱颖而出的是 IBM，它制作了大量关于各种管理主题的完整书籍。您可以将其作为书籍购买，但也可以免费下载。IBM 完整性的缺点是，许多文档似乎落后于 AIX 当前版本一两个版本。

