

## 12.5.7 if 命令

最简单的条件形式是 if 命令。if 关键字后面的命令会被执行并返回其退出状态。如果退出状态为 0，则命令成功，then 关键字后面的语句将被执行。

在 C shell 和 C 语言中，if 命令后面的表达式是布尔型表达式。但在 Bourne 和 Korn shell 中，if 后面的语句是一个命令或一组命令。if 行的最后一个命令的退出状态用于确定是否继续并执行 then 语句下的命令。如果 if 行上最后一个命令的退出状态为 0，则执行 then 语句下的命令。fi 终止 then 之后要执行的命令列表。如果退出状态为非零，意味着命令以某种方式失败，则忽略 then 语句后的语句，控制转到 fi 语句之后的下一行。

条件命令可以嵌套。每个 if 必须有一个对应的 fi。fi 与最近的 if 配对。使用缩进来格式化你的 if 块有助于在调试程序时。

### FORMAT

```
if command
then  # Testing command exit status
    command
    command
fi
--------------------------------
if test expression
then  # Using the test command to test expressions
    command
fi

        or

if [ expression ]
then        # Using the old-style test command--
    command    # brackets replace the word test
fi
--------------------------------
if [[ expression ]]
then        # New-style brackets for testing expressions
    command
fi
--------------------------------
```

## EXAMPLE 12.18 (CONTINUED)

```
2 if [ "$answer" = Y -o "$answer" = y ]   # Old-style test
then
    print "Glad to hear it."
3 fi
```

### EXPLANATION

- 1 用户被问到问题，Are you ok (y/n) ?。read 命令会导致程序等待用户输入。
- 2 test 命令，由 [ 表示，用于测试表达式，如果表达式为真则返回退出状态 0，如果表达式为假则返回非零。如果变量 answer 的计算结果为 Y 或 y，则执行 then 语句后的命令。 （test 命令在测试表达式时不允许使用通配符。）
- 3 fi 终止 then 语句之后的一系列命令。

## 12.5.9 使用新式 Korn test

新式 Korn shell 测试允许表达式包含 shell 元字符和 Korn shell 运算符，如 && 和 ||。

### EXAMPLE 12.19

```
#!/bin/ksh
# Scriptname: are_you_ok2
1 print "Are you ok (y/n) ?"
read answer
2 if [[ "$answer" = [Yy]* ]]   # New-style test
then
    print "Glad to hear it."
3 fi
```

### EXPLANATION

- 1 用户被问到问题，Are you ok (y/n) ?。read 命令会导致程序等待用户输入。
- 2 [[ ]] 是用于测试表达式的特殊 Korn shell 构造。如果 answer 的计算结果为 Y 或 y 后跟任意数量的字符，则执行 then 语句后的命令。
- 3 fi 语句终止 if。

## 12.5.10 使用带数字的老式 Bourne test

要测试数值表达式，老式 Bourne shell test 命令及其运算符在 Korn shell 中仍然可以接受，但首选新式 let 命令。

### EXAMPLE 12.20

```
1 if [ $# -lt 1 ]
then
    print "$0: Insufficient arguments " 1>&2
    exit 1
2 fi
```

### EXPLANATION

- 1 该语句的含义是：如果参数数量小于 1，则打印错误消息并将其发送到标准错误。然后退出脚本。使用 test 命令使用旧式方法测试整数。
- 2 fi 标记 then 之后的一组语句的结束。

## 12.5.11 let 命令和测试数字

尽管使用单方括号和老式 Bourne shell 数值运算符来测试数值表达式仍然是可以接受的，但在 Korn shell 中测试数值表达式的首选方法是使用双括号和新的 C 语言风格的数值运算符。请注意，双括号仅用于测试字符串表达式和文件测试（请参阅表 12.10）。

### EXAMPLE 12.21

```
1 if (( $# < 1 ))
then
    print "$0: Insufficient arguments " 1>&2
    exit 1
2 fi
```

### EXPLANATION

- 1 该语句的含义是：如果参数数量小于 1，则打印错误消息并将其发送到标准错误。然后退出脚本。这是 Korn shell 中执行数值测试的首选方法。
- 2 fi 标记 then 之后的一组语句的结束。

