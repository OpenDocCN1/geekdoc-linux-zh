
<title>入门</title>

<para>

你将学到的第一点是确定你的预算承受范围。

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
你应该注意关于此文档的几点。整个文档被包裹在文章 `<article> </article>` 标签中。文章标题位于 `<title></title>` 标签中。`<section> </section>` 标签表示每个都有独立标题和段落的文本章节。这些章节稍后可以在目录（TOC）中单独处理。

4. 保存并退出编辑器。
5. 接下来，你可以将刚刚创建的文档转换为几种不同的格式。
例如，要创建 HTML 输出，你可以输入：
结果是一个名为 `cardoc` 的新目录。该目录包含了 `stylesheet-images` 目录、一个 `t1.html` 文件和一个 `x8.html` 文件。（运行 `db2html` 程序时，你会看到很多看起来很吓人的错误信息。目前你可以忽略它们，`cardoc.xml` 文档应该包含对 DocBook DTD 的引用）。

```bash
$ db2html cardoc.xml
```

为了查看创建的 HTML 文件，我输入了：

```bash
$ epiphany $HOME/doctype/cardoc/t1.html
```

图 21.11 显示了由 `db2html` 命令创建的输出示例。左侧屏幕显示第一次点击。点击 Next 链接进入页面。右侧显示为你看到的第二个页面。在转换为 HTML 的过程中，`db2html` 命令会在页面中添加“Next!”。

# 第四部分

# 运行应用程序

运行此命令可能需要输入 root 密码或以 root 身份登录。你也可以通过直接在 `lpr` 命令行中添加作业号来移除特定打印机（`-Pprinter`）或特定作业号的队列打印任务。

## 检查打印机状态

有时打印机没有输出任何内容，而你不知道为什么。`lpc` 是一个打印机状态命令，可以为你提供有关打印机运行情况的线索。它是为管理员设计的，因此可能不在你的默认 PATH 中。要启动 `lpc` 命令，请输入以下内容：

```
# /usr/sbin/lpc
```

当命令返回 `lpc>` 提示符时，输入单词 `status`（状态）。

```
lpc> status
hp:
    printer is on device 'lpd' speed -1
    queuing is enabled
    printing is enabled
    no entries
    daemon present
lpc>
```

此此示例显示了打印机 `hp` 的状态：队列和打印已启用，打印机未显示问题，且没有等待的打印任务。要退出 `lpc` 命令，在 `lpc>` 提示符处输入 `exit`（退出）。

## 使用 ghostscript 和 Acrobat 显示文档

如果你每次想更改文档内容或格式时都将 Ghost 或 LaTeX 文档发送到打印机，那么文档发布可能会非常耗纸。为了节省纸张和往返时间，请使用打印预览程序在屏幕上显示文档，正如在打印页面上显示一样。以下章节描述了用于显示 PostScript 文件的 `ghostscript` 命令以及用于显示便携文档格式（PDF）文件的 Adobe Acrobat Reader。

## 使用 ghostscript 和 gg 命令

在 Linux 中显示 PostScript 或 PDF 文档，你可以使用 `ghostscript` 命令。这是一个相当粗糙的界面，旨在让你逐页查看文档并逐行解释它们。

你可以显示电脑上拥有的任何 PS 或 PDF 文件。例如，如果安装了 `samba` 软件包，你可以输入以下内容来显示 PDF 文件（否则，你可以找到自己的 PDF 文件并输入路径）：

```
$ ghostscript -DEVICE=... /usr/share/doc/samba-*/docs/Samba-HOWTO-Collection.pdf slideshow, press <return> to continue<<
```

在提示符处，按 Enter（或 Return）键逐页翻阅文件。当你到达文档末尾时，可以输入另一个 PostScript 或 PDF 文件的名称并翻阅该文件。完成后，输入 `quit`（退出）。

如果 `ghostscript` 检测到 PostScript 或 PDF 文件存在问题，你可能会看到警告或错误消息。在大多数情况下，如果你可以看到文档内容，可以忽略这些消息。

`ggv` (GNOME ghostview) 是另一种更友好的查看 PostScript 文件的方法。要使用 `ggv` 打开名为 `rbash.doc` 的文件，请输入以下内容：

```
$ ggv /usr/share/doc/bash-doc-*/bashref.ps
```
