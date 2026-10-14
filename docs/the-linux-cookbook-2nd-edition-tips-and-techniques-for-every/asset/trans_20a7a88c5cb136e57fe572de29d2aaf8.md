
# 16.1.1 选择 X 字体名称

X 字体名称可能很长且难以输入；为了方便起见，请使用 `xfontsel` 客户端，这是一个用于挑选 X 字体并获取其 X 字体名称的交互式工具。

启动 `xfontsel` 后，其外观如图 16-1 所示（窗口边框会因窗口管理器不同而有所差异）。

![](img/be7f02611e5cefde1a18c788fede22f7_430_0.png)

*图 16-1：启动 xfontsel。*

那一排按钮是下拉菜单，包含系统中 X 字体名称每个字段可用的选项。使用鼠标从每个菜单中选择项目，所选中的 X 字体就会显示在主窗口中。其上方显示它的 X 字体名称。

⇒ 若要将该 X 字体名称设为 X 选择内容，请点击标记为 `select` 的按钮。

此示例将 X 字体名称设为 X 选择内容，从而允许你将其粘贴到命令行或另一个窗口中（见第 254 页的技巧 10.3.2 [粘贴文本]）。

## 16.1.2 列出可用的 X 字体

使用 `xlsfonts` 列出系统中可用的 X 字体族、字号和字重。将带引号的模式作为参数传入，它就会输出系统中所有与该模式匹配的已安装 X 字体的名称；默认情况下，它会列出所有字体。

⇒ 以下是一些使用方法。

- 要列出系统上的所有 X 字体，请键入：
  
  `$ xlsfonts` ↵

- 要列出系统上名称包含文本“rea”的所有 X 字体，请键入：
  $ xlsfonts '*rea*' RET
- 要列出系统上所有粗体 X 字体，请键入：
  $ xlsfonts '*bold*' RET

注意：此方法不用于显示字体中的字符；如需显示字符，请使用下一节所述的 xfd。此外，若要浏览可用的 X 字体，可以使用上一节中的 xfontsel。

## 16.1.3 显示 X 字体中的字符

使用 xfd（“X 字体显示”）工具可以显示指定 X 字体中的所有字符。将要显示的 X 字体名称用引号括起来，作为 -fn 选项的参数。

⇒ 要显示中等粗细的 Courier X 字体中的字符，请键入：
$ xfd -fn '-*-courier-medium-r-normal-*-100-*-*-*-*-iso8859-1' RET

## 16.1.4 调整 Xterm 字体大小

关于为 X 客户端窗口指定字体的信息，请参见第 104 页的技巧 4.2.3 [指定 X 窗口字体]。最有必要为其指定字体的工具之一是 xterm，它通常用于在 X 中运行 shell；许多人喜欢为这个窗口指定所用字体（见第 109 页的技巧 4.5 [在 X 中获取终端窗口]）。

要在 xterm 运行时调整当前字体大小，请按住 CTRL 并在 xterm 窗口中的任意位置单击鼠标右键。此时会出现一个菜单，提供从 Unreadable（无法阅读）、Tiny（极小）到 Huge（巨大）的大小选项。若要将字体恢复为原始大小，请选择 Default（默认）。

## 16.2 使用 TeX 字体

以下技巧专门针对 TeX 字体。

## 16.2.1 列出可用的 TeX 字体

新 TeX 用户常问的一个问题是如何列出系统上安装的所有 TeX 字体——大多数安装都带有大量字体，如果能轻松列出并显示它们会大有帮助。遗憾的是，没有一种统一且万无一失的方法可以做到这一点。TeX 可以使用多种类型的字体，而实际安装的字体又会因系统而异。TeX 字体通常存储在 /usr/share/texmf/fonts/ 和 /usr/local/share/texmf/fonts/ 目录树中。

要获取系统上的 TeX 字体列表，可使用 locate 命令列出扩展名为 .tfm 的文件。这些是 TeX 字体度量文件。并非所有 TeX 字体都有 .tfm 文件，也并非所有 .tfm 文件都是可用的字体，但通过这种方法，你可以大致了解系统上安装了哪些 TeX 字体。

⇒ 要列出系统上可用的 .tfm 字体，请键入：

```
$ locate .tfm RET
```

注意：你可能希望将输出重定向到文件中，或者在单独的终端窗口中使用 less 仔细阅读，同时使用此输出来显示下一节所述的字体样例。

## 16.2.2 查看 TeX 字体样例

TeX 自带的文件 /usr/share/texmf/tex/plain/base/testfont.tex 是一个特殊的 TeX 文件，可用于显示任意 .tfm 字体的样例。

处理此文件时，它会要求输入要显示的字体名称。请给出基本文件名——即省略其路径和扩展名。然后单独成行输入 \sample 和 \end，这两个 TeX 命令会先打印样例，然后结束 TeX 文件。该命令会在当前目录中创建一个名为 testfont.dvi 的 DVI 文件，其中包含指定字体字符集的样例。

⇒ 要查看 plu10 字体的样例，请键入：

```
$ tex /usr/share/texmf/tex/plain/base/testfont.tex RET
This is TeX, Version 3.14159 (Web2C 7.3.1)
(/usr/share/texmf/tex/plain/base/testfont.tex
Name of the font to test = plu10 RET
Now type a test command (\help for help):)
* \sample RET
[1]
* \bye RET
[2]
Output written on testfont.dvi (2 pages, 12344 bytes).
Transcript written on testfont.log.
$ xdvi testfont.dvi RET
```
