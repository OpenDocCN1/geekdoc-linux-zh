

# 70 · 第5 章

由于许可问题，Red Hat 发行版未包含 Adobe 本身提供了一个名为 Acrobat Reader 的免费 PDF 阅读器，可以在 Linux 上运行。要获取它，请将浏览器指向 https://www.adobe.com 并按照下载 Acrobat Reader 的说明操作。文件下载完成后，你需要执行以下命令进行安装（解压）：

```
tar -xzf linux-ar-405.tar.gz
```

这将创建一个名为 ILINXR.install 的目录，在其中你将找到一个名为 INSTGUID.TXT 的文档。如何阅读它留给读者练习（我们是这么说的），但这里有一个提示：这是一个文本文档。你需要以超级用户身份安装 Acrobat Reader，因此在开始安装之前，请务必使用该命令，输入 exit 返回到你的用户配置。

最后一种常见的文档格式是 Adobe PostScript 格式。你可能已经在打印机的语境下听过“PostScript”这个术语，因此可能对 PostScript 格式文件的概念感到困惑。实际上，PostScript 是一种为了渲染文档而创建的编程语言。支持 PostScript 的打印机能够执行呈现给它们的 PostScript 文件中的指令。按照惯，PostScript 文件以 .ps 扩展名结尾。在本章较早之前，你曾创建过帮助页的 PostScript 版本。执行以下命令查看后台发生了什么：

```
more man.ps
```

PostScript 渲染引擎通过第一行中的字符串 %PS-Adobe-x.x 来识别 PostScript 文件。“x”是文件中使用的语言版本。由于帮助页的 PostScript 版本在以原生格式查看时并不十分有趣，让我们看看它渲染后的样子。按 Q 键退出，然后执行此命令：

```
ghostview man.ps
```

ghostview 程序使用另一个程序 gs 来渲染 PostScript 或 PDF 文件，并将其结果显示在屏幕上。像 xpdf 一样，ghostview 提供了必需的导航图标，你可以通过这些图标翻页文档。要退出 ghostview，点击窗口右上角的 X。

# 本章总结

在成为 Linux 大师的道路上，必须掌握的基本技能之一是学习查找文档。由于 Linux 继承了悠久的历史，也带来了同样多的存储思想和指令的方法。基于文本的文档古老艺术随着 manpages、info 页面、PDF 文件和 HTML 的出现而得到了改进，但它从未被完全取代。

# 本章复

## 关键术语

| Gnome Help Browser | Linux Documentation Project | PDF |
|---|---|--|
| Ghostview | Lynx | Portable Document Format |
| HOWTO | Man | PostScript |
| HOWTO-INDEX | Manpage | Standard Generalized Markup |
| Is | Manpath | |
| LDP | Nodes | |

## 复习题

- 1. 帮助文本作者现在将 SGML 标签嵌入到文档中。SGML 是什么意思？
- 2. **is** 命令提供什么功能？
- 3. Manpages 每个都分为几个部分，标记为：Name（名称）、Synopsis（摘要）、Description（描述）、Options（选项）、Files（文件）、__________、Bugs（缺陷）和 Author（作者）。
- 4. info 格式如何区别于 manpage？
- 5. Lynx 是什么？

## 编程作业

### 练习 1：探索标准 Linux 文目录

- 1. 使用 **less** 命令查看 HOWTO-INDEX 文件。
- 2. 使用 **less** 命令查看各种 HOWTO 文件，例如 Apache 和 PostgreSQL 的文件。

### 练习 2：阅读 UNIX Manpages

- 1. 查看 **httpd** 命令的 manpage，并对其各个部分（“Synopsis”、“Description”、“Options”、“Files”和“See Also”）写一个简短的总结。
- 2. 查看 **man** 命令的 manpage，并对其部分写一个简短的总结。
- 3. 使用 manpage 搜索选项找到对单词 **dump** 的引用。
- 4. 使用 **info** 命令查找有关 info 格式的信息。利用其超链接功能，研究如何使用 **info** 并写一个描述性总结。

### 练习 3：使用 HTML 浏览器

- 1. 使用 Netscape 浏览适用于 PostgreSQL 的 HTML 文档。
- 2. 使用 Lynx 浏览器浏览 PostgreSQL 的 HTML 文档。

### 练习 4：探索 Linux 文档项目

- 1. 在 LDP 网站浏览 HOWTO 文档。
- 2. 在 LDP 网站浏览 FAQ（常见问题集）。
- 3. 阅读最新一期的 Linux Gazette，对最近的 Linux 新闻发表评论。

### 练习 5：理解文档转换

- 1. 将 httpd 命令的 manpage 转换为 PostScript 和 PDF 格式。
- 2. 使用 PostScript 阅读器打开生成的 PostScript 文件。
- 3. 在 PDF 阅读器中打开生成的 PDF 文件。

# Web 简介

尽管在 Web 之上构建之前，互联网已经存在了 10 多年。Tim Berners-Lee 在于欧洲核物理实验室（CERN）任职期间创建了 Web。CERN 是一个研究中心，来自各地的科学家在特殊机器中碰撞粒子并分析结果。这些科学家随后从这些粒子的反应中推导出复杂的理论。

（注：原文文本包含大量重复和断句句子，已根据逻辑流进行了清理处理。）

