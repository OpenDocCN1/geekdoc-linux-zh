
```bash
cat <<EOF_
<html><head>
  <title>$TITLE</title>
</head>
<body>
  <h1>$TITLE</h1>
  <p>$($TIMESTAMP (uptime))</p>
  $($report_disk_space)
  $($report_home_space)
</body>
</html>
EOF_
```

## Shell 函数的命名规则与变量遵循相同的规则

一个函数必须包含至少一条命令。`return`命令（可选的）可以满足这一要求。

### 局部变量

在我们目前为止编写的脚本中，所有的变量（包括常量）都是全局变量。全局变量在整个程序运行期间都一直存在。这对于很多情况没有问题，但有时会增加 shell 函数使用的复杂度。在 shell 函数内部，局部变量仅在定义它们的 shell 函数内可访问，并且在 shell 函数终止时就会消失。

使用局部变量允许程序员使用可能已经在脚本全局范围或其他 shell 函数中存在的变量名称，而无必担心潜在的命名冲突。

这里有一个示例脚本，演示了局部变量的定义和使用：

```bash

#!/bin/bash

# local-vars: 局部变量演示脚本

foo=0 # 全局变量 foo

funct_1 () {

  local foo # 变量 foo 局部于 funct_1

  foo=1

  echo "func_1: foo = $foo"

}

funct_2 () {

    local foo # 变量 foo 局部于 funct_2

    foo=2

    echo "func_2: foo = $foo"

}

echo "global: foo = $foo"

funct_1

echo "global: foo = $foo"

funct_2

echo "global: foo = $foo"

```

可见，局部变量是通过在变量名前加上 `local` 单词来定义的。这创建了一个局部于定义 shell 函数的变量。一旦离开该 shell 函数，该变量就不再存在。当我们运行此脚本时，将看到以下结果：

```bash

me@linuxbox ~]$ local-vars

global: foo = 0

funct_1: foo = 1

global: foo = 0

funct_2: foo = 2

global: foo = 0

```

我们看到，在 shell 函数内部对局部变量 `foo` 赋值不会影响函数外部定义的 `foo` 的值。这一特性使得编写 shell 函数时可以使其相互独立并与所属的脚本保持独立。这非常有价值，因为防止了程序的某部分干扰另一部分。它还允许编写具有可移植性的 shell 函数。也就是说，根据需要，它们可以在脚本之间进行剪粘贴。

## 保持脚本运行

在开发程序时，保持程序处于可运行状态是有用的。通过这样做并频繁测试，我们可以在开发早期检测到错误。这将调试变得容易得多。例如，如果我们运行程序，做一个微小的更改，然后再次运行并发现问题，那么最近的更改很可能是问题的来源。通过添加空函数（程序员术中称为“存根” stubs），我们可以在早期验证程序的逻辑流。在构建存根时，包含一些可以向程序员提供反馈的内容是一个好主意，这显示了逻辑流正在执行。如果我们现在查看脚本的输出：

```bash

[me@linux ~]$ sys_info_page

<html>

<head>

  <title>System Information Report For twin2</title>

</head>

<body>

<h1>System Information Report For linuxbox</h1>

<p>Generated 03/19/2018 04:02:10 PM EDT, by me</p>

</body>

</html>

```

我们看到在输出中时间戳之后有一些空行，但我们无法确定原因。如果我们将函数更改为包含一些反馈：

```bash

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

```bash

[me@linux ~]$ sys_info_page

<html>

<head>

  <title>System Information Report For linuxbox</title>

</head>

<body>

<h1>System Information Report For linuxbox</h1>

<p>Generated 03/20/2018 05:17:26 AM EDT, by me</p>

Function report_uptime executed.

Function report_disk_space executed.

Function report_home_space executed.

</body>

</html>

```

我们现在看到，事实上，我们的三个函数正在执行。

由于我们的函数框架已经建立并正常工作，是时候充实一些函数代码了。首先，是 `report_uptime` 函数：

```bash

report_uptime () {

cat <<-EOF

<h2>System Uptime</h2>

<pre>$(uptime)</pre>

EOF

  return

}

```

我们使用此处文档（here document）来输出表头和标签。同样，对于磁盘空间：

```bash

report_disk_space () {

cat <<-EOF

<h2>Disk Space</h2>

<pre>$(df -h)</pre>

EOF

  return

}

```

最后，是主目录空间：

```bash

report_home_space () {

cat <<-EOF

<h2>Home Space</h2>

<pre>$(du -sh ~)</pre>

EOF

  return

}

```

这是组织报告的一种简单方法。在下一章中，我们将探索如何使用控制结构来使脚本更具动态性。

## 总结

在本章中，我们引入了 shell 函数和局部变量。我们看到了如何使用函数来组织代码，还讨论了存根在开发期间保持程序运行的重要性。在下一章中，我们将学习控制结构。

命令的执行。按照惯例，值为 0 表示成功，另一个值表示失败。shell 提供了一个我们用于检查退出状态的参数。在这里我们看到它的运行：

```
[me@linux ~$] ls -d /usr/bin
usr/bin
[me@linux ~$] echo $?
0
```

```
[me@linux ~$] ls -d /bin/usr
ls: cannot access /bin/usr: No such file or directory
[me@linux ~$] echo $?
2
```

在这个示例中，我们执行了两次 `ls` 命令。第一次，命令执行执行。如果我们显示参数 `$?` 的值，我们会看到它是 0。我们第二次执行了 `ls` 命令（指定了一个不存在的目录），导致产生了一个错误，并再次检查了参数 `$?`。这次它包含一个 2，表示命令遇到了错误。某些程序使用不同的退出状态来为错误提供诊断，而许多程序在失败时简单地以值 1 退出。帮助页（man pages）通常包含一个标题为“退出状态”（Exit Status）的章节，描述使用了哪些代码。然而，0 始终表示成功。

shell 提供了极其简单的命令，它们的作用除了以 0 或 1 的退出状态终止外什么都不做。`true` 命令始终执行成功，而 `false` 命令始终执行失败。

```
[me@linux ~$] true
[me@linux ~$] echo $?
0
[me@linux ~$] false
[me@linux ~$] echo $?
1
```

我们可以使用这些命令来查看 `if` 语句是如何工作的。`if` 语句能够正确评估命令的成功或失败。

```
[me@linux ~$] if true; then echo "It's true."; fi
It's true.
[me@linux ~$] if false; then echo "It's true."; fi
[me@linux ~$]
```
