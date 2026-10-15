

## 使用 sed 进行全局更改

另一个方便的命令是 sed，它让你可以在不打开编辑器的情况下对文件进行多次更改。例如，作为一名新任 Web 管理员，你可能会使用 sed 将之前 Web 管理员的电子邮件地址的所有出现位置更改为你自己的地址。正如我们在本节中所示，你可以使用 sed 在文档内进行全局更改。

## 使用 sed 进行全局更改：

```
sed 's/oldaddr@raycomm.com/newaddr@raycomm.com/g' address.htm > address-new.htm
```

输入 sed，后跟

- ▲ 一个单引号 (')
- ▲ 一个开头的 "s"
- ▲ 一个斜杠 (/)
- ▲ 你想要替换的文本 (oldaddr@raycomm.com)
- ▲ 另一个斜杠 (/)
- ▲ 替换文本 (newaddr@raycomm.com)
- ▲ 另一个单引号 (')
- ▲ 另一个 /
- ▲ g，它告诉 sed 全局应用更改。（如果你省略 g，则每行只会更改第一次出现。）
- ▲ 应进行更改的文件名 (address.htm)

你可以将输出重定向到一个新文件名（参见代码清单 6.10）或将其管道传输到另一个命令。你不能重定向到同一文件名，否则你的文件最终将没有内容。

```
[ejr@hobbes manipulate]$ sed 's/oldaddr@raycomm.com/newaddr@raycomm.com' /g address.htm > address-new.htm
[ejr@hobbes manipulate]$ head address-new.htm
<BODY BACKGROUND="/images/background.gif" BGcolor="#FFFFFF" TEXT="#000000" LINK="#000908" VLINK="#000000" ALINK="#ff0000">
<P>
Please send all comments to <A HREF="mailto:newaddr@raycomm.com">newaddr@raycomm.com</A>.
</P>
<TABLE BORDER=0>
<TR>
<TD WIDTH="150" VALIGN=TOP>
[ejr@hobbes manipulate]$
```

代码清单 6.10 你可以使用 sed 对文件进行更改，例如这里的地址更改。

## ✓ 提示

- ■ 你可以让 sed 快速处理多个文档。参见第 10 章，了解如何使用循环创建 shell 脚本的信息。
- ■ 因为 sed 命令可能很长且难以处理，因此将命令保存在单独的文本文件（以免重新输入）可能会有所帮助。例如，如果你将命令 s/oldaddr@raycomm.com/newaddr@raycomm.com/g 保存在名为 script.sed 的文件中，你可以发出 sed -f script.sed address.htm > address-new.htm 来运行 script.sed 文件中的 sed 命令。你的 script.sed 文件中可以包含任意数量的命令。

## 使用 awk 更改文件

虽然 sed 是按行处理的并且让你随心所欲地修改，但 awk 是按字段处理的，非常适合操作数据库或逗号分隔的文件。例如，如果你有一个地址簿文件，你可以使用 awk 来查找并更改你指定的字段中的信息，如代码清单 6.11 所示。在以下步骤中，我们将向你展示一些使用 awk 修改、例如地址簿文件的方法示例。

## 使用 awk 更改文件：

- 1. awk '{ print $1 }' address.book
在 shell 提示符下，使用 awk '{ print $1 }' address.book 文件来查看 address.book 文件并选择（并发送到标准输出）每条记录（行）中的第一个字段。更具体地说，从内到外开始

> $1 引用每行中的第一个字段。除非另有指定，否则 awk 假定空格分隔字段，因此第一个字段从行首开始并持续到第一个空格。

> {} 包含 awk 命令，引号是必要的以将 awk 命令绑定在一起（以便命令中的第一个空格不会被 shell 解释为命令的结束）。参见代码清单 6.11。

- 2. awk -F ', ' '{ print $1 }' address.book
-F 标志告诉 awk 使用其后的字符——在本例中为逗号 (, )——作为字段分隔符。此更改使命令的输出更干净、更准确。如果你正在处理 /etc/passwd，则会使用 -F: 来指定 : 为字段分隔符。

```
[ejr@hobbes manipulate]$ awk '{ print $1 }' address.book
Schmidt,
Feldman,
Brown,
Smith,
Jones,
[ejr@hobbes manipulate]$
```

代码清单 6.11 awk 让你访问文件中的各个字段。

## De-what?

分隔文件使用特定字符来显示一个信息位结束和另一个开始的位置。每个信息片段都是一个单独的字段。例如，包含 "John, Doe, Thornton, Colorado" 的文件是逗号分隔的，字段之间带有逗号。其他文件，例如 /etc/passwd 文件，使用冒号 (:) 来分隔字段。几乎任何在内容中未使用的符号都可以用作分隔符。

