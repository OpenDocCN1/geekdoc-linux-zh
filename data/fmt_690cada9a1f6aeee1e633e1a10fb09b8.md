
9. 你的机器上安装了声卡，你想配置它。但你忘记了命令。输入 `apropos sound` 来查找该命令。命令是什么？

```
ls-a
```

```
man-k
```

```
sndconfig
```

## 主题 B：在线获取帮助

### 解释

可以在很多地方找到帮助。本节将向你介绍其中几个。

### Linux 文档项目 (Linux Documentation Project)

可以在 `www.tldp.org` 找到 Linux 文档项目。它提供了丰富的 Linux 文档链接。根据信息的呈现方式，信息分为若干类：

| 类别 | 说明 |
|------|---|
| Guides (指南) | 关于各种 Linux 主题的长篇、深度在线书籍。 |
| HOWTOs | 关于配置或使用 Linux 的主题。 |
| FAQs (常见问题) | 关于各种 Linux 主题的常见问题解答。 |
| man pages (帮助页) | 许多 Linux 应用和程序的手册页的 HTML 版本。 |

### HOWTOs 和 Mini-HOWTOs

Linux HOWTOs 和 mini-HOWTOs 是如何使用特定程序执行特定任务的详细描述。通常，mini-HOWTOs 比普通的 HOWTOs 短。这些文档有多种格式，包括纯文本、HTML、PDF、PostScript 和 SGML。在 LDP 网站上，HOWTOs 按类别和字母顺序组织。

### Guides (指南)

指南比 HOWTOs 更具深度。由于指南可能长达数百页，因此它们也被称为书籍。指南涵盖了 Linux 安装、内核、网络管理和安全等主题。

### FAQs (常见问题)

FAQs 是带有答案的常见问题。FAQs 试图回答关于特定主题的一些最常见问题。在 LDP 网站上，FAQs 的链接有纯文本、HTML 和 PostScript 格式。

### 其他网站

主要的 Linux 网站是 `www.kernel.org`。你可以在这里找到最新的内核发布。互联网上还有许多网站。本节将向你介绍其中几个。

| 网站 | 类型 | same |
| --- | --- | --- |
| `www.kernel.org.uk` | 新闻 | 包含内核维护者 Alan Cox 的新闻和日记。 |
| `www.linxtoday.com` | 新闻 | 通用 Linux 新闻。 |
| `www.linux.org` | 新闻 | Linux Online！通用新闻和教程。 |
| `www.slashdot.org` | 新闻 | “给极客的新闻”——Linux 及其他新闻。 |
| `www.freshmeat.net` | 软件 | 最大的开源 Linux 软件项目索引，满足你的工作或娱乐需求。 |
| `www.google.com` | 搜索 | 运行在 Linux 上的大型且准确的搜索引擎。你可以访问 `www.google.com/linux` 获取 Linux 特定的结果。 |
| `alt.os.linux` | 新闻组 | 使用新闻阅读器或通过 `http://groups.google.com` (原 Dejanews) 访问。也存在额外的子分类。 |

## B-1: 在线帮助

### 问答

- 1 你可以在 `www.tldp.org` 找到什么信息？

HOWTOs、Guides、FAQs 和 man pages

- 2 HOWTO 和 Guide 之间有什么区别？

指南更长且更深入。

- 3 你正在寻找一个可以在 Linux 上运行并执行特定功能的开源程序。哪个网站可能会列出你可以尝试的软件列表？

`www.freshmeat.net`

## 单元总结：获取帮助

### 主题 A

在这个主题中，你学习了如何在 Linux 内部查找帮助。你接触了 `man` 帮助页和 `info` 帮助页。你还发现了如何在 GUI 中访问信息。

### 主题 B

这个主题为你在互联网上搜索 Linux 信息提供了一些起点。列出的网站提供了 `内核` 版本信息、Linux `新闻` 和 Linux `软件` 发布。你还被引向了一个名为 `Linux 文档项目 (The Linux Documentation Project)` 的大型信息库。

## 独立练习活动

- 1 用户命令列在哪个手册页章节中？

*第 1 *

- 2 你想知道某个命令在哪个手册页章节。你可以使用什么命令查找此信息？

*`man -k command`, `whatis command`; 或 `apropos command`*

- 3 手册页 (man pages) 和 info 页之间的三个区别是什么？

*info 页不那么完整——并非所有命令都有 info 页；info 页使用分级格式；info 页通常更有帮助*

- 4 你想查看某个命令使用的参数，但你不想阅读手册页或 info 页。你如何获取这些信息？

*`command --help`*

- 5 在提示符处输入 `help` 会发生什么？

*出现一个可用的内置 bash 命令列表。*

- 6 如何在提示符处启动 `help`？

*出现一个可用的内置 bash 命令列表。*

# SAIR Linux GNU 安装与配置

这次在上述目录使用 `-a` 标志执行 `ls` 命令，产生如下输出：

```bash
$ls -a             .emacs          gnome2_private  .metacity
            .esd_auth       .gnome-desktop  .nautilus
            archive.tar.gz .fonts.cache-l .gtkrc          .rhn-applet.conf
            .bash_logout    gconf           gtkrc-1.2-gnome2 scriptfile
            .bash_profile   gconfd           ICEAuthority   .Xauthority
            .bashrc         gnome           link-to-scriptfile .xsession-errors
            datafile        gnome2          .lsfile.swp
```

注意隐藏文件被列出了，目录看起来“充满”了很多。

在上述目录使用 `-l` 标志执行 `ls` 命令，输出如下：

```bash
$ls -l
total 0

-rw-rw--r--  1 student      student        0 Oct 27 19:48
archive.tar.gz
-rw-rw--r--  1 student      student        0 Oct 27 19:46
datafile     1 student      student        24 Oct 27 19:47 link-
to-scriptfile -> /home/student/scriptfile
-rw-r-x--  1 student      student        0 Oct 27 19:46
scriptfile
```

现在你看到了一些额外信息。

最右侧列显示目录条目的名称。

向左移动，下一个字段显示文件最后修改的日期和时间。日期左侧是文件大小（字节）。

接下来的两个字段显示与文件关联的所有者和组。此列表是用户 `student` 的家目录。

下一个字段显示文件的链接数。

最后，最左侧的字段是权限掩码。

## 文件和目录权限

在示例中，`datafile` 的所有者是 `student`，关联组是 `student`，文件权限为“rw-r--r--”。文件权限似乎是许多 Linux Linux 用户的困惑来源。它们其实非常简单。

`ls` 命令显示的文件权限实际上是一个二进制掩码。

最左侧（最左边的八进制数字）是“特殊”字段，稍后会描述。你在这里看到的两个有趣的符号是 `d` 或 `1`：`d` 表示该文件是一个目录；`1` 表示该文件是一个链接（指向文件的指针）。

接下来的三个八进制数字分别代表用户、组和“其他用户”的权限位。

### 基础系统导航

以上面的文件 `datafile` 为例，示例（`student`）拥有“rw-”，表示读取和写入但没有执行权限。组（`student`）拥有“r--”，表示只有读取，没有写入或执行权限。其他人拥有DW”，也表示只有读取，没有写入或执行权限。将掩码“rw-r--”转换为八进制数得到 0644（开头的 0 通常不显示，因此常见的表示法是 644.）。

使用 `chmod` 命令修改文件权限。`chmod` 命令有两种形式：使用数字参数作为权限掩码，以及使用字母参数作为权限掩码。如果你想更改文件 `datafile` 的权限允许所有人读取、写入和执行该文件（这通常是一个非常糟糕的主意），`chmod` 的数字形式为：

```bash
$ chmod 777 datafile
```
