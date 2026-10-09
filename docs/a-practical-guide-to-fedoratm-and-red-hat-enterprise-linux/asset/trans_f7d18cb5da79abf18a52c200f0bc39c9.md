

![](img/243613168ac865b539f12460d966088e_1059_0.png)

图 27-6 一个 until 流程图

## until

**until** 和 **while** 结构类似，区别仅在于循环顶部执行测试的语义不同。图 27-6 显示，**until** 会持续循环，**直到** *test-command* 返回一个 *true*（真）的退出状态为止。而 **while** 结构则在 *test-command* 持续返回 *true* 或非错误条件时进行循环。**until** 控制结构的语法如下：

```
until test-command
do
commands
done
```

下面的脚本展示了一个包含 **read**（第 1041 页）的 **until** 结构。当用户输入正确的字符串时，*test-command* 的条件得到满足，结构将控制权转移出循环。

```
$ cat until1
secretname=zach
name=noname
echo "Try to guess the secret name!"
echo
until [ "$name" = "$secretname" ]
do
  read -p "Your guess: " name
done
echo "Very good."
```

```
$ ./until1
Try to guess the secret name!

Your guess: helen
Your guess: barbara
Your guess: rachel
Your guess: zach
Very good.
```

下面的 locktty 脚本类似于伯克利 UNIX 中的 lock 命令以及 GNOME 中的锁屏菜单选项。该脚本提示用户输入密钥（密码），并使用 until 控制结构锁定终端。until 语句使系统忽略键盘上输入的任何字符，直到用户单独在一行中输入密钥并回车，从而解锁终端。locktty 脚本可以在您短时间离开终端时防止他人使用您的终端。如果您担心其他用户会使用您的会话，它还可以让您免于注销。

```
$ cat locktty
#!/bin/bash

trap '' 1 2 3 18
stty -echo
echo
read -p "Key: " key_1
echo
read -p "Again: " key_2
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

## 忘记了 locktty 的密码？

> 如果您忘记了密钥（密码），您需要从另一个（虚拟）终端登录，并发送命令终止正在运行 locktty 的进程（例如，killall -9 locktty）。

locktty 脚本开头的 trap 内置命令（第 1047 页）通过阻止用户通过发送信号（例如，按下中断键）来终止脚本。捕获信号 20 意味着没有人可以使用 CONTROL-Z（作业控制，来自 tty 的停止）来绕过锁定。第 1047 页的表 27-5 提供了信号列表。stty -echo 命令关闭键盘回显（导致终端不显示键盘输入的字符），防止用户输入的密钥出现在屏幕上。关闭键盘回显后，脚本提示用户输入密钥，将其读取到用户创建的变量 key_1 中，提示用户再次输入相同的密钥，并将其保存在 key_2 中。语句 key_3= 创建一个值为 NULL 的变量。如果 key_1 和 key_2 匹配，locktty 会清除屏幕（使用 tput 命令）并启动一个 until 循环。until 循环不断从终端读取输入并将其分配给 `key_3` 变量。一旦用户输入了一个与原始密钥之一（`key_2`）匹配的字符串，**until** 循环就会终止，键盘回显再次开启。

## break 和 continue

您可以通过使用 **break** 或 **continue** 语句来中断 **for**、**while** 或 **until** 循环。**break** 语句将控制权转移到 **done** 语句之后的语句，从而终止循环的执行。**continue** 命令将控制权转移到 **done** 语句，继续执行循环。

下面的脚本演示了这两个语句的使用方法。**for...in** 结构循环遍历 1–10 的值。第一个 **if** 语句在索引值小于或等于 3（`$index` –le 3）时执行其命令。第二个 **if** 语句在索引值大于或等于 8（`$index` –ge 8）时执行其命令。在两个 **if** 之间，**echo** 显示索引的值。对于所有直到并包含 3 的值，第一个 **if** 语句显示 **continue**，执行一个 **continue** 语句，跳过 **echo** $index 和第二个 **if** 语句，然后继续下一个 **for** 语句。对于值 8，第二个 **if** 语句显示单词 **break** 并执行 **break** 语句，从而退出 **for** 循环。

```
$ cat brk
for index in 1 2 3 4 5 6 7 8 9 10
do
if [ $index -le 3 ] ; then
echo "continue"
continue
fi

# echo $index
#
if [ $index -ge 8 ] ; then
echo "break"
break
fi
done
```

```
$ ./brk
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

![](img/243613168ac865b539f12460d966088e_1062_0.png)

图 27-7 一个 case 流程图

## case

case 结构（图 27-7）是一种多分支决策机制。通过该结构的路径取决于 *test-string* 与其中一个 *patterns* 之间的匹配或不匹配。当 *test-string* 与其中一个 *patterns* 匹配时，shell 将控制权转移到 *pattern* 之后的 *commands*。*commands* 由双分号（`;;`）控制运算符终止。当控制权到达该控制运算符时，shell 将控制权转移到 esac 语句之后的命令。case 控制结构的语法如下：

```
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

下面的 case 结构将用户输入的字符用作 test-string。这个值保存在变量 letter 中。如果 test-string 的值为 A，结构将执行模式 A 之后的命令。右括号是 case 控制结构的一部分，而不是模式的一部分。如果 test-string 的值为 B 或 C，结构将执行与匹配模式相对应的命令。星号（*）表示任何字符串，并在没有匹配时作为兜底。如果没有模式匹配 test-string，并且没有兜底（*）模式，控制权将传递到 esac 语句之后的命令，而 case 结构不采取任何操作。

```
$ cat case1
read -p "Enter A, B, or C: " letter
case "$letter" in
A)
echo "You entered A"
;;
B)
echo "You entered B"
;;
C)
echo "You entered C"
;;
*)
echo "You did not enter A, B, or C"
;;
esac
```

```
$ ./case1
Enter A, B, or C: B
You entered B
```

下一次执行 case1 时，显示用户输入了小写字母 b。由于 test-string b 与大写字母 B 的模式（或 case 语句中的任何其他模式）不匹配，程序执行兜底模式之后的命令并显示一条消息：

```
$ ./case1
Enter A, B, or C: b
You did not enter A, B, or C
```

case 结构中的 **pattern** 是一个 glob（类似于模糊的文件引用）。它可以包含表 27-2 中所示的任何特殊字符和字符串。

## 表 27-2 模式

| 模式 | 功能 |
| :--- | :--- |
| `*` | 匹配任何字符串。用于默认情况。 |
| `?` | 匹配任何单个字符。 |
| `[...]` | 定义字符类。括号内的任何字符都会逐一尝试以匹配单个字符。两个字符之间的连字符指定字符范围。 |
| `\|` | 分隔满足 **case** 结构特定分支的替代选择。 |

下一个脚本同时接受大写字母和小写字母：

```
$ cat case2
read -p "Enter A, B, or C: " letter
case "$letter" in
a|A)
echo "You entered A"
;;
b|B)
echo "You entered B"
;;
c|C)
echo "You entered C"
;;
*)
echo "You did not enter A, B, or C"
;;
esac
```

```
$ ./case2
Enter A, B, or C: b
You entered B
```

可选 下面的例子展示了如何使用 case 结构创建一个简单的菜单。**command_menu** 脚本使用 **echo** 显示菜单项并提示用户进行选择。（select 控制结构 [第 1012 页] 是编码菜单的简单方法。）然后，case 结构根据用户的选择执行相应的实用工具。

```
$ cat command_menu
#!/bin/bash
# menu interface to simple commands
echo -e "\n COMMAND MENU\n"
echo " a. Current date and time"
echo " b. Users currently logged in"
```

