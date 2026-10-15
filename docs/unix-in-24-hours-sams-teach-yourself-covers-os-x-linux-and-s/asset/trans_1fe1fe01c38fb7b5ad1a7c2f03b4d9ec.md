
command-block
done

你可以构建任何你喜欢的列表。它可以是一串数字，也可以是命令的输出。前面我提到过遍历文件列表。这通过下面的循环得以演示：

Click here to view code image

```
for var in `ls`
do
    if
        [ -f $var ]
    then
        echo $var is a regular file
    fi
done
```

这会遍历 `ls` 输出中列出的所有文件，只显示普通文件。请注意，如果没有反引号，脚本将测试当前目录中名为 ls 的文件。这是一个完全不同的请求！

对前面代码的一个修改是，因为你在一个 shell 脚本中，可以使用 shell 展开来更高效地完成某些任务。例如，不使用 ls，而是考虑以下内容？

Click here to view code image

```
for var in * ; do
    if [ -f $var ] ; then
        echo $var is a regular file
    fi
done
```

你也可以再次在这个例子中看到，通过重新格式化脚本可以使其可读性大大提高。

## 2. 在 shell 程序中可以执行的一个不错的技巧是遍历命令行参数列表。for 循环提供了一个简洁的机制：如果从命令中省略 in 列表部分，for 循环将遍历命令行参数列表：

```
j=0
for i
do
    j=$(($sj + 1))
    echo $i is argument $j
done
```

这段代码会遍历命令行参数并标识它们在参数顺序中的位置。

在这两种情况下，进入 for 循环时，你就知道需要运行循环多少次。但是，如果你查看等待某事发生的情况，则需要使用不同的循环。while 循环是解决此问题的方案。

### Note

在脚本中遍历参数的另一种方法是使用 shell 的 shift 命令。我们将在下一小时看到这一点。

## 3. 在 Task 16.3 中，我提到过你可能想要等待文件到达的情况。这呼应了我最近遇到的一个真实情况。我们正在处理一个程序日志文件，但不知道它何时会放置在共享服务器目录中。我们尝试设置作业在文件到达后运行，但这种方法仍然遇到问题。

我们通过使用 while 循环解决了这个问题。在脚本执行结束时，我们创建了一个检查点文件。在开始时，如果检查点文件比日志文件更新，我们就会等待。从编程角度来看，就是：

Click here to view code image

```
while
  [ checkpoint -nt logfile ]
do
  sleep 60
done
```

此程序会在检查之间等待一分钟。如果新的日志文件尚未写入，程序将再次休眠 60 秒并重试。

## 4. while 循环也可以以确定性方式使用。在你不关心变量值但知道要运行命令块的次数的情况下，可以使用计数器递增次数：

```
i=0
while
  [ $i -lt 100 ]
do
  i=$(( $i + 1 ))
  commands
done
```

这肯定比在列表中枚举 100 个项目容易得多！

shell 提供了两种方便的机制来重复运行一组命令。这些循环命令在命令行和程序中都很有用。

## Task 16.6: bash Functions

本课所涵盖的大部分内容我将其归类为流程控制：指定在什么条件下执行什么命令。使用 bash 作为程序化 shell 的有趣之处在于，你实际上可以创建自己的函数并在脚本中反复使用，就像在更正式的编程环境中一样。

函数最大的价值在于它们赋予你指定和访问参数的能力。

让我们先试试水，看看它们如何能显著帮助你开发强大的 shell 脚本！

- 1. 函数定义如下：

```
function functionname
{
    shell commands
}
```

从某种意义上说，所有命令别名，如书中前面所讨论的，实际上都是简单的函数。这里有一个例子：

```
$ alias ls
alias ls='ls -F'
```

这可以重写为函数

```
function ls
{
    /bin/ls -F
}
```

它将以几乎完全相同的方式工作。最大的区别是，使用这种写法，无法为 ls 命令指定任何其他参数。

- 2. 要添加参数，只需在 -F 标志后添加 $*：

```
function ls {
    /bin/ls -F $*
}
```

现在像 ls /tmp 这样的命令将按预期工作！

- 3. 当然，使用函数而不是别名的真正价值在于，你可以显著提高新脚本的复杂程度。

作为一个例子，我想有一个命令，它扩展了之前根据文件名后缀指示文件类型的片段。在新版本中，如果图形可以在 Web 浏览器中查看（即它是 GIF 或 JPG 图像），我希望实际输出一些 HTML 片段。新版本还将为找到的 HTML 文件提供可点击的链接，并允许用户在浏览系统时点击进入目录。

### Tip

每个 shell 脚本的第一行都是特殊的，指定应使用什么程序或 shell 来解释文件中的命令。它以 # ! 表示，发音为“she-bang”，原因不明！

这是我在不使用函数的情况下对该问题的第一次尝试：

Click here to view code image

```
#!/usr/local/bin/bash
# A Web-friendly directory browser that knows
# how to show graphic images:

directory=$(QUERY_STRING:-$HOME)
```
