
7      return

8  }

9

10 # Main program starts here

11

12 echo "Step 1"

```

```

13  funct

14  echo "Step 3"

```

当 shell 读取脚本时，它会跳过第 1 行到第 11 行，因为这些行由注释和函数定义组成。执行从第 12 行开始，使用 `echo` 命令。第 13 行调用 shell 函数 `funct`，shell 就像执行任何其他命令一样执行该函数。然后程序控制转移到第 6 行，并执行第二个 `echo` 命令。接下来执行第 7 行。它的 `return` 命令终止函数并将控制返回到函数调用之后的程序行（第 14 行），然后执行最后的 `echo` 命令。请注意，为了使函数调用被识别为 shell 函数而不是解释为外部程序的名称，shell 函数定义必须出现在脚本中调用它们之前。

我们将向脚本中添加最小的 shell 函数定义：

```
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"

CURRENT_TIME=$(date +"%x %r %Z")

TIME_STAMP="Generated $CURRENT_TIME, by $USER"

report_uptime () {

    return

}

report_disk_space () {

    return

}

report_home_space () {

    return

}

cat << _EOF_

<HTML>

    <HEAD>

        <TITLE>$TITLE</TITLE>

    </HEAD>

    <BODY>

        <H1>$TITLE</H1>

        <P>$TIME_STAMP</P>

        $(report_uptime)

        $(report_disk_space)

```
```

```sh
funct_1
echo "global:  foo = $foo"
funct_2
echo "global:  foo = $foo"
```

```

正如我们所见，局部变量是通过在变量名前面加上 `local` 这个词来定义的。这会创建一个仅在定义它的 shell 函数中局部的变量。一旦离开 shell 函数，该变量就不再存在。当我们运行此脚本时，我们看到结果：

```
```text
[me@linuxbox ~]$ local-vars
global:  foo = 0
funct_1: foo = 1
global:  foo = 0
funct_2: foo = 2
global:  foo = 0
```
```

我们看到，在两个 shell 函数内部对局部变量 `foo` 的赋值对函数外部定义的 `foo` 的值没有任何影响。

此功能允许 shell 函数以相互独立且与它们出现的脚本无关的方式编写。这非常有价值，因为它有助于防止程序的一个部分干扰另一个部分。它还允许 shell 函数以可移植的方式编写。也就是说，它们可以根据需要从一个脚本剪切并粘贴到另一个脚本中。

#### 保持脚本运行

在开发我们的程序时，保持程序处于可运行状态是有用的。通过这样做并频繁测试，我们可以在开发过程的早期阶段检测错误。这将使调试问题变得容易得多。例如，如果我们运行程序，进行少量更改，然后再次运行程序并发现问题，那么最近的更改很可能是问题的来源。通过添加空函数，即程序员术语中的存根，我们可以在早期阶段验证程序的逻辑流程。在构建存根时，最好包含一些为程序员提供反馈的内容，以显示逻辑流程正在执行。如果我们现在查看脚本的输出：

```
```text
[me@linuxbox ~]$ sys_info_page
<HTML>
        <HEAD>
```
```

```
<TITLE>System Information Report For linuxbox</TITLE>
<HEAD>
<BODY>
<H1>System Information Report For linuxbox</H1>
<P>Generated 03/19/2009 04:02:10 PM EDT, by me</P>

</BODY>
</HTML>
```
```

我们看到，在时间戳之后输出中有一些空行，但我们无法确定原因。如果我们修改这些函数，加入一些反馈信息：

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

然后再次运行脚本：

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

现在我们看到，事实上，我们的三个函数确实都被执行了。

我们的函数框架已经就位并能正常工作，现在是时候充实一些函数代码了。首先是 `report_uptime` 函数：

```
report_uptime () {
    cat <<- _EOF_
    <H2>System Uptime</H2>
    <PRE>$(uptime)</PRE>
    _EOF_
    return
}
```

这非常简单明了。我们使用一个 here 文档来输出一个章节标题以及 `uptime` 命令的输出，并用 `<PRE>` 标签包围以保持命令的输出格式。`report_disk_space` 函数与此类似：

```
report_disk_space () {
    cat <<- _EOF_
    <H2>Disk Space Utilization</H2>
    <PRE>$(df -h)</PRE>
    _EOF_
    return
}
```

该函数使用 `df -h` 命令来确定磁盘空间的使用量。最后，我们将构建 `report_home_space` 函数：

```
report_home_space () {
    cat <<- _EOF_
    <H2>Home Space Utilization</H2>
    <PRE>$(du -sh /home/*)</PRE>
    _EOF_
    return
}
```

我们使用带 `-sh` 选项的 `du` 命令来完成这项任务。然而，这并不是一个完整的问题解决方案。尽管它在某些系统（例如 Ubuntu）上可以工作，但在其他系统上却不行。原因在于，许多系统设置了家目录的权限，以防止它们被所有用户读取，这是一种合理的安 security 措施。在这些系统上，按上述写法实现的 `report_home_space` 函数，

### 28 – 流程控制：使用 if 分支

在上一章中，我们遇到了一个问题：如何让我们的报告生成脚本适应运行脚本的用户的权限？这个问题的解决方案要求我们找到一种方法，根据测试的结果在脚本中“改变方向”。用编程术语来说，我们需要程序进行分支。

让我们来看一个用伪代码表达逻辑的简单示例；伪代码是一种为人类阅读而模拟计算机语言的方式：

```
X = 5
If X = 5, then:
    Say “X equals 5.”
Otherwise:
    Say “X is not equal to 5.”
```

这就是一个分支的例子。基于“X = 5 吗？”这个条件，如果成立，就做一件事：“说 X 等于 5。”否则，就做另一件事：“说 X 不等于 5。”

#### if

使用 shell，我们可以把上面的逻辑写成下面这样：

```
x=5

if [ $x = 5 ]; then
    echo "x equals 5."
else
    echo "x does not equal 5."
fi
```

或者，我们也可以在命令行中直接输入（稍微简化一下）：
