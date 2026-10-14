
Page body.
</body>
</html>

如果我们将此内容输入到文本编辑器中并将文件保存为 *foo.html*，我们就可以在 Firefox 中使用以下 URL 查看该文件：*file:///home/username/foo.html*。

我们程序的第一阶段将能够将此 HTML 文件输出到标准输出。我们可以很容易地编写一个程序来实现这一点。让我们启动文本编辑器并创建一个名为 `~/bin/sys_info_page` 的新文件。

```
[me@linuxbox ~]$ vim ~/bin/sys_info_page
```

输入以下程序：

```
#!/bin/bash

# Program to output a system information page

echo "<html>"
echo "    <head>"
echo "        <title>Page Title</title>"
echo "    </head>"
echo "    <body>"
echo "        Page body."
echo "    </body>"
echo "</html>"
```

我们对该问题的第一次尝试包含一个 shebang、一个注释（始终是个好主意），以及一系列 echo 命令，每行输出对应一个命令。在保存文件后，我们将使其可执行并尝试运行它。

```
[me@linuxbox ~]$ chmod 755 ~/bin/sys_info_page
[me@linuxbox ~]$ sys_info_page
```

当程序运行时，我们应该在屏幕上看到 HTML 文档的文本，因为脚本中的 echo 命令将其输出发送到标准输出。我们将再次运行程序

并将程序的输出重定向到文件 sys_info_page.html，以便我们可以使用网络浏览器查看结果。

```
[me@linuxbox ~]$ sys_info_page > sys_info_page.html
[me@linuxbox ~]$ firefox sys_info_page.html
```

到目前为止，一切顺利。

在编写程序时，始终努力追求简洁和清晰是个好主意。当程序易于阅读和理解时，维护会更容易，而且它还可以使程序更容易编写，减少输入量。我们当前版本的程序运行良好，但可以更简单。我们实际上可以将所有 echo 命令合并为一个，这肯定会使向程序输出添加更多行变得更容易。因此，让我们将程序更改为以下内容：

```
#!/bin/bash

# Program to output a system information page
echo "<html>
<head>
<title>Page Title</title>
</head>
<body>
Page body.
</body>
</html>"
```

带引号的字符串可以包含换行符，因此可以包含多行文本。shell 会一直读取文本，直到遇到闭合引号为止。在命令行上也是如此：

```
[me@linuxbox ~]$ echo "<html>
> <head>
> <title>Page Title</title>
> </head>
> <body> Page body.
> </body>
> </html>"
```

前导 > 字符是包含在 PS2 shell 变量中的 shell 提示符。每当我们向 shell 输入多行语句时，它就会出现。这个功能现在有点晦涩难懂，但稍后，当我们介绍多行编程语句时，它会变得非常方便。

## 第二阶段：添加一些数据

现在我们的程序可以生成最小的文档，让我们在报告中放入一些数据。为此，我们将进行以下更改：

```
#!/bin/bash

# Program to output a system information page
echo "<html>
    <head>
        <title>System Information Report</title>
    </head>
    <body>
        <h1>System Information Report</h1>
    </body>
</html>"
```

我们在报告的标题和正文中添加了一个页面标题和一个标题。

## 变量和常量

然而，我们的脚本存在一个问题。注意到字符串 System Information Report 是重复的吗？对于我们这个微小的脚本来说这不是问题，但让我们想象一下，如果我们的脚本非常长并且包含该字符串的多个实例。如果我们想将标题更改为其他内容，我们就必须在多个位置进行更改，这可能需要大量工作。如果我们能安排脚本使字符串只出现一次而不是多次会怎样？这将使脚本的未来维护变得容易得多。我们可以这样做：

```
#!/bin/bash

# Program to output a system information page
```

```
title="System Information Report"
echo "<html>"
    <head>
        <title>$title</title>
    </head>
    <body>
        <h1>$title</h1>
    </body>
</html>"
```

通过创建一个名为 title 的变量并为其分配值 System Information Report，我们可以利用参数扩展并将字符串放置在多个位置。

那么，我们如何创建变量呢？很简单，我们直接使用它。当 shell 遇到变量时，它会自动创建它。这与许多编程语言不同，在这些语言中，变量必须在使用前显式声明或定义。shell 对此非常宽松，这可能导致一些问题。例如，考虑在命令行上发生的以下场景：

```
[me@linuxbox ~]$ foo="yes"
[me@linuxbox ~]$ echo $foo
yes
[me@linuxbox ~]$ echo $foo1
[me@linuxbox ~]$
```

我们首先将值 yes 分配给变量 foo，然后使用 echo 显示其值。接下来我们以 foo1 的形式拼写错误地显示变量的值，结果为空白。这是因为 shell 在遇到它时愉快地创建了变量 foo1，并为其赋予了默认值，即空。从中我们了解到，我们必须密切注意拼写！也很重要的是要理解在这个例子中到底发生了什么。从我们之前对 shell 如何执行扩展的了解中，我们知道以下命令：

```
[me@linuxbox ~]$ echo $foo
```

会进行参数扩展并产生以下结果：

