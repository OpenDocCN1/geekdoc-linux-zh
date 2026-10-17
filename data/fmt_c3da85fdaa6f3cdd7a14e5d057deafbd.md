
```sh
$ var=testcase
$ echo $var
testcase
$ echo ${var%e}                    # Remove e from right
testcas
$ echo $var                        # Variable is unchanged
testcase
$ echo ${var%s*e}                  # Remove smallest match from right
testca
$ echo ${var%%s*e}                 # Remove longest match
te
$ echo ${var#?e}                   # Remove smallest match from left
stcase
$ echo ${var#*s}                   # Remove smallest match from left
tcase
$ echo ${var##*s}                  # Remove longest match from left
e
$ echo ${var#test}                 # Remove test from left
case
$ echo ${var%test}                 # No match
testcase
$
```

这些结构有许多实际用途。例如，下面的测试检查存储在变量 `file` 中的文件名是否以两个字符 `.o` 结尾。

```sh
if [ ${file%.o} != $file ] ; then
    # file ends in .o
        ...
fi
```

再举一个例子，下面是一个 shell 程序，它的功能与 Unix 系统的 `basename` 命令完全相同：

```sh
$ cat mybasename
echo ${1##*/}
$
```

该程序显示其参数，但会删除最后一个 `/` 及其之前的所有字符：

```sh
$ mybasename /usr/spool/uucppublic
uucppublic
$ mybasename $HOME
steve
$ mybasename memos
memos
$
```

等等，还有更多的结构。

## `${#variable}`

需要知道一个变量中存储了多少个字符？这正是这个结构所提供的功能：

```sh
$ text='The shell'
$ echo ${#text}
9
$
```

> **提示**
>
> 本章描述的每个参数结构在附录 A 的表 A.3 中都有总结。

## `$0` 变量

每当你执行一个 shell 程序时，shell 都会自动将程序名存储到特殊变量 `$0` 中。这在很多情况下都很有用，例如当同一个程序通过文件系统中的硬链接以不同的命令名被调用时，你可以用编程方式判断实际执行的是哪一个。

它更常用于显示错误信息，因为错误信息基于实际程序文件名，而不是程序中硬编码的内容。如果程序名通过 `$0` 引用，那么重命名程序后，错误信息也会自动更新，无需修改程序：

```sh
$ cat lu
#
# Look someone up in the phone book
#

    if [ "$#" -ne 1 ] ; then
        echo "Incorrect number of arguments"
        echo "Usage: $0 name"
        exit 1
fi

name=$1
grep "$name" $PHONEBOOK

if [ $? -ne 0 ] ; then
        echo "I couldn't find $name in the phone book"
fi
$ PHONEBOOK=$HOME/phonebook
$ export PHONEBOOK
$ lu Teri
Teri Zak             201-393-6000
$ lu Teri Zak
Incorrect number of arguments
Usage: lu name
$ mv lu lookup                    Rename it
$ lookup Teri Zak                See what happens now
Incorrect number of arguments
Usage: lookup name
$
```

某些 Unix 系统会自动让 `$0` 变成包含目录的完整路径名，这会导致错误信息和使用用法显得笨拙。这种情况下，可以使用 `$(basename $0)`，或者利用前面介绍过的技巧去掉路径名：

```sh
${0##*/}
```

## `set` 命令

shell 的 `set` 命令有两个用途：一是设置各种 shell 选项，二是重新赋值位置参数 `$1`、`$2` 等等……

### `-x` 选项

在第 7 章中，我们曾简单介绍过使用 `sh -x` 选项来帮助调试 shell 程序中的问题；而 `set` 命令则允许你在程序的具体片段中开启和关闭跟踪模式。

在程序中，语句

```sh
set -x
```

会开启跟踪模式。这意味着之后执行的所有命令，都会在完成文件名、变量和命令替换以及 I/O 重定向之后，由 shell 打印到标准错误输出。被跟踪的命令前面会带有加号。

```sh
$ x=*
$ set -x                         Set command trace option
$ echo $x
+ echo add greetings lu rem rolo
add greetings lu rem rolo
$ cmd=wc
+ cmd=wc
$ ls | $cmd -l
+ ls
+ wc -l
        5
$
```

你可以随时通过执行带 `+x` 选项的 `set` 命令来关闭跟踪模式：

```sh
$ set +x
+ set +x
$ ls | wc -l
        5
$

                         Back to normal
```

请注意，跟踪选项不会传递给子 shell。不过，你仍然可以跟踪子 shell 的执行，方法是使用 `sh -x` 选项后跟程序名来调用程序，例如：

```sh
sh -x rolo
```

或者，你也可以在程序内部插入一系列 `set -x` 和 `set +x` 命令。实际上，你可以在程序里任意插入多个 `set -x` 和 `set +x` 命令，根据需要随时开启或关闭跟踪模式！

### 不带参数的 set

如果你不给 `set` 传递任何参数，它会按字母顺序列出当前环境中存在的所有变量，无论是局部变量还是已导出变量：

```sh
$ set                         Show me all variables
CDPATH=.:/users/steve:/usr/spool
EDITOR=/bin/vi
HOME=/users/steve
IFS=

LOGNAME=steve
MAIL=/usr/spool/mail/steve
MAILCHECK=600
PATH=/bin:/usr/bin:/users/steve/bin:.
PHONEBOOK=/users/steve/phonebook
PS1=$
PS2=>
PWD=/users/steve/misc
SHELL=/usr/bin/sh
TERM=xterm
TMOUT=0
TZ=EST5EDT
cmd=wc
x=
$
```

### 使用 `set` 重新赋值位置参数

你应该还记得，位置参数无法被赋予新值或重新赋值。例如，要把 `$1` 重新赋值为 100，逻辑上可能会写成这样：

```sh
1=100
```

但这样做是行不通的。位置参数是在 shell 程序被调用时设定的。

不过，有一个巧妙的技巧：你可以使用 `set` 来改变它的值。如果在命令行中给 `set` 提供若干单词作为参数，位置参数 `$1`、`$2`……就会被赋值为这些单词。之前存储在位置参数中的值会丢失。因此，在 shell 程序中，命令

```sh
set a b c
```

会把 `a` 赋给 `$1`，`b` 赋给 `$2`，`c` 赋给 `$3`。`$#` 也会相应地被设为 3，以反映新的参数个数。

下面是一个更复杂的例子：

```sh
$ set one two three four
$ echo $1:$2:$3:$4
one:two:three:four
$ echo $#                         *This should be 4*
4
$ echo $*                         *What does this reference now?*
one two three four
$ for arg; do echo $arg; done
one
two
three
four
$
```
