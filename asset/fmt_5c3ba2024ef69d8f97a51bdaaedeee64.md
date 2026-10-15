
Shell 函数名称遵循与变量相同的规则。函数必须包含至少一个命令。可选的 `return` 命令满足了这一要求。

## 局部变量

在我们迄今为止编写的脚本中，所有变量（包括常量）都是全局变量。全局变量在整个程序中保持存在。这对许多情况来说是可以的，但有时会使 shell 函数的使用变得复杂。在 shell 函数内部，通常希望有局部变量。局部变量只能在定义它的 shell 函数内访问，并在 shell 函数终止后就不再存在。

拥有局部变量允许程序员使用可能已经存在的变量名，而无需担心潜在的名称冲突，无论这些名称是在脚本全局中还是在其他 shell 函数中。

下面是一个演示局部变量如何定义和使用的示例脚本：

```
#!/bin/bash

# local-vars: script to demonstrate local variables

foo=0      # global variable foo

funct_1 () {

    local foo   # variable foo local to funct_1

    foo=1

    echo "funct_1: foo = $foo"

}

funct_2 () {

    local foo   # variable foo local to funct_2

    foo=2

    echo "funct_2: foo = $foo"

}

echo "global:  foo = $foo"

funct_1
```

```
echo "global:  foo = $foo"

funct_2

echo "global:  foo = $foo"
```

正如我们所见，局部变量是通过在变量名前加上 `local` 这个词来定义的。这会在定义它的 shell 函数中创建一个局部变量。一旦离开 shell 函数，该变量就不再存在。当我们运行此脚本时，我们看到结果：

```
[me@linuxbox ~]$ local-vars

global:  foo = 0

funct_1: foo = 1

global:  foo = 0

funct_2: foo = 2

global:  foo = 0
```

我们看到，在两个 shell 函数内部对局部变量 `foo` 的赋值对函数外部定义的 `foo` 的值没有任何影响。

此功能允许 shell 函数以彼此独立以及与其中出现的脚本独立的方式编写。这非常有价值，因为它有助于防止程序的一个部分干扰另一个部分。它还允许 shell 函数以可移植的方式编写。也就是说，它们可以根据需要从一个脚本剪切并粘贴到另一个脚本中。

## 保持脚本运行

在开发我们的程序时，保持程序处于可运行状态是有用的。通过这样做并频繁测试，我们可以在开发过程的早期阶段发现错误。这将使调试问题变得容易得多。例如，如果我们运行程序，进行一个小的更改，然后再次运行程序并发现问题，那么很可能最近的更改是问题的来源。通过添加空函数，即程序员术语中的存根，我们可以在早期阶段验证程序的逻辑流程。在构建存根时，最好包含一些为程序员提供反馈的内容，以显示逻辑流程正在执行。如果我们现在查看脚本的输出：

```
[me@linuxbox ~]$ sys_info_page

<HTML>

    <HEAD>

        <TITLE>System Information Report For twin2</TITLE>
```




System Information Report For linuxbox
Generated 03/19/2009 04:02:10 PM EDT, by me

我们看到在时间戳之后输出中出现了一些空行，但我们无法确定原因。如果我们修改函数以包含一些反馈：

```
report_uptime () {

    echo "Function report_uptime executed."

    return

}

report_disk_space () {

    echo "Function report_disk_space executed."

    return

}

report_home_space () {

    echo "Function report_home_space executed."

    return

}
```

并再次运行脚本：

```
[me@linuxbox ~]$ sys_info_page

<HTML>

    <HEAD>

        <TITLE>System Information Report For linuxbox</TITLE>

    </HEAD>

    <BODY>

        <H1>System Information Report For linuxbox</H1>

        <P>Generated 03/20/2009 05:17:26 AM EDT, by me</P>

        Function report_uptime executed.

        Function report_disk_space executed.

        Function report_home_space executed.

    </BODY>

</HTML>
```

我们现在看到，事实上，我们的三个函数正在被执行。

在函数框架就位并正常工作后，是时候完善部分函数代码了。首先是 `report_uptime` 函数：

```
report_uptime () {

    cat <<-_EOF_

        <H2>System Uptime</H2>

        <PRE>$(uptime)</PRE>

    _EOF_

    return

}
```

它非常简单。我们使用一个 here document 来输出一个章节标题和 `uptime` 命令的输出，并用 `<PRE>` 标签包围以保留命令的格式。`report_disk_space` 函数类似：

```
report_disk_space () {

    cat <<-_EOF_

        <H2>Disk Space Utilization</H2>

        <PRE>$(df -h)</PRE>

    _EOF_

    return

}
```

此函数使用 `df -h` 命令来确定磁盘空间使用情况。最后，我们将构建 `report_home_space` 函数：

```
report_home_space () {

    cat <<-_EOF_

        <H2>Home Space Utilization</H2>

        <PRE>$(du -sh /home/*)</PRE>

    _EOF_

    return

}
```

我们使用 `du` 命令并带 `-sh` 选项来执行此任务。然而，这并不是解决问题的完整方案。虽然它在某些系统上有效，例如 Ubuntu，但在其他系统上则无效。原因在于许多系统将主目录的权限设置为防止其被全局读取，这是一种合理的 安全措施。在这些系统上，按原样编写的 `report_home_space` 函数只有在我们的脚本以超级用户权限运行时才有效。更好的解决方案是让脚本根据用户的权限调整其行为。我们将在下一章讨论这个问题。

## Shell Functions In Your .bashrc File

Shell 函数是别名的优秀替代品，并且实际上是创建用于个人使用的小型命令的首选方法。别名在支持的命令和 shell 功能方面非常有限，而 shell 函数则允许任何可以脚本化的内容。例如，如果我们喜欢为脚本开发的 `report_disk_space` shell 函数，我们可以为 `.bashrc` 文件创建一个名为 `ds` 的类似函数：

```
ds () {

  echo "Disk Space Utilization For $HOSTNAME"

  df -h
}
```
