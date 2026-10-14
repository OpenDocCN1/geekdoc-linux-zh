

## 26 – 开始一个项目

从本章开始，我们将开始构建一个程序。该项目的目的是了解各种 shell 特性如何用于创建程序，更重要的是，创建优秀的程序。

我们将编写的程序是一个报告生成器。它将展示有关我们系统及其状态的各种统计信息，并以 HTML 格式生成此报告，以便我们可以使用 Firefox 或 Konqueror 等网页浏览器查看。

程序通常以一系列阶段构建，每个阶段都会增加功能和能力。我们程序的第一阶段将生成一个非常简化的 HTML 页面，其中不包含任何系统信息。那将在以后添加。

### 第一阶段：最小文档

我们首先需要知道的是格式良好的 HTML 文档的格式。它看起来像这样：

```
<HTML>
    <HEAD>
        <TITLE>Page Title</TITLE>
    </HEAD>
    <BODY>
        Page body.
    </BODY>
</HTML>
```

如果我们将其输入到文本编辑器中并将文件保存为 foo.html，我们可以在 Firefox 中使用以下 URL 查看该文件：

file:///home/username/foo.html

我们程序的第一阶段将能够将此 HTML 文件输出到标准输出。我们可以很容易地编写一个程序来实现这一点。让我们启动文本编辑器并创建一个名为 ~/bin/sys_info_page 的新文件：

```
[me@linuxbox ~]$ vim ~/bin/sys_info_page
```

并输入以下程序：

```
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

我们对这个问题的第一次尝试包含一个 shebang、一个注释（总是好主意）以及一系列 echo 命令，每个输出行一个。在保存文件后，我们将使其可执行并尝试运行它：

```
[me@linuxbox ~]$ chmod 755 ~/bin/sys_info_page
[me@linuxbox ~]$ sys_info_page
```

当程序运行时，我们应该在屏幕上看到 HTML 文档的文本，因为脚本中的 echo 命令将其输出发送到标准输出。我们将再次运行程序并将程序的输出重定向到文件 sys_info_page.html，以便我们可以用网页浏览器查看结果：

```
[me@linuxbox ~]$ sys_info_page > sys_info_page.html
[me@linuxbox ~]$ firefox sys_info_page.html
```

到目前为止，一切顺利。

在编写程序时，始终努力追求简洁和清晰是一个好主意。维护在程序易于阅读和理解时更容易，不用说，它可以通过减少输入量使程序更容易编写。我们当前版本的程序运行良好，但可以更简单。我们实际上可以将所有 echo 命令合并为一个，这肯定会使向程序输出添加更多行变得更容易。因此，让我们将程序更改为以下内容：

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

带引号的字符串可以包含换行符，因此包含多行文本。shell 将继续读取文本，直到遇到闭合引号。在命令行上也是如此：

```
[me@linuxbox ~]$ echo "<HTML>
>     <HEAD>
>         <TITLE>Page Title</TITLE>
>     </HEAD>
>     <BODY>
>         Page body.
>     </BODY>
> </HTML>"
```

前导“>”字符是包含在 PS2 shell 变量中的 shell 提示符。每当我们向 shell 输入多行语句时就会出现它。这个功能现在有点晦涩，但稍后，当我们介绍多行编程语句时，它会变得非常方便。

### 第二阶段：添加一些数据

现在我们的程序可以生成最小文档，让我们在报告中放入一些数据。为此，我们将进行以下更改：

```
#!/bin/bash

# Program to output a system information page
echo "<HTML>
    <HEAD>
        <TITLE>System Information Report</TITLE>
```

