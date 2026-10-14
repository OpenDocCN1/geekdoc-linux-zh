
是等效命令。出于减少输入量的考虑，在命令行输入选项时首选短选项，但在编写脚本时，长选项可以提供更好的可读性。

#### 缩进和行 continuation

在使用长命令时，通过将命令分散到多行可以增强可读性。在第 18 章中，我们看了一个 `find` 命令的特别长的例子：

```sh
[me@linuxbox ~]$ find playground \( -type f -not -perm 0600 -exec chmod 0600 '{}' ';' \) -or \( -type d -not -perm 0711 -exec chmod 0711 '{}' ';' \)
```

显然，这个命令乍一看有点难以理解。在脚本中，如果这样编写，这个命令可能更容易理解：

```sh
find playground \\
    \( \\
        -type f \\
        -not -perm 0600 \\
        -exec chmod 0600 '{}' ';' \\
    \) \\
    -or \\
    \( \\
        -type d \\
        -not -perm 0711 \\
        -exec chmod 0711 '{}' ';' \\
    \)
```

通过使用行 continuation（反斜杠-换行序列）和缩进，这个复杂命令的逻辑对读者来说描述得更清晰。这种技术在命令行上也有效，尽管很少使用，因为它输入和编辑起来非常笨拙。脚本和命令行之间一个区别是，脚本可以使用制表符来实现缩进，而命令行不能，因为制表符用于激活补全。

> ### 为脚本编写配置 vim
>
> vim 文本编辑器有许多、许多配置设置。有几个常见的选项可以促进脚本编写：
>
> `:syntax on`
>
> 打开语法高亮显示。设置此项后，查看脚本时，shell 语法的不同元素将以不同颜色显示。这有助于识别某些编程错误。它看起来也很酷。请注意，要使此功能正常工作，您必须安装完整的 vim 版本，并且您正在编辑的文件必须具有 shebang 指示该文件是 shell 脚本。如果上面命令有困难，请尝试 `:set syntax=sh` 代替。
>
> `:set hlsearch`
>
> 打开突出显示搜索结果的选项。假设我们搜索单词“echo”。启用此选项后，每个实例的单词都会被突出显示。
>
> `:set tabstop=4`
>
> 设置制表符占用的列数。默认值为八列。将值设置为四（这是常见做法）可以使长行更易于在屏幕上显示。
>
> `:set autoindent`
>
> 打开“自动缩进”功能。这会导致 vim 将新行缩进与刚输入的行相同。这可以加快许多编程构造的输入速度。要停止缩进，键入 Ctrl-d。
>
> 这些更改可以通过将这些命令（不带前导冒号字符）添加到您的 `~/.vimrc` 文件中使其永久生效。

#### 总结

在本脚本编写的第一章中，我们研究了如何编写脚本并使其在系统上轻松执行。我们还看到了如何使用各种格式技术来提高脚本的可读性（从而提高可维护性）。在未来的章节中，易于维护将一再成为良好脚本编写的核心原则。

#### 进一步阅读

- 有关各种编程语言中的“Hello World”程序和示例，请参阅：
  http://en.wikipedia.org/wiki/Hello_world
- 这篇维基百科文章更详细地介绍了 shebang 机制：
  http://en.wikipedia.org/wiki/Shebang_(Unix)

### 26 – 开始一个项目

从本章开始，我们将开始构建一个程序。该项目的目的是了解各种 shell 特性如何用于创建程序，更重要的是，创建优秀的程序。

我们将编写的程序是一个报告生成器。它将展示有关我们系统及其状态的各种统计信息，并以 HTML 格式生成此报告，以便我们可以使用 Firefox 或 Konqueror 等网页浏览器查看。

程序通常以一系列阶段构建，每个阶段都会增加功能和能力。我们程序的第一阶段将生成一个非常简化的 HTML 页面，其中不包含任何系统信息。那将在以后添加。

#### 第一阶段：最小文档

我们首先需要知道的是格式良好的 HTML 文档的格式。它看起来像这样：

```html
<HTML>

    <HEAD>

        <TITLE>Page Title</TITLE>

    </HEAD>

    <BODY>

        Page body.

    </BODY>

</HTML>
```

如果我们将其输入到文本编辑器中并将文件保存为 `foo.html`，我们可以在 Firefox 中使用以下 URL 查看该文件：

`file:///home/username/foo.html`

我们程序的第一阶段将能够将此 HTML 文件输出到标准输出。我们可以很容易地编写一个程序来实现这一点。让我们启动文本编辑器并创建一个名为 `~/bin/sys_info_page` 的新文件：

```sh
[me@linuxbox ~]$ vim ~/bin/sys_info_page
```

并输入以下程序：

```bash
#!/bin/bash

# Program to output a system information page

echo "<HTML>"
echo "    <HEAD>"
echo "        <TITLE>Page Title</TITLE>"
echo "    </HEAD>"
echo "    <BODY>"
echo "        Page body."
echo "    </BODY>"
echo "</HTML>"
```

我们对这个问题的第一次尝试包含一个 shebang、一个注释（总是好主意）以及一系列 `echo` 命令，每个输出行一个。在保存文件后，我们将使其可执行并尝试运行它：

```sh
[me@linuxbox ~]$ chmod 755 ~/bin/sys_info_page
[me@linuxbox ~]$ sys_info_page
```

当程序运行时，我们应该在屏幕上看到 HTML 文档的文本，因为脚本中的 `echo` 命令将其输出发送到标准输出。我们将再次运行程序并将程序的输出重定向到文件 `sys_info_page.html`，以便我们可以用网页浏览器查看结果：

```sh
[me@linuxbox ~]$ sys_info_page > sys_info_page.html
[me@linuxbox ~]$ firefox sys_info_page.html
```

到目前为止，一切顺利。

在编写程序时，始终努力追求简洁和清晰是一个好主意。维护在程序易于阅读和理解时更容易，不用说，它可以通过减少输入量使程序更容易编写。我们当前版本的程序运行良好，但可以更简单。我们实际上可以将所有 `echo` 命令合并为一个，这肯定会使向程序输出添加更多行变得更容易。因此，让我们将程序更改为以下内容：

```bash
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

带引号的字符串可以包含换行符，因此包含多行文本。shell 将继续读取文本，直到遇到闭合引号。在命令行上也是如此：

```sh
[me@linuxbox ~]$ echo "<HTML>

>     <HEAD>

>         <TITLE>Page Title</TITLE>

>     </HEAD>

>     <BODY>

>         Page body.

>     </BODY>

> </HTML>"
```

前导“>”字符是包含在 `PS2` shell 变量中的 shell 提示符。每当我们向 shell 输入多行语句时就会出现它。这个功能现在有点晦涩，但稍后，当我们介绍多行编程语句时，它会变得非常方便。

#### 第二阶段：添加一些数据

现在我们的程序可以生成最小文档，让我们在报告中放入一些数据。为此，我们将进行以下更改：

```bash
#!/bin/bash

# Program to output a system information page

echo "<HTML>

    <HEAD>

        <TITLE>System Information Report</TITLE>
```
