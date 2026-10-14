
虽然注释在命令行中作用不大，但它们仍然有效。我们脚本的第一行有点神秘。它看起来像是一个注释，因为它以`#`开头，但它看起来非常有目的性，而不仅仅如此。`#!`序列实际上是一种被称为 shebang 的特殊结构。shebang 用于告知应该使用哪个解释器来执行随后的脚本。每个 shell 脚本都应该包含此作为第一行。

让我们把脚本文件保存为`hello_world`。

如果我们的脚本位于列表中的任何目录中，我们的问题就解决了。`PATH`变量包含一个冒号分隔的待搜索目录列表。我们可以查看`PATH`的内容。

## 24 – 编写你的第一个脚本

开启搜索结果高亮选项。假设我们搜索单词`echo`。

开启此选项后，该单词的每个实例都将被高亮。

`set tabstop=4`设置制表符字符占据的列数。默认是 8 列。

将该值设置为 4（这是一种常见做法）可以让长行更容易适应屏幕显示。

`set autindent`

开启“自动缩进”功能。这使得`vim`在输入新行时，与刚刚输入的行具有相同的缩进量。这可以加快许多类型编程构造的输入速度。要停止缩进，请输入 Ctrl-d。

通过向你的`~/.vimrc`文件中添加这些命令（不带开头的冒号字符），可以将这些更改永久化。

### 总结

在脚本编写的第一章中，我们学习了如何编写脚本并让它们在系统中易于执行。我们还看到了如何使用各种格式化技术来提高脚本的可读性（从而提高其可维护性）。在未来的章节中，易于维护将反复作为编写良好脚本的核心原则出现。

### 进阶阅读

- 有关各种编程语言中的 "Hello World" 程序和示例，请参见：

`http://en.wikipedia.org/wiki/Hello_world`

- 这篇维基百科文章更多讨论了 shebang 机制：

`http://en.wikipedia.org/wiki/Shebang_(Unix)`

## 25 – 启动项目

从这一章开始，我们将开始构建一个程序。这个项目的目的是观察如何使用各种 shell 特性来创建程序，更重要的是创建良好的程序。

我们将编写的程序是一个报告生成器。它将展示我们系统及其状态的各种统计数据，并生成 HTML 格式的报告，以便我们使用 Firefox 或 Chrome 等网络浏览器查看。

程序通常分阶段构建，每个阶段添加功能和能力。我们程序的第一阶段将生成一个非常简单的 HTML 页面，不包含任何系统信息。那将在之后完成。

### 第一阶段：最小文档

我们首先需要知道良好的 HTML 文档格式。它看起来如下：

```html
<HTML>
  <HEAD>
    <TITLE>Page Title</TITLE>
  </HEAD>
  <body>
    Page body.
  </body>
</HTML>
```

如果我们将这些内容输入文本编辑器并将文件保存为`foo.html`，我们就可以在 Firefox 中通过以下 URL 查看该文件：

```
file:///home/username/foo.html
```

我们程序的第一阶段能够将此 HTML 文件输出到标准输出。我们可以很容易地编写一个程序来实现。让我们启动文本编辑器并创建一个名为`~/bin/sys_info_page`的新文件：

```
[me@linuxbox ~]$ vim ~/bin/sys_info_page
```

并输入以下程序：

```bash
#!/bin/bash
# 输出系统信息页的程序
echo "HTML"
echo "  <HEAD>"
echo "    <TITLE>Page Title</TITLE>"
echo "  </HEAD>"
echo "  <body>"
echo "    Page body."
echo "  </body>"
echo "</HTML>"
```

我们对这个问题的第一次尝试包含一个 shebang、一个注释（总是是个好主意）和一系列`echo`命令。在保存文件后，我们将赋予它可执行权限并运行它：

```
[me@linuxbox ~]$ chmod 755 ~/bin/sys_info_page
[me@linuxbox ~]$ sys_info_page
```

当程序运行时，我们应该能在屏幕上看到显示的 HTML 文档的文本，脚本中的`echo`命令将它们的输出发送到标准输出。我们将运行程序并将程序的输出重定向到文件`sys_info_page.html`，以便我们用网络浏览器查看结果：

```
[me@linuxbox ~]$ sys_info_page > sys_info_page.html
[me@linuxbox ~]$ firefox sys_info_page.html
```

到目前为止良好。

在编写程序时，追求简单和清晰始终是一个好主意。当程序易于阅读和理解时，维护会变得更容易，更说它还可以减少输入量来让程序变得更容易编写。我们当前版本的程序运行良好，但可以更简单。我们实际上可以把所有的`echo`命令合并为一个，这无疑将向程序输出中添加更多行变得更容易。所以，让我们把程序改为如下所示：

```bash
#!/bin/bash

# 输出系统信息页的程序

echo "<HTML>
<HEAD>
  <TITLE>Page Title</TITLE>
</HEAD>
<body>
  Page body.
</body>
</HTML>"
```

引号字符串可以包含换行符，因此包含多行文本。shell 将继续读取文本，直到遇到闭引号。它在命令行上也是这样工作的：

```
[me@linuxbox ~]$ echo "<HTML>
<HEAD>
  <TITLE>Page Title</TITLE>
</HEAD>
<body>
  Page body.
</body>
</HTML>"
```

开头的 ">" 字符是包含在`PS2` shell 变量中的 shell 提示符。每当我们输入多行时，它就会出现。

### 第二阶段：添加少量数据

现在我们的程序可以生成最小文档了，让我们在报告中放入一些数据。为了实现这一点，我们将以下更改：

```bash
#!/bin/bash

# 输出系统信息页的程序
title="System Report"
echo "<HTML>
<HEAD>
  <TITLE>$title</TITLE>
</HEAD>
<body>
  <h1>$title</h1>
  <p>The system is running smoothly.</p>
</body>
</HTML>"
```

通过创建一个名为`title`并赋值 "System Report"，我们可以利用参数扩展并将字符串放置在多个位置。

### 变量与常量

那么，我们如何创建变量？简单，直接使用它即可。当 shell 遇到变量时，它会自动创建它。这与许多在使用之前必须声明或定义的编程语言不同。shell 对此非常宽松，这可能会导致一些问题。例如，考虑这个在命令行上执行的场景：

```
[me@linuxbox ~]$ foo="yes"
[me@linuxbox ~]$ echo foo
yes
[me@linuxbox ~]$ echo $foo
```

我们首先将 "yes" 赋值给变量`foo`，然后用`echo`显示。接下来我们显示拼写为 "fool" 的变量值并得到了空结果。这是因为 shell 在遇到它时高兴地创建了该变量，并给了它空值的默认值。从中我们了解到必须密切注意拼写！理解在这个例子中实际上发生了什么也很重要。根据我们之前对 shell 如何执行扩展的观察，我们知道命令：

```
[me@linuxbox ~]$ echo $foo
```

经历了参数扩展并导致：

```
[me@linuxbox ~]$ echo yes
```

而命令：

```
[me@linuxbox ~]$ echo $fool
```

扩展为：

```
[me@linuxbox ~]$ echo
```

空变量扩展为空！这会给需要参数的命令带来混乱。这里有一个例子：

```
[me@linuxbox ~]$ foo=foo.txt
[me@linuxbox ~]$ foo1=foo1.txt
[me@linuxbox ~]$ cp $foo $fool
cp: missing destination file operand `foo.txt`
```

尝试`cp --help`获取更多信息。

我们为两个变量`foo`和`foo1`赋值了值。然后我们执行了一个`cp`操作，但拼写错了第二个参数的名字。在扩展后，`cp`命令只接收到了一个参数，而它需要两个。

关于变量名，有一些规则：

- 变量名可以由字母数字字符（字母和数字）以及下划线组成。
- 变量名的第一个字符必须是字母或下划线。
- 不允许出现空格和标点符号。
