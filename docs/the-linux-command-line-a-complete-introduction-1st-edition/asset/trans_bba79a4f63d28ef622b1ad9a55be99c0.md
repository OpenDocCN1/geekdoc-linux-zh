
## 使用循环读取文件

while 和 until 可以处理标准输入。这使得可以使用 while 和 until 循环来处理文件。在下面的例子中，我们将显示前面章节中使用的 distros.txt 文件的内容：

```
#!/bin/bash

# while-read: read lines from a file
while read distro version release; do
  printf "Distro: %s\tVersion: %s\tReleased: %s\n" \
    $distro \
    $version \
    $release
done < distros.txt
```

要将文件重定向到循环，我们将重定向运算符放在 done 语句之后。循环将使用 read 从重定向的文件中读取字段。每次读取一行后，read 命令都会退出，并返回状态 0，直到到达文件末尾。此时，它将返回非零退出状态，从而终止循环。也可以将标准输入通过管道传入循环：

```
#!/bin/bash

# while-read2: read lines from a file
sort -k 1,1 -k 2n distros.txt | while read distro version release; do
  printf "Distro: %s\tVersion: %s\tReleased: %s\n" \
    $distro \
    $version \
    $release
done
```

这里我们获取 sort 命令的输出并显示文本流。然而，重要的是要记住，由于管道会在子 shell 中执行循环，因此在循环内创建或赋值的任何变量在循环终止时都会丢失。

## 最后的说明

随着循环的引入，再加上我们之前接触过的分支、子程序和顺序结构，我们已经涵盖了程序中使用的所有主要流程控制类型。bash 还有一些锦囊妙计，但它们都是对这些基本概念的改进。

## 30

## 故障排查

随着脚本变得越来越复杂，是时候来看看当事情出错、脚本没有按我们的预期运行时会发生什么了。在本章中，我们将介绍脚本中常见的一些错误类型，并描述一些可以用来定位和消除问题的技巧。

### 语法错误

其中一类常见的错误是*语法*错误。语法错误涉及错误地输入了 shell 语法的某些元素。在大多数情况下，这类错误会导致 shell 拒绝执行脚本。

在下面的讨论中，我们将使用这个脚本演示常见类型的错误：

```
#!/bin/bash

# trouble: script to demonstrate common errors
```

```
number=1

if [ $number = 1 ]; then
    echo "Number is equal to 1."
else
    echo "Number is not equal to 1."
fi
```

按照上面的写法，这个脚本可以成功运行：

```
[me@linuxbox ~]$ trouble
Number is equal to 1.
```

### 缺少引号

让我们编辑脚本，去掉第一个 echo 命令后面的参数中结尾的引号：

```
#!/bin/bash

# trouble: script to demonstrate common errors

number=1

if [ $number = 1 ]; then
    echo "Number is equal to 1.
else
    echo "Number is not equal to 1."
fi
```

看看会发生什么：

```
[me@linuxbox ~]$ trouble
/home/me/bin/trouble: line 10: unexpected EOF while looking for matching `"'`
/home/me/bin/trouble: line 13: syntax error: unexpected end of file
```

它产生了两个错误。有趣的是，报告的行号并不是缺少引号的位置，而是程序中更靠后的位置。如果我们跟踪缺少引号之后的程序，就能明白原因。bash 会继续查找结束引号，直到找到为止，而它会在第二条 echo 命令之后立即找到。此后，bash 会变得非常困惑，if 命令的语法也被破坏了，因为 fi 语句现在位于一个带引号（但未闭合）的字符串内部。

在较长的脚本中，这种错误可能很难发现。使用带有语法高亮功能的编辑器会有所帮助。如果安装了完整的 vim 版本，可以通过输入以下命令启用语法高亮：

```
:syntax on
```

### 缺少或意外的标记

另一个常见错误是忘记完成复合命令，例如 if 或 while。让我们看看，如果删除 if 命令中测试后的分号会发生什么。

```
#!/bin/bash

# trouble: script to demonstrate common errors

number=1

if [ $number = 1 ] then      echo "Number is equal to 1."
else                         echo "Number is not equal to 1."
fi
```

结果如下：

```
[me@linuxbox ~]$ trouble
/home/me/bin/trouble: line 9: syntax error near unexpected token `else'
/home/me/bin/trouble: line 9: `else'
```

同样，错误信息指向的错误发生在实际问题之后。实际上发生的事情非常有趣。我们记得，if 接受一系列命令，并计算列表中最后一条命令的退出状态。在我们的程序中，我们打算让这个列表只包含一条命令 [，它是 test 的同义词。[ 命令会将其后面的内容作为参数列表——在我们的例子中，有四个参数：$number、=、1 和 ]。由于分号被移除，then 一词被添加到参数列表中，这在语法上是合法的。后面的 echo 命令也是合法的。它被解释为 if 要计算退出状态的命令列表中的另一条命令。接下来遇到 else，但它出现的位置不合适，因为 shell 会将其识别为保留字（对 shell 具有特殊含义的词）而不是命令名。因此产生了错误信息。

### 未预料的展开

脚本中可能偶尔出现一些错误。有时脚本运行正常，有时则会因为展开的结果而失败。如果我们恢复缺少的分号，并将 number 的值改为空变量，就可以进行演示：

```
#!/bin/bash

# trouble: script to demonstrate common errors

number=
```

