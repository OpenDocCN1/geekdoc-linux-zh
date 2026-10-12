
## `grep` 选项

`grep` 的默认操作是在行内查找指定字符串的匹配项并打印。此操作对于从大量输出中提取关键数据非常有用；例如，要查找用户 `karen` 终端，使用以下命令：

```bash
$ who | grep "karen"
karen pts/2 Aug 21 13:42
$
```

在 `who` 命令的所有输出中，只显示包含字符串“`karen`”的行。尽管这很有用，但有时实际输出并不如其周围的其他项目重要。

## 配合 `grep` `sed` 使用

例如，如果你不在乎 `karen` 登录在哪里，但想知道她有多少个并发会话，可以使用 `-c` 选项：

```bash
$ who | grep -c "karen"
1
$
```

你也可以修改它，使用逻辑或 (`||`)，如果操作失败，则会告诉你用户尚未登录：

```bash
who | grep "karen" || echo "She has not come in yet"
```

`-c` 选项用于统计将要显示的行数，但显示本身被抑制了。`-c` 选项基本上执行与以下相同的任务：

```bash
$ who | grep "karen" | wc -l
1
$
```

然而，从进程中减少一个额外的操作会更快、更高效。可以与 `grep` 配合使用的选项还有：

- `-f`: 使用文件来查找要搜索的字符串。
- `-H`: 在显示中包含匹配项来源文件的默认标题（如果适用），它出现在每行的开头，但 `-h` 防止标题出现（默认不显示）。
- `-i`: 忽略大小写。如果不存在此选项，你可能需要在测试文件中搜索 `"karen"`, `"Karen"`, `"KAREN"` 及其所有变体以找到匹配。
- `-L`: 打印不包含匹配项的文件名，而 `-l` 打印包含匹配项的文件名。
- `-n`: 在显示中显示行号。这与对输出行进行编号（`nl` 可以做到）不同，因为这些模式表示的是现有文件的编号，而不是输出。
- `-q`: 静默所有输出，通常用于测试返回条件。
- `-s`: 防止发生的错误显示错误消息。如果你在扫描所有目录以查找项时，不想显示权限不足以查看某些内容的错误，此选项非常有用。
- `-v`: 作为“非”选项。它产生的显示与不使用它时产生的显示相反。例如，`who | grep -v karen` 显示所有不是 `karen` 的用户。
- `-w`: 强制找到的显示匹配整个单词。这为前面讨论的查找“`cat`”但无变体提供了最佳解决方案。
- `-x`: 强制找到的显示匹配整行。

你可以根据需要混合组合这些选项，只要一个参数不抵消另一个即可。例如，可以使用 `-wH` 或 `-H` 搜索整个单词并包含标题信息。然而，你不能指定想查看行号又只看最终计数（`-nc`），因为这两个选项会互相抵消。

接下来的一些示例展示了你如何使用这些选项。对于第一个示例，假设我们想要获取当前目录下所有子目录的详细列表 (`ls -l`)，并且对实际文件名不感兴趣。在 `ls -l` 的输出中，第一个字段显示条目的权限。如果条目是文件，第一个字符是 `-`；如果是目录，则是 `d`。你使用以下命令：

```bash
ls -l | grep "^d"
```

如果你想知道拼写字典中有多少单词，可以使用多种方法查出：

```bash
wc -l /usr/dict/words
```

或者使用：

```bash
grep -c "." /usr/dict/words
```

这两者都根据文件内的行数生成数字。然而，假设你想找到有多少以字母“`c`”（大写或小写）开头的单词：

```bash
grep -c "^c" /usr/dict/words
```

（注：由于原文后部分存在大量重复和 OCR 错误，译文已根据核心逻辑进行了清理和整合。）

```bash
$ egrep "Harris" names

Shannon Harris

Richard Harriss

William Harrisson

$
```

要查找长度大于一个字符的数值，你可以将文本包含在括号内。例如，如果你想找到 `Harriss` 和 `Harrison`（而不是 `Harris`），可以将 `"on"` 变成一个出现零次或多次的实体：

```bash
$ egrep "Harriss(on)?" names

Richard Harriss

William Harrisson

$
```

自从 `egrep` 诞生以来（同样是在 Unix 时代），大多数功能已经集成到 Linux 自带的 `grep` 版本中。通过在 `grep` 中使用 `-E` 选项，你可以获得 `egrep` 的大部分功能。

> 例如，`grep -E` 与 `egrep` 是等价的。

![](img/f9e5762d07ca45a6f38ffcb92cd56e5e_100_0.png)

# `sed`

`sed` 的名字是 `stream editor`（流编辑器）的缩写，这个描述非常准确。该工具接受输入（文本）像河流或溪流一样流过它。它根据给定的参数对文本进行编辑并修改。`sed` 的语法为：

```
sed (options) {commands} filename
```

选项的数量有限，但命令非常多。接受的选项有：

- `-e`—指定要执行的命令。
- `-f`—指定查找命令的文件。
- `-n`—以静默模式运行。

理解命令最好的方法是查看几个示例。给 `sed` 或任何编辑器提供的简单命令之一是将一个字符串替换为另一个字符串。你通过 `s`（substitute，替换）命令来实现，后面跟着一个斜杠、要查找的字符串、一个斜杠、要替换的第一个值、with，以及另一个斜杠。整个条目应该出现在单引号内：

```
'/old value/new value/'
```

示例如下：

```bash
$ echo I think the new neighbors are getting a new air pump | sed '/s/air/heat/'
```

显示的输出变为：

`I think the new neighbors are getting a new heat pump`

字符串 `"air"` 被字符串 `"heat"` 替换了。文本替换是其最简单的功能之一，也是 `sed` 最常使用的场景，这也是它的威力和特性真正优异的地方。

![](img/f9e5762d07ca45a6f38ffcb92cd56e5e_101_0.png)

> 重要的是，`sed` 不是一个交互式编辑器。一旦你给了它要执行的命令，它就会无需用户的进一步操作即可执行。

默认情况下，`sed` 按顺序逐扫描每一行。如果它搜索整行后没有找到匹配项，它将移动到下一行。如果它行内找到了搜索文本，它将进行更改并立即移动到下一行。这可能会产生一些意外的结果。例如，假设你想将单词 `"new"` 改为 `"old"`：

```bash
$ echo I think the new neighbors are getting a new air pump | sed '/s/new/old/'
```

输出变为：

`I think the old neighbors are getting a new air pump`

搜索短语的第二次出现没有被更改，因为 `sed` 在找到第一个匹配项后就结束了该行的处理。如果你想更改行内的所有出现处，必须在命令末尾使用 `g` 来进行全局搜索：

```bash
$ echo I think the new neighbors are getting a new air pump | sed '/s/new/old/g'
```

## 使用 `grep` 和 `sed`

输出变为：

`I think the old neighbors are getting a old air pump`

你在命令行上使用 `-e` 选项来标记每个命令：

```bash
$ echo this line is shorter | sed -e 's/line/phrase/' -e 's/short/long/'
```

输出变为：

`this phrase is longer`

第二种方法是将替换标准放在文件中，然后使用 `-f` 选项调用该文件：

```bash
$ cat wishlist
s/line/phrase/
s/short/long/
$ echo this line is shorter | sed -f wishlist
this phrase is longer
```

两种方法产生相同的结果，但使用文件存储命令使得更改标准、跟踪操作以及以后重新运行变得更加容易。

![](img/f9e5762d07ca45a6f38ffcb92cd56e5e_102_0.png)

> 重要的是，对于多个操作，`sed` 会在开始第二个操作之前完成第一个操作。它在开始第三个操作（以及整个文件）之前完成第二个操作，以此类推。技术上（但不推荐），你也可以通过在替换后使用分号或通过单引号输入模式来完成相同的操作：

```bash
$ echo this line is shorter | sed 's/line/phrase/;s/short/long/'
```

## 限制行

或者你可以使用：

```bash
$ echo this line is shorter | sed 's/line/phrase/;s/short/long/'
```
