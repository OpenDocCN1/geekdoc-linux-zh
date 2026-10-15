

## 表13.14 bash环境变量（续）

| 变量名 | 含义 |
|---|---|
| SHELL | 当shell被调用时，它会扫描环境中是否有此名称。shell会为PATH、PS1、PS2、MAILCHECK和IFS提供默认值。HOME和MAIL由login(1)设置。 |
| SHELLOPTS | 包含已启用的shell选项列表，如braceexpand、hashall、monitor等。 |
| SHLVL | 每次启动一个bash实例时，该值增加1。 |
| TMOUT | 指定退出前等待输入的秒数。 |
| UID | 展开为当前用户的用户ID，在shell启动时初始化。 |

a. 在bash 2.x之前的版本中不可用。

## 设置环境变量

要设置环境变量，可以在赋值后或变量设置时使用export命令。（参见表13.15。）使用带-x选项的内置declare命令也可以实现同样的效果。（导出变量时不要在变量前加$。）

## 格式

```
export variable=value
variable=value; export variable
declare -x variable=value
```

## 示例13.34

```
export NAME=john
PS1='\d\W\$USER\$ ' ; export PS1
declare -x TERM=sun
```

## 表13.15 export命令及其选项

| 选项 | 值 |
|---|---|
| -- | 标记选项处理结束；其余参数被视为参数。 |
| -f | 名称-值对被视为函数而不是变量。 |
| -n | 将全局（已导出）变量转换为局部变量。该变量将不会导出到子进程。 |
| -p | 显示所有全局变量。 |

## 示例13.13

```
1 $ export TERM=sun    # or declare -x TERM=sun
2 $ NAME="John Smith"
$ export NAME
$ echo $NAME
John Smith
3 $ echo $$
319                 # pid number for parent shell
4 $ bash             # Start a subshell
5 $ echo $$
340                 # pid number for new shell
6 $ echo $NAME
John Smith
7 $ declare -x NAME="April Jenner"
$ echo $NAME
April Jenner
8 $ exit              # Exit the subshell and go back to parent shell
9 $ echo $$
319                 # pid number for parent shell
10 $ echo $NAME
John Smith
```

## 说明

1 TERM变量被赋值为sun。该变量同时被导出。现在，从此shell启动的进程将继承该变量。你可以使用declare -x来做同样的事情。

2 定义变量NAME并导出，以便从该shell启动的子shell可以使用它。

3 输出此shell的PID值。

4 启动一个新的bash shell。新shell称为子shell。原始shell是其父shell。

5 新bash shell的PID存储在$$变量中，并回显其值。

6 在父shell中设置的变量已导出到此新shell并显示出来。

7 内置declare函数是设置变量的另一种方式。使用-x开关，declare会将变量标记为导出。变量被重置为April Jenner。它会导出到所有子shell，但不会影响父shell。导出的值不会向上传播到父shell。

8 退出此bash子shell。

9 再次显示父shell的PID。

10 变量NAME包含其原始值。当从父shell导出到子shell时，变量会保留其值。子shell无法更改父shell中变量的值。

## 13.10.6 取消变量的设置

局部变量和环境变量都可以使用unset命令取消设置，除非这些变量被设置为只读。

## 示例13.56

```
unset name; unset TERM
```

## 说明

unset命令将变量从shell的内存中移除。

## 13.10.7 打印变量的值

echo命令。内置的echo命令将其参数打印到标准输出。带-e选项的echo允许使用许多控制输出外观的转义序列。表13.16列出了echo选项和转义序列。

## 表13.16 echo选项和转义序列

| 选项 | 含义 |
|---|---|
| -e | 允许解释下面所示的转义序列 |
| -E | 即使在某些默认解释这些转义字符的系统上，也禁用对这些转义字符的解释ᵃ |
| -n | 抑制输出行末尾的换行符 |

**转义序列**
| \a | 警报（响铃）ᵃ |
| \b | 退格 |
| \c | 打印该行而不带换行符 |
| \f | 换页 |
| \n | 换行 |
| \r | 回车 |
| \t | 制表符 |
| \v | 垂直制表符 |
| \\ | 反斜杠 |
| \nnn | ASCII码为nnn（八进制）的字符 |

a. 在bash 2.x之前的版本中不可用。

