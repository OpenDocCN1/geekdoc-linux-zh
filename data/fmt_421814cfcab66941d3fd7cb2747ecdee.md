
$ print "Where is this going?"

```
注意，标准错误仍然连接到你的终端：
```

$ print -u2 "This is going to standard error"

This is going to standard error

```
让我们退出子 shell 并查看输出文件：
```

$ exit

$ cat std.out

/home/anatole/bin

anatole

Where is this going?
```

在这里，文件 `redir.out` 被打开为文件描述符 5 用于读写：
```
$ exec 5<>redir.out
```
现在 `print` 命令向文件描述符 5 写入内容：
```
$ print -u5 "This is going to fd 5"
```
然后 `cat` 命令从那里读取：
```
$ cat <&5

This is going to fd 5
```
最后，我们使用另一个 `exec` 来关闭文件描述符 5：
```
$ exec 5<&-
```
任何后续向其写入或从其读取的尝试都将产生此错误消息：
```
$ print --u5 "Trying to write to fd 5 again"

/bin/ksh: 5: bad file unit number
```
标准输入可以这样从文件获取：
```
exec 0<file
```
命令可以从文件中读取，这几乎就像你在终端上输入了它们一样。

`exec` 命令也可以用于用新程序替换当前程序。例如，你知道如果你想运行 C shell，可以像这样将其作为子 shell 调用：
```
$ csh

{aspd:1}
```
但如果你不需要它，为什么还要有一个额外的父 shell 进程挂在那里呢？在这种情况下，可以使用 `exec` 命令用 C shell 替换当前 shell：
```
$ exec csh

{aspd:1}
```
现在，如果你从 C shell 退出，就会注销。

这是另一个应用。还记得 `select` 命令部分中的 `smenu` 脚本吗？你可以通过添加更多命令，从它创建一个功能完整的 UNIX 界面菜单。如果你想将其设置为登录 shell，则需要将其添加到 `.profile` 文件中：
```
exec smenu
```
并且执行将被限制在 `smenu` 中。

## read 命令

`read` 命令用于从终端或文件读取输入。`read` 命令的基本格式为：
```
read variables
```
其中从标准输入读取一行，因此，第一个变量获取第一个单词并分配给相应的变量，第二个变量获取第二个单词，依此类推。在这里，“This is output”被读入变量 `X`、`Y` 和 `Z` 中。输入内容的第一个单词是 `This`，所以它被赋值给第一个变量 `X`。第二个单词是 `is`，所以它被赋值给第二个变量 `Y`。第三个单词是 `output`，所以它被赋值给 `Z`。
```
$ print "This is output" | read X Y

$ print $X

This

$ print $Y

is

$ print $Z

output
```
如果没有足够的变量来对应输入中的所有单词，最后一个变量将获取所有剩余单词。此命令与上一个相同，只是多给了一个字符串 "again"。
```
$ print "This is output " | read X Y

$ print $X

This

$ print $Y

is
```
因为有四个字符串但只有三个变量，`Z` 获取了剩余的单词：

### 8: read 选项

| 选项 | 说明 |
| :--- | :--- |
| -p | 从进程中读取输入行 |
| -r | 不将 \ 视为续行符 |
| -s | 在历史文件中读取输入行的副本 |
| -u | 从文件描述符读取输入 |

`read` 命令通常使用 `IFS`（内部字段分隔符）变量作为单词分隔符。`IFS` 的默认是空格、制表符或换行符（按此顺序），但可以设置为其他值。当你想要读取不是空白符分隔的数据时，这非常有用。在示例中，`IFS` 被设置为逗号：
```
$ IFS=
```
然后 `print` 参数使用新的单词分隔符供 `read` 分离：
```
$ print 'This,is,output' | read WORD1 WORD2 WORD3

$ print $WORD1 $WORD2 $WORD3

This is output
```
通过将 `IFS` 设置为 `:`,可以将 `/etc/passwd` 中的字段读取到单独的变量中。
```
$ cat ifs_test

IFS=:

exec </etc/passwd

while read -r NAME PASS UID GID COMM HOME SHELL

do

    print "Account name= $NAME

Home directory=$HOME

Login Shell=: $SHELL"

done
```
从文件中读取输入

除了从终端读取外，`read` 命令还用于从文件读取输入。`read` 命令本身只会读取一行，因此你需要配合循环命令使用。要读取文件内容，使用以下格式：
```
exec 0<file

while read variable

do

    commands

done
```
如果 `exec` 打开文件失败，脚本将带有此错误消息退出：
```
script-name: file: cannot open
```
这是一个精简版的 `kcat`。它是 `cat` 命令的简单版本。它在标准输出上逐行显示给定文件。
```
$ kcat

exec 0<$1

while read LINE

    print $LINE

done
```
性能方面，它比 `cat` 命令慢 3-4 倍，但对于演示目的足够。这里是示例输出：
```
$ kcat test.input

1: All work and no play makes a dull boy.

2: All work and no play makes a dull boy.

3: All work and no play makes a dull boy.

.
```
`kcat` 命令的真实版本位于附录 D。这是另一种可以读取输入文件的格式：
```
cat file | while read variable

do

    commands
```
在测试系统中，读取文件的 `exec` 格式比上面的最后一个版本快 40-60 倍。在你的系统中可能会不同，但仍然是一个巨大的性能改进。

# IFS 变量

`read` 命令通常使用 `IFS` 变量作为单词分隔符。`IFS` 的默认是空格、制表符或换行符（按此顺序），但可以设置为其他值。当你想要读取不是空白符分隔的数据时，这非常有用。在示例中，`IFS` 被设置为逗号：
```
$ IFS=
```
然后 `print` 参数使用新的单词分隔符供 `read` 分离：
```
$ print 'This,is,output' | read WORD1 WORD2 WORD3

$ print $WORD1 $WORD2 $WORD3

This is output
```
通过将 `IFS` 设置为 `:`,可以将 `/etc/passwd` 文件中的字段读取到单独的变量中。
```
$ cat ifs_test

IFS=:

exec </etc/passwd

while read -r NAME PASS UID GID COMM HOME SHELL

do

    print "Account name= $NAME

Home directory=$HOME

Login Shell=: $SHELL"

done
```

# 第8 章：编写 Korn Shell 脚本

以下是示例输出：
```
$ ifs_test

Account name=root

Home directory=/

Login Shell=/bin/ksh

Account name=anatole

Home directory=/home/anatole

Login Shell=/bin/ksh
```

# 更多 read 用

`read` 命令的另一种格式是：
```
read options [variables]
```
其中输入被读取并根据给定选项赋值给变量。`-u` 用于从特定的文件描述符读取输入。如果文件描述符大于2，则必须先用 `kcat` 命令打开。让我们再次查看简化版的 `kcat`。它可以被更改为在显示下一行之前提示继续，如下：
```
$ cat kcat

exec 0<$1

while read LINE

do

  print $LINE
