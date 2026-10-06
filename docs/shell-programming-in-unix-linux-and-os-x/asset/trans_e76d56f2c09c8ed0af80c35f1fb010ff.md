

# 函数 269

函数定义可以根据需要跨任意行。shell 将继续使用次级命令提示符提示你输入函数内的命令，直到你用 `)` 完成函数定义为止。

你可以将常用函数的定义放在 `.profile` 文件中，这样每当你登录时都可以使用它们。或者，你也可以将定义分组在一个文件中（例如 `myfuncs`），并通过输入以下命令在当前 shell 中执行该函数：

-   `. ./myfuncs`

如你现在所知，这会导致在 `myfuncs` 中定义的任何函数在当前 shell 中变得可用。

下面这个名为 `mycd` 的函数利用了函数在当前环境中运行的特性。它模拟了 Korn shell 中 `cd` 命令的操作，该命令具有替换当前目录路径部分内容的能力（更多解释，请参见第 14 章中关于 `cd` 的讨论）。

```bash
$ myfuncs
# See what's inside
# new cd function:
#   mycd switches dir
#   mycd old new  Substitute for old in current directory's path
#
mycd () {
  if [ $# -le 1 ]; then
    # normal case -- 0 or 1 argument
    cd $1
  elif [ $# -eq 2 ]; then
    # special case -- substitute $2 for $1
    cd $$(echo $PWD | sed "s|$1|$2/")
  else
    # mycd can't have more than two arguments
    echo mycd: bad argument count
    exit 1
  fi
}
```

```bash
$ .myfuncs  Read in definition
$pwd
/users/steve

$ mycd  Change directory
Did it work?
$ cd /users/pat
$ mycd pat tony  Substitute tony for pat
$pwd
/users/tony
$
```

# 第 12 章 遗留问题

函数的执行速度比同等的 shell 程序更快，因为 shell 不需要去磁盘上搜索程序、打开文件并将其内容读入内存；它可以直接跳转并直接执行各个单独命令。

函数的另一个优势能够将相关程序分组在单个文件中。例如，第 10 章中的 `add`、`lu` 和 `rem` 程序现在可以定义为 `rollo` 程序中的独立函数。这种方法的模板如下所示：

```bash
$ cat rollo
# rollo program written in function form
add () {
    # Function to add someone to the phone book
    # put commands from add here
}

lu () {
    # Function to look someone up in the phone book
    # put commands from lu here
}

rem () {
    # Function to remove someone from the phone book
    # put commands from rem here
}
```

原始 `add`、`lu` 或 `rollo` 中的任何命令都不需要更改。前三个命令通过将它们包含在 `rollo` 内部（夹在函数头和右大括号之间）被转换为函数。将它们定义为函数会导致它们无法作为独立命令被访问。

# 删除函数定义

要从 shell 中移除函数的定义，请使用带有 `-f` 选项的 `unset` 命令。眼吗？它与你用于从 shell 中移除变量定义的命令相同吗？

```bash
$ unset -f lu
$ lu: not found
```

# return 命令

如果你在函数内部使用 `exit`，它的效果不仅是终止函数的执行，还会返回到调用它的命令行。如果你只是想退出函数，请使用 `return` 命令，其格式为 `return n`。值 `n` 用作函数的返回状态。如果省略，则状态为最后一个执行的命令的状态。如果你没有在函数中包含 `return` 语句，发生也是这种情况。返回状态在其他所有方面都等同于 `exit` 状态。

# type 命令

当你输入要执行的命令名称时，知道它是函数、shell 内置命令、标准 Unix 命令还是 shell 别名是有用的。这就是 `type` 命令派显用场的地方。`type` 命令接受一个或多个名称作为参数，并告诉你它关于该名称已知的信息。这里是一些示例：

```bash
$ type () { who | wc -l; }
$ type pwd is a shell builtin
$ type ls is aliased to '/bin/ls'
$ type cat is /bin/cat
$ type lu is a function
```

# 重新回顾 Rollo

本章介绍了 `rollo` 程序的最终改进版本，它增强了额外的选项，并允许更通用类型的条目（不仅仅是名称和数字）。本章的章节讨论了 `rollo` 的各个组件，从主 `rollo` 程序本身开始。在本章最后，显示了示例输出。

# 数据格式化考虑

虽然书中之前显示的初始“名称和数字”型 `rollo` 程序很方便，但毫无疑问，更实用的程序应该允许不仅仅是名称和数字。例如，你可能还想保存地址和电子邮件地址。新的 `rollo` 程序允许电话录中的条目由多行组成。一个典型的条目可能是：

Steve's Ice Cream
444 6th Avenue
New York City 10003
212-555-3021

为了增加电话录的灵活性，现在每个条目可以包含任意数量的行。电话录中的另一个条目可能是：

YMCA
(201) 555-2344

为了在逻辑上分离电话录中的条目，通过将条目末的换行符替换为不同的字符，将每个条目“打包”成一行。我们随机选择了脱字符符号 `^`，因为它在普通用户输入、地址等地方很少出现。这个决定的唯一影响是该字符不能作为电话条目本身的一部分。

使用这种技术，所示第一个条目将以如下形式存储在电话录文件中：
Steve's Ice Cream*444 6th Avenue*New York City 10003*212-555-3021*

以及第二个条目为：
YMCA^(201) 555-2344^

现在，处理这种格式的条目变得非常容易，这证明了深入思考问题和解决方案可以带来巨大的益处。

# rollo

```bash（此处为代码块，根据要求不翻译，已保持原样）
```

