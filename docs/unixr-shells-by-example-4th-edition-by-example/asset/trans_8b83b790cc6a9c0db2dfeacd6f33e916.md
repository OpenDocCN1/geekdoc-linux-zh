

## EXPLANATION

- 1 true 命令是一个 UNIX 命令，也是 Korn shell 中冒号命令的别名。它总是以 0 状态退出，并且经常用于启动无限循环。 （空命令 (:) 也可以用来做同样的事情。）进入循环体。
- 2 提示用户输入。用户的输入被赋给变量 answer。
- 3 如果 answer 求值为 Y、y、Yes、Yup 或 Ya（以 Y 或 y 开头的任何内容），则执行 break 命令，控制转到第 6 行。打印 Here we are 行。直到用户回答以 Y 或 y 开头的内容，程序将继续提示输入。这可能会无限持续下去！
- 4 如果第 3 行的测试失败，则执行 else 命令。当循环体在 done 关键字处结束时，控制重新开始于第 1 行的 while 顶部。
- 5 循环体的结束。
- 6 在执行 break 命令后，控制从此处开始。

continue 命令。continue 命令在某个条件为真时重新开始于循环顶部。continue 下方的所有命令将被忽略。continue 命令将控制返回到最内层循环的顶部；如果嵌套在多个循环中，continue 命令可以将其参数作为数字。控制可以从任意数量的外层循环的顶部开始。

## FORMAT

```
continue [n]
```

## EXAMPLE 12.43

```
(The Mailing List)
$ cat mail_list
errie
john
richard
melanie
greg
robin

(The Script)
# Scriptname: mailtomail?list
#!/bin/ksh
1 for name in $(< mail_list)
do
2   if [[ "$name" = "richard" ]] then
3     continue
4   else
      mail $name < memo
5   fi
done
```

## EXPLANATION

- 1 for 循环将遍历存储在名为 mail_list 的文件中的姓名列表。每次从列表中将一个姓名赋给变量 name 时，它就会从列表中移出并被列表中的下一个姓名替换。
- 2 名称匹配 richard；执行 continue 命令。因为 richard 已经移出，下一个用户 melanie 将被赋给变量 name。
- 3 continue 命令将控制返回到循环顶部，跳过循环体其余部分的任何命令。
- 4 列表中的所有用户，除了 richard，都将收到 memo 文件的副本。
- 5 循环体的结束。

### 12.6.7 Nested Loops and Loop Control

如果使用嵌套循环，break 和 continue 命令可以让你控制要终止哪个循环。

## EXAMPLE 12.44

```
(The Script)
#!/bin/ksh
1 while true ; do
  < Commands here>
2 for user in tom dick harry joe
  do
    if [[ $user = [Dd]* ]]
    then
3     continue 2
      < Commands here >
4 while true
  do
      < Commands here>
5 break 3
  done
6
7 fi
8 done
9 print Out of loop
```

## EXPLANATION

- 1 true 命令总是返回零退出状态。循环设计为无限进行，除非使用循环控制命令。
- 2 进入 for 循环。

## EXPLANATION (CONTINUED)

- 3 for 循环将遍历列表中的每个名称。如果 user 变量以 D 或 d 开头，continue 命令会使控制转到 while 循环的顶部。如果没有参数，continue 命令会使控制从 for 循环顶部开始。参数 2 告诉 shell 转到第二个封闭循环的顶部并在那里重新开始执行。
- 4 while 循环是嵌套的。true 命令总是以零状态退出。循环将无限进行。
- 5 break 命令终止最外层的 while 循环。执行从第 9 行开始。
- 6 done 关键字标记最内层 while 循环的结束。
- 7 这个 done 关键字标记 for 循环的结束。
- 8 这个 done 关键字标记最外层 while 循环的结束。
- 9 出循环。

### 12.6.8 I/O Redirection and Loops

Korn shell 允许你在循环中使用重定向和管道。与 Bourne shell 不同，循环在此 shell 中运行，而不是在子 shell 中。循环内设置的变量在循环退出时仍会被设置。

## Redirecting the Output of a Loop to a File.

循环的输出不必发送到屏幕，而是可以重定向到文件或管道。参见示例 12.45。

## EXAMPLE 12.43

```
(The Command Line)
1 $ cat memo
abc
def
ghi

----------------------------------------
(The Script)
#!/bin/ksh
# Program name: numberit
# Put line numbers on all lines of memo
2 if (( $# < 1 ))
then
    print "Usage: $0 filename" >&2
    exit 1
fi
3 integer count=1      # Initialize count
4 cat $1 | while read line   # Input is coming from memo
do
