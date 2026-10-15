

## EXPLANATION

+   1 变量 num 被赋值为 15。
+   2 typeset 命令将数字转换为二进制格式。显示的是数字的基数（2），后面跟一个井号（#），以及数字的二进制值。
+   3 typeset 命令将数字转换为八进制格式并显示数字在 8 进制中的值。
+   4 typeset 命令将数字转换为十六进制格式并显示数字在 16 进制中的值。
+   5 read 命令接受用户输入。输入以二进制格式输入，存储在变量 number 中，并以二进制格式显示。
+   6 typeset 命令将 number 转换为整数。它仍然以二进制格式显示。
+   7 typeset 命令将 number 转换为十进制整数并显示。
+   8 typeset 命令将 number 转换为八进制并显示其在 8 进制中的值。

## 12.3.3 Listing Integers

仅带 -i 参数的 typeset 命令将列出所有预设整数及其值，如以下显示所示。

```
$ typeset -i
ERRNO=2
LINENO=1
MAILCHECK=600
OPTIND=1
PPID=4881
RANDOM=25822
SECONDS=47366
TMOUT=0
n=5
number=#15
```

## 12.3.4 Arithmetic Operators and the let Command

let 命令是 Korn shell 内置命令，用于执行整数运算。 （参见表 12.4。）这取代了 Bourne shell 的整数测试方法。使用 let 命令的替代且首选的方法是使用 (( )) 运算符。

## Table 12.4 let Operators

| Operator | Meaning |
|---|---|
| - | Unary minus |
| ! | Logical NOT |

## Table 12.4 let Operatorsᵃ (continued)

| Operator | Meaning |
|---|---|
| ~ | Bitwise NOT |
| * | Multiply |
| / | Divide |
| % | Remainder |
| + | Add |
| - | Subtract |
| << | Bitwise left shift |
| >> | Bitwise right shift |
| <= >= < > == != | Comparison operators |
| & | Bitwise AND |
| ^ | Exclusive OR |
| && | Logical AND |
| || | Logical OR |
| ! | Unary NOT |
| = | Assignment |
| += -= *= /= %= <<= >>= &= ^= |= | Shortcut assignments |

a. The ++ and -- operators are supported on versions of ksh that are newer than 1988

## EXAMPLE 12.10

```
1
$ i=5
2
$ let i=i+1
$ print $i
6
3
$ let "i = i + 2"
$ print $i
8
4
$ let "i+=1"
$ print $i
9
```

## EXPLANATION

+   1 变量 i 被赋值为 5。
+   2 let 命令将 1 加到 i 的值上。执行算术运算时，变量替换不需要 $ （美元符号）。
+   3 如果参数包含空白，则需要引号。
+   4 使用了快捷运算符 += 将 1 加到 i 的值上。

## EXAMPLE 12.11

(The Command Line)

```
1 $ (( i = 9 ))
2 $ (( i = i * 6 ))
$ print $i
54
3 $ (( i > 0 && i <= 10 ))
4 $ print $?
1
$ j=100
5 $ (( i < j || i == 5 ))
$ print $?
0
7 $ if (( i < j && i == 54 ))
> then
> print True
> fi
True
$
```

## EXPLANATION

+   1 变量 i 被赋值为 9。 (( )) 运算符是 let 命令的另一种形式。因为表达式被包含在双括号中，所以运算符之间允许有空格。
+   2 变量 i 被赋值为 i*6 的乘积。
+   3 测试数值表达式。如果两个表达式都为真，则返回 0 退出状态。
+   4 特殊变量 ? 保存上一个执行的命令（let 命令）的退出状态。因为值为 1，所以命令失败（求值为 false）。
+   5 测试数值表达式。如果其中一个表达式为真，则返回 0 退出状态。
+   6 特殊变量 ? 保存上一个执行的命令（let 命令）的退出状态。因为值为 0，所以命令成功（求值为 true）。
+   7 if 条件命令在 let 命令之前。等待命令完成时出现二级提示。如果退出状态为 0，则执行 then 语句后的命令；否则返回主提示。

## 12.4 Positional Parameters and Command-Line Arguments

命令行参数可以通过位置参数在脚本中引用：例如，$1 设置为第一个参数，$2 设置为第二个参数，$3 设置为第三个参数。位置参数可以用 set 命令重置。参见表 12.5。

## Table 12.5 Positional Parameters

| Variable | Function |
|---|---|
| $0 | References the name of the script |
| $# | Holds the value of the number of positional parameters |
| $* | Contains a list of all the positional parameters |
| $@ | Means the same as $*, except when enclosed in double quotes |
| "$*" | Expands to a single argument, for example, "$1 $2 $3" |
| "$@" | Expands to separate arguments, for example, "$1" "$2" "$3" |

## 12.4.1 The set Command and Positional Parameters

set 命令设置位置参数。如果位置参数已经设置，set 命令将重置它们，删除旧列表中的任何值。要取消设置所有位置参数，请使用 set --。

## EXAMPLE 12.12

```
(The Script)
$ cat args
#!/bin/ksh
# Script to test command-line arguments
1 print The name of this script is $0.
2 print The arguments are $*.
3 print The first argument is $1.
4 print The second argument is $2.
5 print The number of arguments is $#.
6 oldparameters=$*
7 set Jake Nicky Scott
8 print All the positional parameters are $*.
9 print The number of positional parameters is $#.
10 print $oldparameters
```
