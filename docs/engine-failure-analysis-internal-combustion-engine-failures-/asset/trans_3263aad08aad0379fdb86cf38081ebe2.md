

# 第 1 章

![](img/e85417bb52fc523c6fc7b3b77b124ecb_490_0.png)

# 编辑文本编辑器

本章提供了一份参考指南，介绍了 Linux 系统上最常见的文本编辑器中最广泛使用的功能，范围从 **joe** 和 **pico** 等简单易用的编辑器，到 **emacs** 和 **vi** 等高度复杂的编辑器，后者专为程序员设计。虽然 Linux 系统通常配置为使用 **emacs** 或 **vi** 作为默认编辑器，但你可能会更喜欢使用 **joe** 等更用户友好、更简单的编辑器来编辑简单的文本文件（例如配置文件）（参见本章中“指定默认编辑器”一节）。

请注意，本章讨论的一些文本编辑器提供许多用于高级用途的选项，包括脚本和编程，这些选项并未在此列出。此处包含的是旨在用于文本编辑应用程序的命令。有关这些高级命令的更多信息，请参阅该程序的文档。

> **提示** 本章描述的一些键盘快捷键需要用户在按住 Ctrl 键的同时再按下另外两个键。为了表示这种类型的快捷键，使用逗号来连接两个 Ctrl 键快捷键。例如，Ctrl + k, Ctrl + e 表示“按住 Ctrl 键，并在按住的同时依次按下 k 和 e。” 某些其他命令要求你输入一个 Ctrl 键快捷键，松开 Ctrl 键，然后输入第二个键。为了表示这种类型的快捷键，使用逗号来将一个 Ctrl 键快捷键与第二个键连接起来。例如，Ctrl + h, b 表示“按住 Ctrl 键，松开 Ctrl 键，输入第一个字母（在此情况下为 h），然后输入第二个字母（b）。” 本章讨论的键盘快捷键通常区分大小写；Ctrl + L 与 Ctrl + l 不同。

# 快速一览

| 如何操作 | 示例 |
| :--- | :--- |
| 检查拼写？ | emacs: Alt + $<br>joe: Ctrl + [ , n<br>pico: Ctrl + t |
| 关闭光标所在窗口？ | emacs: Ctrl + x, 0<br>vi: Ctrl + w, q |
| 创建一个新文件？ | emacs: Ctrl + x, Ctrl + f<br>joe: Ctrl + k, e<br>vi: :x |
| 删除一行？ | emacs: Ctrl + k<br>joe: Ctrl + j<br>pico: Ctrl + k<br>vi: dd |
| 标记一块文本？ | emacs: Ctrl + 空格键<br>joe: Ctrl + k, b<br>pico: Ctrl + ^ |
| 移动到文件开头？ | emacs: Home<br>pico: Ctrl + w, Ctrl + y 或 1G (1, shift 6) |
| 移动到文件末尾？ | emacs: End<br>pico: Ctrl + w, Ctrl + v |
| 打开一个文件？ | emacs: Ctrl + x, Ctrl + v<br>joe: Ctrl + k, e<br>pico: Ctrl + r<br>vi: :e |
| 退出编辑器？ | emacs: Ctrl + x, Ctrl + c<br>joe: Ctrl + k, X<br>pico: Ctrl + x<br>vi: :x 或 :q! |
| 在编辑更改后重新格式化文本？ | emacs: Alt + q<br>joe: Ctrl + r<br>pico: Ctrl + j |
| 保存一个文件？ | emacs: Ctrl + x, Ctrl + s<br>joe: Ctrl + k, d<br>pico: Ctrl + o<br>vi: :w |
| 向下滚动？ | **emacs:** PgDn<br>**joe:** PgDn<br>**pico:** Ctrl + n<br>**vi:** PgDn 或 j 或 向下箭头 |
| 向上滚动？ | **emacs:** PgUp<br>**joe:** PgUp<br>**pico:** Ctrl + p<br>**vi:** PgUp 或 k 或 向上箭头 |
| 搜索文本？ | **emacs:** Ctrl + s<br>**joe:** Ctrl + k, f<br>**pico:** Ctrl + #w<br>**vi:** /模式 |
| 在屏幕上查看程序的键盘快捷键？ | **emacs:** F1<br>**joe:** Ctrl + k, h<br>**pico:** Ctrl + g<br>**vi:** F1 |
| 将屏幕分为两个窗口？ | **emacs:** Ctrl + x, 3<br>**joe:** Ctrl + k, o<br>**vi:** :sp |
| 撤销编辑更改？ | **emacs:** Ctrl + _<br>**joe:** Ctrl + _<br>**vi:** u |

# 指定默认编辑器

要确定当前正在使用的默认编辑器，请输入 `echo $EDITOR` 并按回车键；如果有默认编辑器，你将看到其路径名。如果你希望更改默认编辑器，请执行以下操作：

1. 在你的主目录中，使用文本编辑器打开名为 `.bash_profile` 的文件。
2. 添加以下行：
   ```bash
   EDITOR=pathname
   export EDITOR
   ```
   在此语法中，`pathname` 是你想要使用的编辑器的路径名。例如，若要使用 Joe 作为默认编辑器，请输入以下内容：
   `EDITOR=/usr/bin/joe`
   假设 Joe 位于 /usr/bin/joe。要确定 Joe 的位置，请输入 `whereis joe` 并按回车键。

> **提示** 要使默认编辑器更改生效，请注销当前会话并重新登录。

# 字母顺序命令参考

本节讨论以下类型的编辑器：

- 面向程序员的完整功能编辑器 (emacs, vi)
- 易于用于更改文本文件的编辑器 (joe, pico)
- 面向流的自动文本文件处理编辑器 (sed)

# emacs

```bash
emacs [ option ] [ filename ]
```

在 X 终端窗口中，此命令启动 GNU Emacs 文本编辑器。在控制台上，它启动同一实用程序的文本模式版本。这两个实用程序使用相同的命令快捷键，在本节中进行了描述（要快速概览，请参阅“Emacs 基础知识”一节）。可选地，你可以通过指定文件名或使用空格分隔的文件名列表来打开一个或多个文件。

此处记录的是 GNU Emacs v. 20.3.1。有关更多信息和下载，请访问 [http://www.gnu.org](http://www.gnu.org)。如果你以前从未使用过 Emacs，请务必从精心制作的教程开始。要启动它，请按 Ctrl + h, t。

Emacs 是一个庞大且复杂的程序，具有许多用于专门目的的可选模块。因此，本节仅涵盖 Emacs 的基础知识。未涵盖的内容包括用于 *缩写*（可展开为较长字符串的用户定义代码）的命令、累积文本、ASCII 图片、二进制文件编辑、日历、日记、目录编辑、电子邮件、格式化（使用 Postscript、Tex 和 troff）、*帧*（在多个窗口中运行相同的 Emacs 会话）、缩进（用于编写程序）、基本（默认）模式以外的模式、*矩形* 以及 Usenet。请注意，Emacs 提供 X Window System 版本，该版本随大多数 Linux 版本分发，并允许你使用菜单命令来执行本节讨论的大多数（但并非所有）键盘命令。

> **提示** 如果你在文本模式下运行 Emacs（通过启动控制台或带有 **-nw** 选项的程序启动），你可能会发现 Backspace 或 Delete 键被映射到 Emacs 的帮助功能。要修复此问题，请在你的主目录中创建或修改一个名为 `.emacs` 的文件。向此文件添加以下行：
>
> ```lisp
> (keyboard-translate ?\C-h ?\C-?)
> (keyboard-translate ?\C-\\ ?\C-h)
> ```
>
> 进行此更改后，你需要按 Ctrl + \\（反斜杠）而不是 Ctrl + h 来访问各种帮助命令。

## 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `+n` | 打开文件后将光标定位到第 *n* 行 |
| `-bd *color*` | 将边框设置为指定颜色 |
| `-bg *color*` | 将背景设置为指定颜色 |
| `-b *n*` | 将边框宽度设置为指定的 *n* 个像素 |
| `-cr color` | 将文本光标设置为指定颜色 |
| `-d display name` | 在指定的显示名称上创建 Emacs 窗口 |
| `-fg color` | 将前景设置为指定颜色 |
| `-font font name` | 使用指定的字体名称作为默认字体 |
| `-geometry geometry` | 以指定的几何形状创建窗口 |
| `-i` | 当 Emacs 窗口最小化时使用特殊图标 |
| `-ib n` | 将内部边框宽度设置为指定的 *n* 个像素 |
| `-ms color` | 将鼠标光标设置为指定颜色 |
| `-name name` | 以指定的名称创建窗口 |
| `-nw` | 在 X 终端窗口中以文本模式运行 Emacs |
| `-q` | 跳过加载初始化文件 |
| `-r` | 以反转视频显示窗口 |
| `-t filename` | 使用指定的文件名作为终端设备，而不是标准终端 (tty) |
| `-u user` | 使用指定用户的初始化文件 |

## Emacs 基础知识

Emacs 命令映射到 Ctrl 和 Meta 键。在基于 Intel 的 Linux 系统上，Meta 键映射到 Alt 键，因此下表显示所有映射到 Meta 的键盘快捷键，但列出的为 Alt 键而非 Meta。如果你正在一台没有 Alt 键的计算机上使用 Linux，你可以按 Esc 键代替。例如，你可以按 Esc, q 来填充当前段落，而不是按 Alt + q。

你可以使用鼠标操作 Emacs。有关基本鼠标操作的更多信息，请参阅本节中的表格“使用鼠标操作 Emacs”。

