
点号（`.`）命令是 `source` 命令的别名，这是一个 shell 内置命令，它读取指定的 shell 命令文件并将其视为来自键盘的输入。

> 注：Ubuntu 会在用户的 `.bashrc` 文件执行时，如果 `~/bin` 目录存在，则自动将其添加到 `PATH` 变量中。因此，在 Ubuntu 系统上，如果我们创建 `~/bin` 目录然后注销并重新登录，一切就能正常工作。

## 脚本的良好位置

`~/bin` 目录是存放个人使用脚本的好地方。如果我们编写一个脚本允许系统上的每个人使用，传统的位置是 `/usr/local/bin`。供系统管理员使用的脚本通常位于 `/usr/local/sbin`。在大多数情况下，本地提供的软件，无论是脚本还是编译程序，都应放置在 `/usr/local` 层级中，而不是 `/bin` 或 `/usr/bin`。这些目录由 Linux 文件系统层次结构标准指定，仅包含由 Linux 发行商提供和维护的文件。

## 更多格式技巧

严肃的脚本编写的一个关键目标是易于维护；也就是说，脚本的作者或其他人为了适应不断变化的需求而修改脚本的难易程度。使脚本易于阅读和理解是促进易于维护的一种方法。

## 为脚本编写配置 VIM

`vim` 文本编辑器有许多、许多配置设置。几个常见的选项可以促进脚本编写。

`:syntax on` 打开语法高亮显示。启用此设置后，shell 语法的不同元素在查看脚本时将以不同颜色显示。这有助于识别某些类型的编程错误。看起来也很酷。请注意，要使此功能正常工作，您必须安装完整的 `vim` 版本，并且您正在编辑的文件必须有 shebang 表明该文件是 shell 脚本。如果您对 `:syntax on` 有困难，请尝试 `:set syntax=sh` 代替。

`:set hlsearch` 打开高亮搜索结果的选项。假设我们搜索单词 `echo`。启用此选项后，每个实例的单词都会被高亮显示。

`:set tabstop=4` 设置制表符占用的列数。默认值为八列。将值设置为 4（这是常见做法）可以让长行更易于在屏幕上显示。

`:set autoindent` 打开自动缩进功能。这会导致 `vim` 将新行缩进与刚输入的行相同。这可以加快许多编程结构的输入速度。要停止缩进，请输入 `CTRL-D`。

这些更改可以通过将这些命令（不带前导冒号字符）添加到您的 `~/.vimrc` 文件中使其永久生效。

## 最后说明

在本章关于脚本编写的第一章中，我们研究了如何在我们的系统上编写脚本并使其易于执行。我们还看到了如何使用各种格式技术来提高脚本的可读性（从而提高可维护性）。在未来的章节中，易于维护将一再成为良好脚本编写的核心原则。

## 25

## 开始一个项目

从本章开始，我们将开始构建一个程序。本项目的目的是了解各种 shell 特性如何用于创建程序，更重要的是，创建良好的程序。

我们将编写的程序是一个报告生成器。它将展示有关我们系统及其状态的各种统计信息，并以 HTML 格式生成此报告，以便我们可以用网络浏览器查看。

程序通常是分阶段构建的，每个阶段都会增加功能和能力。我们程序的第一阶段将生成一个非常简化的 HTML 页面，其中不包含任何系统信息。那将在以后添加。

## 第一阶段：最小文档

我们首先需要知道的是格式良好的 HTML 文档的格式。它看起来像这样：

```
<HTML>

    <HEAD>

        <TITLE>Page Title</TITLE>

</HEAD>

<BODY>    Page body.

</BODY>

</HTML>
```

如果我们将其输入到文本编辑器中并将文件保存为 `foo.html`，我们可以在 Firefox 中使用以下 URL 查看文件：`file:///home/username/foo.html`。

我们程序的第一阶段将能够将此 HTML 文件输出到标准输出。我们可以很容易地编写一个程序来实现这一点。让我们启动文本编辑器并创建一个名为 `~/bin/sys_info_page` 的新文件。

```
[me@linuxbox ~]$ vim ~/bin/sys_info_page
```

然后我们输入以下程序：

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>"
echo "<HEAD>"
echo "  <TITLE>Page Title</TITLE>"
echo "</HEAD>"
echo "<BODY>"
echo "    Page body."
echo "</BODY>"
echo "</HTML>"
```

我们对这个问题的第一次尝试包含一个 shebang；一个注释（总是一个好主意）；以及一系列 `echo` 命令，每行输出一个。保存文件后，我们将使其可执行并尝试运行它：

```
[me@linuxbox ~]$ chmod 755 ~/bin/sys_info_page
[me@linuxbox ~]$ sys_info_page
```

当程序运行时，我们应该看到 HTML 文档的文本显示在屏幕上，因为脚本中的 `echo` 命令将其输出发送到标准输出。我们将再次运行程序并将程序的输出重定向到文件 `sys_info_page.html`，以便我们可以用网络浏览器查看结果：

```
[me@linuxbox ~]$ sys_info_page > sys_info_page.html
[me@linuxbox ~]$ firefox sys_info_page.html
```

到目前为止，一切顺利。

编写程序时，始终努力追求简洁和清晰是一个好主意。维护在程序易于阅读和理解时更容易，更不用说当我们减少输入量时，程序也更容易编写。我们当前版本的程序运行良好，但可以更简单。我们可以将所有 `echo` 命令合并为一个，这肯定会使向程序输出添加更多行变得更容易。因此，让我们将程序改为这样：

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>
<HEAD>
<TITLE>Page Title</TITLE>
</HEAD>
<BODY>
Page body.
</BODY>
</HTML>"
```

带引号的字符串可以包含换行符，因此可以包含多行文本。shell 将继续读取文本，直到遇到结束引号。在命令行上也是如此：

```
[me@linuxbox ~]$ echo "<HTML>
<HEAD>
> <TITLE>Page Title</TITLE>
> </HEAD>
> <BODY>
> Page body.
> </BODY>
> </HTML>"
```

前导 `>` 字符是包含在 `PS2` shell 变量中的 shell 提示符。每当我们向 shell 输入多行语句时，它就会出现。这个特性现在有点晦涩难懂，但以后当我们介绍多行编程语句时，它会变得非常方便。

## 第二阶段：添加一些数据

现在我们的程序可以生成最小文档，让我们在报告中放入一些数据。为此，我们将进行以下更改：

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>
<HEAD>
<TITLE>System Information Report</TITLE>
</HEAD>
<BODY>
<H1>System Information Report</H1>
</BODY>
</HTML>"
```

我们在报告的正文中添加了页面标题和一个标题。

## 变量和常量

我们的脚本存在一个问题，不过。注意字符串 `System Information Report` 是重复出现的吗？对于我们这个很小的脚本来说这不是问题，但让我们想象一下，如果我们的脚本非常长，并且有多个该字符串的实例。如果我们想把标题改成其他内容，我们就必须在多个地方进行更改，这可能会很费工夫。如果我们能安排脚本让该字符串只出现一次而不是多次会怎样？那样会让脚本的未来维护变得容易得多。我们可以这样做：

```bash
#!/bin/bash

# Program to output a system information page

title="System Information Report"

echo "<HTML>
<HEAD>
<TITLE>$title</TITLE>
</HEAD>
<BODY>
<H1>$title</H1>
</BODY>
</HTML>"
```

通过创建一个名为 `title` 的变量并为其赋值为 `System Information Report`，我们可以利用参数扩展并将该字符串放在多个位置。

## 创建变量和常量

那么，我们如何创建变量呢？很简单，我们直接使用它。当 shell 遇到一个变量时，它会自动创建它。这与许多编程语言不同，在那些语言中变量必须在使用前显式声明或定义。shell 对此非常宽松，这可能导致一些问题。例如，考虑在命令行上发生的这个场景：
