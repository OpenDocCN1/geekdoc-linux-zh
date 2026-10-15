
如果你想为系统上的每个用户运行一个脚本，大多数 Linux 发行版都提供了 `/etc/bashrc` 文件（注意 `bashrc` 文件名前面没有点）。每当你在系统上启动 bash shell 时，bash shell 都会执行该文件中的语句。

### 总结

Linux 系统允许你通过信号（signals）来控制脚本。`bash` shell 接受信号，并将它们传递给 shell 进程下运行的任何进程。Linux 信号允许你轻松地杀死失控进程或临时暂停长时间运行的进程。

你可以在脚本中使用 `trap` 语句来捕获信号并执行命令。此功能提供了一种简单的方法，用于检查用户可以在脚本执行期间是否将其中断。

默认情况下，当你在终端会话中运行脚本时，交互式 shell 会挂起直到脚本完成。你可以通过在命令名称后添加 ampersand (`&`) 让脚本或命令以后台模式运行。当你以后台模式运行脚本或命令时，交互式 shell 会返回，让你继续输入更多命令。使用这种方法运行的后台进程仍然与终端会话绑定。如果你退出终端会话，后台进程也会退出。

为了防止这种情况发生，请使用 `nohup` 命令。该命令会拦截旨在停止命令的信号，例如当你退出终端会话时的信号。这允许脚本即使在你退出终端时也能在后台模式下继续运行。

当你将进程移动到后台模式时，你仍然可以控制它的发生情况。`jobs` 命令允许你查看从 shell 会话启动的进程。一旦你知道了后台进程的作业 ID，就可以使用 `kill` 命令向该进程发送 Linux 信号，或使用 `fg` 命令将进程带回 shell 会话的前台。你可以通过 `Ctrl-Z` 键组合挂起正在运行的进程，然后使用 `bg` 命令将其放回后台模式。

`nice` 和 `renice` 命令允许你更改进程的优先级级别。通过赋予较低的优先级，你允许 CPU 为其分配较少的时间。这在运行消耗大量 CPU 时间的长进程时非常有用。

除了在控制运行中的进程的同时，你还可以确定进程在系统上的启动时间。与其直接从命令行提示符运行脚本，不如将进程调度在另一个可用时间运行。有几种不同的方法可以实现这一点。`at` 和 `batch` 命令允许你在预设时间运行一次脚本。`cron` 程序提供了一个接口，可以按照固定的时间间隔运行脚本。

最后，Linux 系统提供了一些脚本文件，供你调度脚本在系统启动时或每当用户启动新 bash shell 时运行。`.rc.local`（openSUSE 中为 `boot.local`）文件允许你列出每次系统启动时都启动的脚本。该系统允许管理员在启动时运行用于系统维护的特殊脚本。同样，`.bash_profile` 和 `.bashrc` 文件位于每个用户的家目录下，为放置随新 shell 运行的脚本和命令提供了位置。`.bash_profile` 在用户每次登录系统时运行脚本，而 `.bashrc` 文件在每个新实例上运行脚本。

在下一章中，我们将查看如何编写脚本函数。脚本函数允许你编写一次代码块，然后在脚本的多个位置使用它们。

# 第三部分

# 高级 Shell 脚本编写

| 本部分内容 |
| --- |
| 第 14 章 创建函数 |
| 第 15 章 为脚本添加颜色 |
| 第 16 章 引入 sed 和 gawk |
| 第 17 章 正则表达式 |
| 第 18 章 高级 sed |
| 第 19 章 高级 gawk |

# 第 14 章

## 创建函数

通常在编写 shell 脚本时，你会发现发自己在多个地方使用相同的代码。如果只是一小段代码，这通常不是什么问题。然而，如果你在 shell 脚本中多次重写大段代码，那会非常累。`bash` shell 提供了一种支持用户定义函数的方法来帮助你。你可以将 shell 脚本代码封装到函数中，然后在脚本的任何地方按你需要多次使用它。本章将引导你完成创建自己的 shell 函数的过程，并演示如何在其他 shell 脚本应用程序中使用它们。

| 本章内容 |
| --- |
| 创建函数 |
| 使用参数 |
| 共享函数 |

## 基础脚本函数

当你开始编写更复杂的 shell 脚本时，你会发现自己自己在重用执行简单任务的代码部分。有时它们是一些简单的内容，例如显示文本消息和从脚本用户处获取答案。其他时候，它们是在脚本中作为较大过程的一部分被多次使用的复杂计算。

在这些种情况下，在脚本中反复编写相同的代码块可能会很令人厌烦。只需要写一次代码块，然后能够引用它就太好了。

## 创建函数

可以使用两种格式来创建函数。第一种格式使用关键字 `function` 加上名称：

```
function name {
  commands
}
```

定义函数的第二种格式更接近在其他语言中定义函数的方式：

```
name() {
  commands
}
```

函数名后的空括号表示你正在定义一个函数。

## 使用函数

要在你的脚本中使用函数，只需在行中指定函数名称，就像运行任何其他命令一样：

```
$ cat test1
!/bin/bash
# 在脚本中使用函数
```

```
function func1 {
  echo "This is an example of a function"
}
count=1
while [ $count -le 5 ];
do
  func1
  count=$[$count + 1 ]
done
```

## 高级 Shell 脚本

这是一个函数的示例
这是循环的结束
`./test2`: `func2`: command not found
现在是脚本的结束
$

第一个函数 `func1` 在脚本中的几条语句之后定义的，这是完全没有问题的。当脚本中使用 `func1` 函数时，shell 知道去哪里找到它。

然而，脚本在定义 `func2` 函数之前就尝试使用它。由于 `func2` 函数没有被定义，当脚本运行到我使用它的地方时，它产生了一条错误信息。

你还需要注意你的函数名称。记住，每个函数名称必须是唯一的，否则就会就会问题。如果你重新定义了一个函数，新的定义将覆盖原始的函数定义，而不会产生任何错误信息：

```
$ cat test3
#!/bin/bash
# 使用重复的函数名进行测试
function func1 {
echo "This is the first definition of the function name"
}
function func1 {
echo "This is a repeat of the same function name"
}
func1
echo "This is the end of the script"
$ ./test3
This is the first definition of the function name
This is a repeat of the same function name
This is the end of the script
$
```

`func1` 函数的原始定义运行正常，但在第二次定义 `func1` 之后，任何对该函数的后续使用都会使用第二个定义。

## 返回值

`bash` shell 将函数视为微脚本，并具有完善的退出状态（见第 8 章）。你有三种不同的方法可以为你的函数生成退出状态。

## 默认退出状态

默认情况下，函数的退出状态是函数中最后一条命令返回的退出状态。在函数执行后，你使用标准的 `$?` 变量来确定函数的退出状态：

```
$ cat test4
!/bin/bash
# 测试函数的退出状态
func1() {
  echo "trying to display a non-existent file"
  ls -l badfile
}
echo "testing the function:"
func1
echo "The exit status is: $?"
./test4
testing the function:
trying to display a non-existent file
ls: badfile: No such file or directory
The exit status is: 1
$
```

```
$ cat test4b
!/bin/bash
# 测试函数的退出状态
func1() {
  ls -l badfile
  echo "This was a test of a bad command"
}
echo "testing the function:"
func1
echo "The exit status is: $?"
$ ./test4b
testing the function:
ls: badfile: No such file or directory
This was a test of a bad command
The exit status is: 0
$
```
