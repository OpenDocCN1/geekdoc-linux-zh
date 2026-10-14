

## 控制运算符：另一种分支方式

bash 提供了两个可以执行分支的控制运算符。&&（与）和 ||（或）运算符的工作方式与 [ ] 复合命令中的逻辑运算符类似。其语法如下：

```
command1 && command2
```

以及

```
command1 || command2
```

了解这些运算符的行为非常重要。对于 && 运算符，command1 会被执行，并且只有在 command1 成功时才会执行 command2。对于 || 运算符，command1 会被执行，并且只有在 command1 不成功时才会执行 command2。

在实际应用中，这意味着我们可以这样做：

```
[me@linuxbox ~]$ mkdir temp && cd temp
```

这将创建一个名为 temp 的目录，如果创建成功，则当前工作目录将更改为 temp。只有在 mkdir 命令成功时才会尝试第二个命令。同样，像这样的命令：

```
[me@linuxbox ~]$ [ -d temp ] || mkdir temp
```

会测试 temp 目录是否存在，并且只有在测试失败时才会创建该目录。这种结构在处理脚本中的错误时非常方便，我们将在后面的章节中更详细地讨论这个问题。例如，我们可以在脚本中这样做：

```
[ -d temp ] || exit 1
```

如果脚本需要 temp 目录，而该目录不存在，则脚本将以退出状态 1 终止。

## 总结

本章的开始提出了一个问题。我们如何让 sys_info_page 脚本检测用户是否有权限读取所有主目录？有了对 if 的了解，我们可以通过向 report_home_space 函数添加以下代码来解决这个问题：

```
report_home_space () {
    if [[ $(id -u) -eq 0 ]]; then
        cat <<- _EOF_
<H2>Home Space Utilization (All Users)</H2>
<PRE>$(du -sh /home/*)</PRE>
_EOF_
    else
        cat <<- _EOF_
<H2>Home Space Utilization ($USER)</H2>
<PRE>$(du -sh $HOME)</PRE>
_EOF_
    fi
    return
}
```

我们评估 id 命令的输出。使用 -u 选项，id 输出有效用户的数字用户 ID。超级用户始终为零，而其他每个用户都是大于零的数字。了解这一点后，我们可以构建两个不同的 here 文档，一个利用超级用户权限，另一个仅限于用户自己的主目录。

我们将暂时离开 sys_info_page 程序，但不用担心。它会回来的。在此期间，我们将介绍一些在恢复工作时需要的内容。

## 进一步阅读

bash 手册页的几个部分提供了本章所涵盖主题的进一步细节：

- - Lists（涵盖控制运算符 || 和 &&）
- - Compound Commands（涵盖 [[ ]]、( ( ) ) 和 if）
- - CONDITIONAL EXPRESSIONS
- - SHELL BUILTIN COMMANDS（涵盖 test）

此外，维基百科上有一篇关于伪代码概念的良好文章：

http://en.wikipedia.org/wiki/Pseudocode

## 29 – 读取键盘输入

到目前为止我们编写的脚本缺少大多数计算机程序共有的一个功能——交互性。也就是说，程序与用户交互的能力。虽然许多程序不需要交互，但一些程序从能够直接接受用户输入中受益。例如，来自上一章的这个脚本：

```
#!/bin/bash

# test-integer2: evaluate the value of an integer.

INT=-5

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [ $INT -eq 0 ]; then
        echo "INT is zero."
    else
        if [ $INT -lt 0 ]; then
            echo "INT is negative."
        else
            echo "INT is positive."
        fi
        if [ $((INT % 2)) -eq 0 ]; then
            echo "INT is even."
        else
            echo "INT is odd."
        fi
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

每次我们想要更改 INT 的值时，都必须编辑脚本。如果脚本能够询问用户输入值会更有用。在本章中，我们将开始研究如何为我们的程序添加交互性。

