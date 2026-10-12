
**回答：** 可以；事实上，`for-in` 循环非常便于管理文件。你可以使用特殊字符生成文件名，作为 `for-in` 循环中的值列表。例如，特殊字符 `*` 本身生成所有文件和目录的列表，而 `*.c` 则列出所有以 `.c` 扩展的文件。放在 `for-in` 循环值列表中的特殊字符 `*` 将生成一个由当前目录下所有文件名组成的值列表，如下：

```bash
for myfiles in *
  do
```

备份脚本会对每个文件进行备份，并放在名为 `backup` 的目录中。注意使用特殊字符 `*` 来生成所有 `.c` 扩展的文件名列表。

```bash
for backfile in *.c
  do
    cp $backfile backup/
    echo $backfile
```

以下是备份脚本的运行结果：

```bash
$ backup
io.c
lib.c
main.c
```

# `for` 结构

未指定列表的 `for` 结构将命令行参数作为其值列表。调用 shell 时，命令行上指定的参数变成一个值列表。`for` 命令中使用的变量自动设置为序列中的值。在循环的第一次迭代中，变量被设置为第一个参数的值。第二次，它被设置为第二个参数的值。

未指定列表的 `for` 结构等同于由 `$*` 或 `$@` 特殊参数生成的列表。如果你愿意，可以使用 `for-in` 结构显式引用每个参数并将其赋值给变量。然而，取决于你使用 `$*` 还是 `$@` 特殊参数，参数引用的方式会有不同。如果你使用 `$*` 参数，`for-in` 将命令行上的每个单词视为参数，无论它是否带引号。例如，`hello goodbye` 被视为五个独立的参数。带引号的 `"hello goodbye"` 被视为三个独立的参数。如果你对 `$*` 本身加引号，如 `"$*"`，你将得到一个参数。在下一个示例中，`indargs` 脚本只有三个参数，但 `for-in` 结构将忽略带引号的参数。

```bash
echo "There are $# arguments"

for argf in $*
do
    echo $argf
done
```

以下是 `indargs` 脚本的运行结果：

```
$ indargs hello goodbye
There are 3 arguments
hello
and
goodbye
```

## `continue` 命令

`continue` 命令用于循环，跳过循环体中的剩余语句并继续下一次迭代。使用 `continue` 命令可能会导致代码晦涩。应该少用。

# `true`、`false` 和 `break` 命令

`true` 命令是一个简单的命令，其退出状态始终为 0，始终成功。与之对应的 `false` 命令退出状态始终为 1，始终失败。`break` 命令用于提前退出循环。`break` 命令用于立即终止循环。

# 74 Linux 编程：初学者指南

> **提示**

无限循环通常包含一个 `break` 语句。然而，同时使用 `break` 命令和无限循环会导致代码晦涩。它们应该少用。

## 专家问

**问题：** 我如何在循环中引用参数？

**回答：** 如果你想让带引号的参数被视为一个，你需要使用 `$@` 参数。此外，你需要在 `$@` 参数周围加上引号，如下：

```bash
echo "There are $# arguments"

for argf in "$*"
do
    echo $argf
done
```

以下是脚本的运行结果：

```
$ script "hello goodbye"
There are 1 arguments
hello and goodbye
```

# 模块 3：BASH Shell 控制结构 77

## 一分钟训练

- 如果循环中的测试始终为真，它会停止吗？

- 是否有方法强制循环停止？

# 项目 3-2：网页索引

`myindex` 程序整合了 BASH shell 中常用的许多编程功能。该程序会自动生成一个可以作为其他网页索引的网页。它假设某些子目录包含网页。

## 步骤详解

1. 检测当前目录下的目录，然后检查确定其中是否包含任何页面。网页是以 `.html` 或 `.htm` 扩展的文件。这些文件的名称被放置在由 HTML 命令组成的字符串中，使用 `href` 来选择和显示文件。HTML 引用组织成带有 `<ul>` 和 `</ul>` 标签的列表，每个项目之前都有一个 `<li>` 标签。目录名使用 `<h1>` 标签作为标题。

2. 在 HTML 文件中搜索标题，并将其作为索引中的链接文本。

3. 使用 `grep` 搜索 `<TITLE>` 模式的出现。如果找到，则将其返回给 `title` 变量。

4. 如果没有找到模式，则向 `$status` 变量返回错误级别 1。

5. 检查此变量以查看 `grep` 是否成功。如果是，使用一组 `sed` 命令去除前导和后缀 `<TITLE>` 和 `</TITLE>` 标签以及任何其他字符。

6. 将剩余的标题文本赋值给 `ntitle` 变量。

# 78 Linux 编程：入门指南

7. 如果 `grep` 没有找到 `<TITLE>` 标签，则将文件名赋值给 `ntitle`。

8. 使用 `basename` 从路径名中提取文件名，删除前面的目录名。

9. 使用 `cut` 去除扩展名（使用点号作为分隔符输出第一个字段）。`.htm` 和 `.html` 扩展名均可以被删除。

10. 在为文本赋值给 `ntitle` 后，将其用作 `href` HTML 行中的链接文本。该行以 `<li>` 标签开头，表示它是一个列表项。

此处显示了 `myindex` 脚本：

```bash
#!/bin/sh
echo '<HTML>'
echo '<HEAD>'
echo '<TITLE>My Index</TITLE>'
echo '</HEAD>'
echo '<BODY>'
echo '<H1>Index of HTML Files</H1>'

for i in *
do
	if [ -d $i ]
	then
		echo "<h2>$i</h2>"
		echo '<ul>'
		for j in $i/*.htm
		do
			if [ -f $j ]
			then
				line=$(grep '<TITLE>' $j)
				if [ $? -eq 1 ];
				then
					title=$(basename $j | cut -f1 -d.)
				else
					title=$(echo $line | sed 's/.*<TITLE>//' | sed 's/</TITLE>.*//')
				fi
				echo "<li><a href=$j>$title</a></li>"
			fi
		done
		echo '</ul>'
	fi
done
echo '</BODY>'
echo '</HTML>'
```

# 模块 3：BASH Shell 控制结构 79

`myindex` 程序输出到标准输出，因此必须使用以下行代码将其重定向到文件以进行保存：

```bash
$ myindex > index.html
```

以下是 `myindex.html` 的示例。

```html
<HTML>
<HEAD>
<TITLE>My Index</TITLE>
</HEAD>
<body
<h1>Index of HTML Files</h1>
<h2>doctype</h2>
<ul>
<li><a href="notes/perl.notes">Why I like Perl?</a></li>
<li><a href="notes/texnotes.html">TeX and LaTeX Notes</a></li>
</ul>
<h2>mywebs</h2>
<ul>
<li><a href="mywebs/mypics.html">mypics</a></li>
<li><a href="mywebs/vacation.html">My Summer Vacation</a></li>
</ul>
</body
</HTML>
```

图 3-1 显示了它的输出，它将在浏览器中显示。

![](img/3cfc28f62e3fe98d5a49b453e25d689c_102_0.png)

图 3-1 由 `myindex` 脚本生成的 `myindex.html` 显示

# 在控制结构中使用重定向和管道

你可以将控制结构视为向标准输出发送数据的命令。该输出随后可以被重定向或通过管道（传输到另一个命令），就像任何 Linux 命令的输出一样。在控制结构命令中，你可以在 `done` 关键字之后立即放置重定向运算符，将循环的输出重定向到文件。例如，在 `myListave` 文件中，`for-in` 循环中的 `echo` 命令会将名称和日期置于标准输出中。这些项目名称和日期随后重定向到名为 `foods` 的文件中。

```bash
items="milk cookies apples cheese"
for grocery in $items
do 
  echo "$grocery"
done > foods
```
