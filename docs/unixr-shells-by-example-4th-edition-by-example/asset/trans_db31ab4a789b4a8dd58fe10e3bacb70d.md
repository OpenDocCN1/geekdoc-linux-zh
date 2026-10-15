

可以采用军用时间或 12 小时 AM/PM 格式。时间也可以相对于当前时间指定，使用 + 号。 使用 − 号，事件将从列表中移除。

## 格式

```
sched
sched [-+]hh:mm command
sched -n
```

## 示例

```
1    > sched 14:30 echo '^G Time to start your lecture!'
2    > sched 5PM  echo Time to go home.
3    > sched +1:30 /home/ellie/scripts/logfile.sc
4    > sched
     1    17:47 /home/scripts/logfile.sc
     2    5PM   echo Time to go home.
     3    14:30 echo '^G Time to start your lecture!'
5    > sched -2
     > sched
     1    17:47 /home/scripts/logfile.sc
     2    14:30 echo '^G Time to start your lecture!'
```

## 解释

- 1. sched 命令安排 echo 命令在 14:30 执行。届时将发出蜂鸣声（Ctrl-G）并显示消息。
- 2. sched 命令将安排 echo 命令在下午 5 点执行。
- 3. 脚本 logfile.sc 将在 1 小时 30 分钟后执行。
- 4. sched 命令按数字顺序显示已安排的事件，最后一个排在最前。
- 5. 使用数字参数时，sched 将从已安排列表中移除编号的任务。任务编号 2 已被移除，如 sched 的输出所示。

a. 要将 ^G 放入 echo 语句中，输入 Ctrl-M，然后输入 Ctrl-V，然后输入 Ctrl-G。

> 8. 来自 tcsh 手册页：“已安排事件列表中的命令将在安排命令的时间之后打印第一个提示符之前执行。可能错过命令应运行的确切时间，但逾期命令将在下一个提示符时执行。”

## 9.19 在 TC Shell 中打印变量的值

### 9.19.1 echo 命令

内置的 echo 命令将其参数打印到标准输出。echo 允许使用大量转义序列，这些序列会被解释并显示为制表符、换行符、换页符等。表 9.21 列出了 echo 选项和转义序列。

TC shell 使用 BSD 和 SVR4 的风格，但允许你通过使用内置的 echo_style 变量来修改 echo 命令的行为；例如，set echo_style=bsd。参见表 9.22，以及 echo 的手册页。

表 9.21 echo 选项和转义序列

选项 | 含义
--- | ---
-n | 抑制行尾的换行符

转义序列
\a | 警报（铃声）
\b | 退格
\c | 打印行但不带换行符
\f | 换页
\n | 换行
\r | 回车
\t | 制表符
\v | 垂直制表符
\\ | 反斜杠
\nnn | ASCII 码为 nnn（八进制）的字符

表 9.22 echo_style 变量（SVR4 和 BSD）

系统 | 行为
--- | ---
bsd | 如果第一个参数是 -n，则抑制换行符
both | -n 和转义序列均生效（默认值）
none | 既不识别 sysv 也不识别 bsd
sysv | 在 echo 字符串中展开转义序列

## 示例 9.101

```
1  > echo The username is $LOGNAME.
    The username is ellie.
2  > echo "\t\tHello there\c"
    Hello there
3  > echo -n "Hello there"
    Hello there
4  > set echo_style=none
5  > echo "\t\tHello there\c"
    -n \t\tHello there\c
```

## 解释

1  echo 命令将其参数打印到屏幕。变量替换由 shell 在执行 echo 命令之前完成。

2  echo 命令默认支持与 C 编程语言类似的转义序列，也用于 SVR4 版本的 echo。> 是 shell 提示符。

3  使用 -n 选项，echo 在不带换行符的情况下显示字符串。

4  echo_style 变量被赋值为 none。BSD -n 开关和 SVR4 转义序列均不生效。

5  使用新的 echo 样式，字符串将被显示。

### 9.19.2 printf 命令

GNU 版本的 printf 可用于格式化打印输出。它以与 C 语言 printf 函数相同的方式打印格式化的字符串。格式由一个字符串组成，其中可能包含格式化指令，用来描述打印输出的外观。格式化指令以 % 开头，后跟限定符（d i o u X f e g G c s），其中 %f 代表浮点数，%d 代表整数（十进制）。

要查看 printf 限定符的完整列表以及如何使用它们，请在命令行提示符下输入 printf --help。 （参见表 9.23。）要查看你使用的 printf 的版本，请输入 printf --version。

## 格式

```
printf format [argument...]
```

## 示例 9.102

```
printf "%10.2f%5d\n" 10.5 25
```

