
`grep` 的输出被重定向到 `/dev/null`（第 237 页），因为不需要输出；只有退出码很重要。`if` 语句检查 `grep` 的取反退出状态（前导感叹号否定或改变退出状态的意义——`true` 变为 `false`，反之亦然），当找到匹配行时，该状态为 `0` 或 `true`（取反后为 `false`）。如果退出状态不为 `0` 或不为 `false`（取反后为 `true`），则说明该单词不在正确拼写单词文件中。`echo` 内建命令将不在正确拼写单词文件中的单词列表发送到标准输出。

一旦检测到 `EOF`（文件末尾），`read` 内建命令返回 `false` 的退出状态。控制权随即离开 `while` 结构，脚本终止。

在使用 `spell_check` 之前，请创建一个包含你经常使用但不在标准字典中的单词的正确拼写文件。例如，如果你在一家名为 Blinkenship 和 Klimowski, Attorneys 的公司工作，你会将 Blinkenship 和 Klimowski 放入该文件。以下示例展示了 `spell_check` 如何检查名为 `memo` 的文件中的拼写，并从拼写错误单词的输出列表中移除 Blinkenship 和 Klimowski：

```bash
$ aspell -l < memo
Blinkenship
Klimowski
target
hte
$ cat word_list
Blinkenship
Klimowski
$ spell_check word_list memo
target
hte
```

关于更多信息，请参见 `aspell` 手册（位于 `/usr/share/doc/aspell` 目录或在 `aspell.net` 上）。

> 1. 此 `if` 语句也可以写成
>
>    `$ grep -qw "${line}" "$1"`
>
>    `-q` 选项抑制 `grep` 的输出，只返回一个退出码。`-w` 选项使 `grep` 仅匹配整个单词。

## until

`until` 和 `while` 结构非常相似，唯一的区别在于循环顶部执行的测试的意义。图 27-6 表明，`until` 会持续循环，直到 `test-command` 返回 `true` 的退出状态。`while` 结构在 `test-command` 持续返回 `true` 或非错误条件时循环。`until` 控制结构具有以下语法：

```text
until test-command
    do
    commands
    done
```

以下脚本演示了一个包含 `read` 的 `until` 结构。当用户输入正确的字符字符串时，`test-command` 得到满足，结构将控制权传送到循环之外。

```bash
$ cat until1
secretname=jenny
name=noname
echo "Try to guess the secret name!"
echo
until [ "$name" = "$secretname" ]
do
    echo -n "Your guess: "
    read name
done
echo "Very good."
```

```bash
$ until1
Try to guess the secret name!

Your guess: helen
Your guess: barbara
Your guess: rachel
Your guess: jenny
Very good
```

以下 `locktty` 脚本类似于 Berkeley UNIX 上的 `lock` 命令和 GNOME 中的“锁定屏幕”菜单项。该脚本提示你输入一个密钥（密码），并使用 `until` 控制结构锁定终端。`until` 语句使系统忽略在键盘上输入的任何字符，直到用户在单独的一行中输入该密钥，从而解除终端锁定。`locktty` 脚本可以防止别人在你短暂离开终端时使用它。如果你担心其他用户会登录你的账户，它可以免去你必须注销的麻烦。

```bash
$ cat locktty
#!/bin/bash
# UNIX/WORLD, III:4

trap '' 1 2 3 18
stty -echo
echo -n "Key: "
read key_1
echo
echo -n "Again: "
read key_2
echo
key_3=
if [ "$key_1" = "$key_2" ]
then
    tput clear
    until [ "$key_3" = "$key_2" ]
    do
        read key_3
    done
else
    echo "locktty: keys do not match" 1>&2
fi
stty echo
```

### 忘记了 locktty 的密码？

如果你忘记了密钥（密码），你需要从另一个（虚拟）终端登录并终止运行 `locktty` 的进程。

`trap` 内建命令 `locktty` 脚本开头的 `trap` 内建命令（第 943 页）阻止用户通过向脚本发送信号来终止它（例如，按中断键）。捕获信号 18 意味着没有人可以使用 `CONTROL-Z`（作业控制，来自 `tty` 的停止信号）来破解锁定。（参见第 943 页的表 27-5 获取信号列表。）

`stty -echo` 命令使终端不显示在键盘上输入的字符，从而防止用户输入的密钥出现在屏幕上。在关闭键盘回显后，脚本提示用户输入密钥，将其读取到用户创建的变量 `key_1` 中，提示用户再次输入相同的密钥，并将其保存在 `key_2` 中。语句 `key_3=` 创建一个值为 `NULL` 的变量。如果 `key_1` 和 `key_2` 匹配，`locktty` 清除屏幕（使用 `tput` 命令）并开始一个 `until` 循环。`until` 循环持续尝试从终端读取并将输入赋值给 `key_3` 变量。一旦用户输入了与原始键之一（`key_2`）匹配的字符串，`until` 循环终止，并且键盘回显再次开启。

## break 和 continue

你可以使用 `break` 或 `continue` 语句来中断 `for`、`while` 或 `until` 循环。`break` 语句将控制权转移到 `done` 语句之后的语句，从而终止循环的执行。`continue` 命令将控制权转移到 `done` 语句，从而继续循环的执行。

以下脚本演示了这两个语句的用法。`for` `in` 结构循环遍历 1–10 的值。第一个 `if` 语句在索引值小于或等于 3（`$index -le 3`）时执行其命令。第二个 `if` 语句在索引值大于或等于 8（`$index -ge 8`）时执行其命令。在这两个 `if` 之间，`echo` 显示索引的值。对于所有包括 3 在内的较小值，第一个 `if` 语句显示 `continue` 并执行 `continue` 语句，该语句跳过 `echo $index` 和第二个 `if` 语句，并继续下一个 `for` 语句。对于值 8，第二个 `if` 语句显示 `break` 并执行 `break` 语句，从而退出 `for` 循环：

```bash
$ cat brk
for index in 1 2 3 4 5 6 7 8 9 10
do
if [ $index -le 3 ] ; then
echo "continue"
continue
fi
#
echo $index
#
if [ $index -ge 8 ] ; then
echo "break"
break
fi
done

$ brk
continue
continue
continue
4
5
6
7
8
break
```

## case

`case` 结构（图 27-7，第 912 页）是一种多分支决策机制。通过该结构的路径取决于 `test-string` 与其中一个 `patterns` 之间是否匹配。`case` 控制结构具有如下语法：

```bash
case test-string in
	pattern-1)
		commands-1
	;;
	pattern-2)
		commands-2
	;;
	pattern-3)
		commands-3
	;;
... 
	esac
```

以下 `case` 结构检查用户输入作为 `test-string` 的字符。该值存储在变量 `letter` 中。如果 `test-string` 的值为 `A`，该结构执行跟随 `pattern` `A` 之后的命令。右括号是 `case` 控制结构的一部分，而不是 `pattern` 的一部分。如果 `test-string` 的值为 `B` 或 `C`，该结构执行跟随匹配 `pattern` 之后的命令。星号 (`*`) 表示*任意字符串*，并作为未匹配时的兜底选项。如果没有 `pattern` 与 `test-string` 匹配，且没有通配 (`*`) `pattern`，控制权将传递给 `esac` 语句之后的命令，而 `case` 结构不采取任何操作。
