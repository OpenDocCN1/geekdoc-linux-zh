

## EXPLANATION

+   1 外层 for 循环开始。循环第一次执行时，Jan 被赋给 month。
+   2 内层 for 循环开始。循环第一次执行时，1 被赋给 week。内层循环完全迭代完毕后才会返回外层循环。
+   3 如果用户输入 n 或按下 Enter，则执行第 4 行。
+   4 带参数 2 的 continue 命令使控制跳转到第二个最外层循环的顶部。没有参数的 continue 将控制返回到最内层循环的顶部。
+   5 控制返回到最内层的 for 循环。
+   6 这个 done 终止最内层的循环。
+   7 这个 done 终止最外层的循环。

## 8.6.7 I/O 重定向和子 shell

输入可以从文件通过管道或重定向到循环。输出也可以从循环通过管道或重定向到文件。shell 会启动一个子 shell 来处理 I/O 重定向和管道。循环内定义的任何变量在循环终止后都不会为脚本的其余部分所知。

## 将循环的输出重定向到文件。

请参阅示例 8.41，了解如何将循环的输出重定向到文件的演示。

## EXAMPLE 8.41

```
(The Command Line)
1 $ cat memo
abc
def
ghi

(The Script)
#!/bin/sh
# Program name: numberit
# Put line numbers on all lines of memo
2 if [ $# -lt 1 ]
then
3 echo "Usage: $0 filename" >&2
exit 1
fi
4 count=1        # Initialize count
5 cat $1 | while read line   # Input is coming from file on command line
do
```

## EXAMPLE 8.41 (CONTINUED)

```
6  [ $count -eq 1 ] && echo "Processing file $1..." > /dev/tty
7  echo $count $line
8  count=`expr $count + 1`
9  done > tmp$$        # Output is going to a temporary file
10 mv tmp$$ $1
```

(The Command Line)

```
11 $ numberit memo
    Processing file memo...
```

```
12 $ cat memo
    1 abc
    2 def
    3 ghi
```

## EXPLANATION

+   1 文件 memo 的内容被显示。
+   2 如果用户在运行此脚本时未提供命令行参数，则参数的个数 ($#) 将小于 1，错误消息会出现。
+   3 如果参数个数小于 1，则使用消息会发送到标准错误 (>&2)。
+   4 变量 count 被赋值为 1。
+   5 UNIX cat 命令显示存储在 $1 中的文件名的内容，并将输出通过管道传递给 while 循环。read 命令在循环第一次执行时被赋予文件的第一行，第二次循环时赋予文件的第二行，以此类推。read 命令在成功读取输入时返回 0 的退出状态，失败时返回 1。
+   6 如果 count 的值为 1，则执行 echo 命令，其输出被发送到 /dev/tty，即屏幕。
+   7 echo 命令打印 count 的值，后跟文件中的行。
+   8 count 增加 1。
+   9 此整个循环的输出，即 $1 中的文件的每一行，被重定向到文件 tmp$$，除了文件的第一行被重定向到终端 /dev/tty。
+   10 tmp 文件被重命名为分配给 $1 的文件名。
+   11 程序被执行。待处理的文件名为 memo。
+   12 脚本执行完毕后，文件 memo 被显示，证明每一行前面都添加了行号。

> a. $$ 扩展为当前 shell 的 PID 号码。通过将此号码附加到文件名，文件名变得唯一。

## 8.6 Looping Commands

## EXAMPLE 8.4

```
(The Input File)
$ cat testing
apples
pears
peaches

(The Script)
#!/bin/sh
# This program demonstrates the scope of variables when
# assigned within loops where the looping command uses
# redirection. A subshell is started when the loop uses
# redirection, making all variables created within the loop
# local to the shell where the loop is being executed.
1  while read line
2  do
3      echo $line   # This line will be redirected to outfile
       name=JOE
4  done < testing > outfile  # Redirection of input and output
5  echo Hi there $name

(The Output)
Hi there
```

## EXPLANATION

+   1. 如果 read 命令的退出状态成功，则进入 while 循环的主体。read 命令从文件 testing 获取输入，该文件名称在第 4 行的 done 之后命名。每次循环，read 命令都会从文件 testing 读取另一行。
+   2. line 的值将在第 4 行被重定向到 outfile。
+   3. 变量 name 被赋值为 JOE。由于此循环使用了重定向，变量是循环本地的。
+   4. done 关键字包括从文件 testing 重定向输入，以及将输出重定向到文件 outfile。此循环的所有输出都将进入 outfile。
+   5. 退出循环后，name 未定义。它是 while 循环本地的，仅在该循环的主体中已知。由于变量 name 没有值，只显示字符串 Hi there。

