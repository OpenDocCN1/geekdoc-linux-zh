
`cp /usr/share/man/man1/chown.1.gz /tmp`

`gunzip /tmp/chown.1.gz`

`groff -TAscii -man /tmp/chown.1 | less`

## 第 6 章 - 使用 Red Hat Linux 发布

为了排版格式化 man 页，可以使用 PostScript 或 HP LaserJet 输出。在这种情况下，你不希望将文档格式化到屏幕上。你应该将输出重定向到文件或打印机。这里有几个示例：

```
groff -Tps -man /tmp/chown.1 > /tmp/chown.ps
groff -TJ4 -man -1 /tmp/chown.1
```

第一个示例创建 PostScript 输出 (`-Tps`) 并将其重定向到名为 `/tmp/chown.ps` 的文件。该文件可以使用 PostScript 查看器（如 `ghostscript`）查看或发送到打印机 (`lpr /tmp/chown.ps`)。第二个示例创建 HP LaserJet 输出 (`-TJ4`) 并将其重定向到默认打印机 (`-l` 选项)。如果你的默认打印机是 PostScript 打印机，请使用 `-Tps`。

### 使用 Geoff 创建 man 页

在 HOW-TO 和 info 文件之前，man 页是 UNIX（以及类 UNIX）系统信息的字体。每个命令、文件格式、设备或其他组件都有自己的 man 页，或者与具有相似组件的项分组合在一个 man 页中。创建你自己的 man 页只需要学习几个宏（特别是 man 宏）。图 6-1 是一个名为 `payoff` 命令的虚拟 man 页源文件示例。

大多数 man 页存储在 `/usr/share/man` 的子目录下。在创建 man 页之前，请参考类似的 man 页以查看它们包含的标记和标题。`man1` 是命令；`man2` 包含系统调用；`man3` 有库函数；`man4` 有特殊设备文件 (`/dev/*`)；`man5` 是文件格式；`man6` 是游戏；`man7` 有杂组件，而 `man8` 是管理命令。

![](img/380d929a08ad0f9245d542259c5760b8_238_0.png)

www.unltded.com 额外内容

## 第二部分 使用 Red Hat Linux

![](img/380d929a08ad0f9245d542259c5760b8_239_0.png)

```
.waycol -I -the roff processor source for the waycol command
.TH waycol I "June 15, 1999" GNU "Linux Programmer's Manual"
.SH NAME
waycol I My cool command
.SH SYNOPSIS
waycol I [-Vfabc -VR] [/V file ... -VR]
.SH VERSION
waycol documents waycol version X.XX,
.SH DESCRIPTION
waycol VR is a cool command.
.SH OPTIONS
这个版本的 waycol VR 比上一个好。
.JP -a
使用它运行所有项，
.JP -b
运行时间选项，
.JP -c
运行一个或两个选项，
.JP -v
随命令打印版本，
.SH COMMAND
如果你不喜欢它，就不要告诉我，这会伤我的感情。
.SH ENVIRONMENT
waycol VR 使用环境变量：
.SH DISPLAY
这设置显示。
这包含 waycol 数据库的位置，
.SH FILES
/usr/waycol - 包含 waycol内容的目录，
.SH AUTHOR
Chris Craft (chris@history.com)
.SH SEE
我想告诉我的朋友。
```

图 6-1: 简单的标记使用包含组件描述信息的行创建。在开头，关于 GNU 许可证的信息被注释掉了。第一个是标题（使用 `.TH` 宏），包含了 man 页的标题、章节号、组件源（如发行版名称），以及标题。带有 `.SH` 宏的章节至少有 `NAME`、`SYNTAX` 和 `DESCRIPTION` 标题。man 页可能包含不同类型的信息，如环境变量、错误或文件。man 页还包含用于选项的缩进段落；例如，`\lB` 将当前字体改为粗体，`\lI` 将字体改为斜体，`\bR` 将其改回普通字体。图 6-2 显示了 waycol man 页通过以下命令格式化并发送到打印机后的样子：

```
groff -man -Tps -l waycol
```

## 第 6 章 - 使用 Red Hat Linux 发布

**表 6-1 列出了可以在 man 页上使用的宏（通常位于 `/usr/share/groff/tmac`）。它们在 `tmac` 文件中定义，并在 `man(7)` 手册中也有描述。**

| 宏 | 描述 | 宏 | 描述 |
| :--- | :--- | :--- | :--- |
| .B | 粗体 | .BI | 粗体，斜体（交替） |
| .BR | 粗体，罗马（交替） | .DT | 设置制表符 |
| .B | 开始悬挂缩进 | .I | 斜体 |
| .IB | 斜体，粗体（交替） | .IP | 开始悬挂。用于描述选项。使用长标签 |
| .IR | 斜体，罗马（交替） | .LP | 开始段落（同 .PP） |
| .PD | 设置段落间距 | .PP | 开始段落（同 .IP） |
| .RB | 罗马，粗体（交替） | .RE | 结束缩进（在 .RS 之后） |
| .RI | 罗马，斜体（交替） | .RS | 开始缩进（使用 .RE 结束缩进） |

**表 6-2: man 页格式化添加页眉并布局页面。**

| 宏 | 描述 | 宏 | 描述 |
| :--- | :--- | :--- | :--- |
| .B | 粗体 | .BI | 粗体，斜体（交替） |
| .BR | 粗体，罗马（交替） | .DT | 设置制表符 |
| .HP | 开始悬挂缩进 | .I | 斜体 |
| .IB | 斜体，粗体（交替） | .IP | 开始悬挂。用于描述选项。使用长标签 |
| .IR | 斜体，罗马（交替） | .LP | 开始段落（同 .PP） |
| .PD | 设置段落间距 | .PP | 开始段落（同 .IP） |
| .RB | 罗马，粗体（交替） | .RE | 结束缩进（在 .RS 之后） |
| .RI | 罗马，斜体（交替） | .RS | 开始缩进（使用 .RE 结束缩进） |

等等，页面显示是 209。

www.unltded.com 额外内容

创建信件、备忘录（与 Groff 的 `-mm` 选项一起使用）曾在早期 UNIX 用户中流行，用于制作技术文档、信件和备忘录。虽然带有各种 WYSIWYG 模板的更现代文字处理器让 mm 过时了，但在紧急情况下，mm 仍然是在文本环境中创建版风格文档的快速方法。

使用 mm 宏格式化并打印文档，请使用以下命令行（假设你的默认打印机是 PostScript 打印机）：

```
groff -mm -Tps -l letter.mm
```

以下是一个使用 mm 宏制作信件的简单示例：

```
.WA "Christopher T. Craft"
999 Anyway Way
Anytown, UT 84111 USA
.WE
.IA
John W. Doe
111 Notown Blvd.
Notown, UT 84111
.IE
.LO RN "Our telephone conversation"
.LO SA "Dear Mr. Doe"
.LT
参考我们 4 号的电话通话，我致电是为了确认我们即将在 18 号进行的约会。我期待讨论合并。我相信我们有一个双利赢的局面。
.FC "Yours Truly,
.SG
```

在这个示例中，使用了 `.WA`, `.IA`, `.LO`, `.LT`, `.FC` 和 `.SG` 宏。`.WA` 宏开始写件者的地址，`.WE` 结束地址。`.IA` 开始收件者的姓名和地址，`.IE` 结束收件者的地址。`.LO RN` 在信件中添加了“关于：”，后面跟了文本“我们的电话通话”。`.LO SA` 用于添加问候行。`.LT` 表示文档是信件格式。

在信件正文之后，`.FC` 指明使用的正式结束语。最后，`.SG` 将写件者的姓名作为签名行。如果你使用代码示例之前的段落中提到的 `groff` 命令行，该信件的输出如图 6-3 所示。

# 第 6 章 ♦ 在 Red Hat Linux 上发布 211

图 6-3：使用 mm 宏创建一个简单的备忘录。

mm 宏经常用于生成技术备忘录。这是一个签字页示例，可能会放在较大的技术备忘录首页。
