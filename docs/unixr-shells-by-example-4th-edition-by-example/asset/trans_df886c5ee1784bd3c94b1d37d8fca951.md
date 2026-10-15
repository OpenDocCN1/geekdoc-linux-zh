

## 解释

+   1 echo 命令提示用户，Who was the 2nd U.S. president to be impeached? read 命令等待用户输入。输入将被存储在变量 answer 中。
+   2 进入 while 循环，测试命令，括号，测试表达式。如果变量 answer 不完全等于字符串 Bill Clinton，则进入循环体，并在 do 与 done 之间的命令被执行。
+   3 do 关键字是循环体的开始。
+   4 要求用户重新输入。
+   5 done 关键字标记循环体的结束。控制返回到 while 循环顶部，并再次测试表达式。只要 answer 不求值为 Bill Clinton，循环将继续迭代。当用户输入 Bill Clinton 时，循环结束。程序控制转到第 6 行。
+   6 当循环体结束时，控制从此处开始。

## 示例 14.39

(The Script)

```
$ cat sayit
#!/bin/bash
# Scriptname: sayit
echo Type q to quit.
go=start
1 while [[ -n "$go" ]]  # Make sure to double quote the variable
do
2     echo -n I love you.
3     read word
4     if [[ $word == [Qq] ]]
    then        # [ "$word" = -o "$word" = Q ]  Old style
        echo "I'll always love you!"
    go=
    fi
done
```

(The Output)

```
Type q to quit.
I love you.     <-- When user presses Enter, the program continues
I love you.
I love you.
I love you.
I love you.
I love you.q
I'll always love you!
$
```

## 解释

+   1 while 之后执行的命令被测试其退出状态。test 命令的 -n 选项测试非空字符串。因为变量 go 最初有值，测试成功，产生零退出状态。如果变量 go 未用双引号括起来且变量为空，test 命令会抱怨：
+   
+   go: test: argument expected
+   2 进入循环。将字符串 I love you 回显到屏幕。
+   3 read 命令等待用户输入。
+   4 测试表达式。如果用户输入 q 或 Q，则显示字符串 I'll always love you!，并且变量 go 被设为空。当重新进入 while 循环时，测试不成功，因为变量为空。循环终止。控制转到 done 语句之后的行。在此示例中，脚本将终止，因为没有更多行可执行。

### 14.6.4 until 命令

until 命令的使用方式与 while 命令类似，但仅当 until 之后的命令失败时才执行循环语句，即当命令返回非零退出状态时。当到达 done 关键字时，控制返回到循环顶部，until 命令再次检查命令的退出状态。直到 until 正在评估的命令的退出状态变为 0，循环才会继续。当退出状态达到 0 时，循环退出，程序执行从 done 关键字之后开始。

## 格式

```
until command
do
    command(s)
done
```

## 示例 14.40

```
#!/bin/bash
until who | grep linda
do
    sleep 5
done
talk linda@dragonwings
```

## 解释

1 until 循环测试管道中最后一个命令 grep 的退出状态。who 命令列出在此机器上登录的用户并将其输出通过管道传递给 grep。grep 命令只有在找到用户 linda 时才会返回 0 退出状态（成功）。

2 如果用户 linda 尚未登录，则进入循环体，程序休眠五秒。

3 当 linda 登录时，grep 命令的退出状态将为零，控制将转到 done 关键字之后的语句。

## 示例 14.41

```
(The Script)
#!/bin/bash
# Scriptname: hour

1 hour=0
2 until (( hour > 24 ))
do
3   case "$hour" in
    [0-9]|1[0-1]) echo "Good morning!"
    ;;
    12) echo "Lunch time."
    ;;
    1[3-7]) echo "Siesta time."
    ;;
    *) echo "Good night."
    ;;
  esac
4   (( hour+=1 ))  # Don't forget to increment the hour
5 done
```

(The Output)
Good morning!
Good morning!
...
Lunch time.
Siesta time.
...
Good night.
...

