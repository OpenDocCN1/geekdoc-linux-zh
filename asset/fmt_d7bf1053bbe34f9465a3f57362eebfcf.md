
$ mkdir `$HOME/doct`

$ cd `$HOME/doct`

## 528 第四部分 ♦ 运行应用程序

- 2. 打开一个文本编辑器来编写你的 DocBook 文档。例如，你可以输入：

```bash
$ edit cardoc.sgml
```

使用像 `jedit` 这样的文本编辑器，你可以在 `www.jedit.org` 获取，对于处理 DocBook 中使用的长标签名非常有帮助。

- 3. 输入你希望出现在文档中的标签和文本。大多数 DocBook 文档要么是 `<book>` 类型（大型多部分文档），要么是 `<article>` 类型（单章节文档）。要尝试 DocBook 文档，请输入以下内容：

```xml
<xml version="1.0">
<article>
  <title>选择一台新车</title>
  <header>
    <abstract>
      在文中，你将学习如何对汽车进行定价、议价和购买。
    </abstract>
  </header>
  <section>
    <title>开始入门</title>
    <para>
      你将学习的第一点是确定你的预算范围。
    </para>
  </section>
  <section>
    <title>下一步</title>
    <para>
      在了解自己的承受能力后，你就可以开始搜索了。
    </para>
  </section>
</article>
```

你应该注意此文档的几点：整个文档被包裹在 `<article> </article>` 标签中。文章标题位于 `<title></title>` 标签内。`<section> </section>` 标签表示文本章节，每个章节都包含一个标题和一个段落。这些章节稍后可以在目录（TOC）中被单独处理。

- 4. 保存文件并退出文本编辑器。

- 5. 现在，你可以将刚刚创建的文档转换为多种格式。例如，要创建 HTML 输出，你可以输入：

```bash
$ db2html cardoc.sgml
```

## 第 20 章 ✨ 处理文字与图像 529

结果是一个名为 `carddoc` 的新目录。在 `carddoc` 目录中运行 `db2html` 的结果是了 `stylesheet-images` 目录、一个 `t2.html` 文件和一个 `xl2.html` 文件。

要查看刚刚创建的 HTML 文件，我输入了：

```bash
$ epiphany `$HOME/doctest/cardoc/t2.html`
```

图 20-11 显示了 `db2html` 命令创建输出示例。左侧屏幕显示第一页。点击页面顶部的“Next”（下一页）链接，右侧是第二页。在转换为 HTML 的过程中，`db2html` 命令为每页添加了“Next/Previous”（下一页/上一页）按钮。还将每个章节的标题放在第一页的目录以及浏览器标题中。

![](img/23f52a815d30c05fbbf68ff8ce6d21ac_559_0.png)

**图 20-11：** 使用 `db2html` 命令将 DocBook 文件输出为 HTML。

从现在起，你可以继续添加内容和不同类型的标签。如果你正在为特定项目（如之前提到的 Linux 项目）编写文档，你应该获取有关特定标签以及可能遇到的其他样式问题的信息。

## 转换 DocBook 文档

之前的示例演示了如何创建一个简单的 DocBook 文档并将其转换为 HTML 输出。以下工具可以将 DocBook 转换为其他格式：

| 工具 | 将 DocBook 文件转换为 |
|---|---|
| docbook2dvi | 设备无关文件格式 |
| docbook2html | HTML 格式 |
| docbook2man | 页面格式 |
| docbook2pdf | 即可携式文档格式 (PDF) |
| docbook2ps | PostScript 格式 |
| docbook2rtf | 富文本格式 (RTF) |
| docbook2tex | Tex 格式 |
| docbook2texti | GNU TeInfo 格式 |
| docbook2txt | 纯文本格式 |

## 在 Linux 中打印文档

大多数 Linux 系统的打印功能由通用 UNIX 打印系统（CUPS）服务提供。作为非管理员用户，你对打印机的配置没有太大控制权。不过，你可以检查哪些打印机是可用的。

## 第 20 章 ✦ 文本与图像的处理 533

当命令返回 `lpc>` 提示符时，输入单词 `status:`：

```
lpc> status
hp:
printer is on device 'lpd' speed -1
queueing is enabled
printing is enabled
no entries
lpc>
```

此示例显示了打印机 `hp:` 的状态：队列和打印功能已启用，打印机未显示问题，且没有等待的打印作业。要退出 `lpc` 命令，请在 `lpc>` 提示符处输入 `exit`。

## 使用 Ghostscript 和 Acrobat 显示文档

如果你每次想更改文档内容或格式时都向打印机发送 Groff 或 LaTeX 文档，那么文档出版可能会非常耗纸。为了节省纸张和往返时间，可以使用打印预览在屏幕上显示文档及其在打印页面上的显示效果。接下来的章节描述了用于显示 PostScript 文件的 `ghostscript` 命令以及用于显示便携文档格式 (PDF) 文件的 Adobe Reader。

## 使用 ghostscript 和 gg 命令

在 Linux 中显示 PostScript 或 PDF 文档，你可以使用 `ghostscript` 命令。这是一个相当粗糙的界面，旨在让你逐页查看文档并一次解释一个。

你可以显示计算机上拥有的任何 PS 或 PDF 文件。例如，如果安装了 `samba` 软件包（否则，你可以找到自己的 PDF 文件进行尝试）：

```
$ ghostscript /usr/share/doc/samba/Samba-HOWTO-Collection.pdf
>>showpage, press <return> to continue<<
```

在提示符处，按 Enter 键（或 Return 键）逐页查看文件。当你到达文档末尾时，可以输入另一个 PostScript 或 PDF 文件的名称并逐页查看该文件。完成后，输入 `quit`。

534 第四部分 ♦ 运行应用程序

```
$ ggv /usr/share/doc/bash-doc-*/bashref.ps
```

当 `ghostview` 窗口打开时时，你可以看到文档。在页面上左键点击并上下移动鼠标来滚动文档。你可以使用 Page Up（上页）和 Page Keys（翻页键）来翻阅文档。你可以点击左列中的页码跳转到特定页面，或点击“全部打印”（Print All）按钮打印整个文档。

## 使用 Adobe Acrobat Reader

便携文档格式 (PDF) 提供了一种以打印显示形式存储文档的方法。通过 Adobe Acrobat Reader，你可以以非常友好的方式查看 PDF 文件。Adobe Acrobat 让你在 PDF 文件内部移动变得非常简单。PDF 文件可能包含超链接、目录、图形和各种字体。

你可以从 Adobe 网站（`www.adobe.com/products/acrobat/readstep2.html`）获取 Linux 版 Adobe Acrobat Reader。在该网站上选择 Linux 作为平台。Guru Labs（`www.gurulabs.com/downloads.html`）提供了适用于 Fedora 的 RPM 格式的最新版本 Adobe Acrobat Reader。

安装 Adobe Acrobat Reader 后，输入以下命令启动程序：

```
$ accroad
```
