

# 示例 14.2（续）

```
5 ls  # List files in the present working directory
6 echo "Bye for now $LOGNAME. The time is `date +%T`!"
```

(The Command Line)
$ greetings  # Don't forget to turn on x permission!
bash: ./greetings: Permission denied.
$ chmod +x greetings
$ greetings or ./greetings

3
Hello barbara, it's nice talking to you.
Your present working directory is /home/lion/barbara/prog
You are working on a machine called lion.
Here is a list of your files.

+   5
+   Afile    cplus    letter    prac
+   Answerbook cprog library prac1
+   bourne    joke    notes    perl5

6
Bye for now barbara. The time is 18:05:07!

## 说明

+   1 脚本的第一行 #!/bin/bash 让内核知道将执行此程序中各行的解释器；在这种情况下，是 bash 解释器。
+   2 注释是以井号开头的不可执行行。它们可以单独占一行，也可以附加在命令之后的一行上。
+   3 在 shell 执行变量替换后，echo 命令将该行显示在屏幕上。
+   4 在 shell 执行命令替换后，echo 命令将该行显示在屏幕上。
+   5 执行 ls 命令。注释将被 shell 忽略。
+   6 echo 命令显示双引号内的字符串。变量和命令替换（反引号）在放在双引号内时会被展开。在这种情况下，引号其实并不是必要的。

## 14.2 读取用户输入

### 14.2.1 变量（复习）

在上一章我们谈到了声明和取消设置变量。变量可以设置为当前 shell 的局部变量或环境变量。除非你的 shell 脚本会调用另一个脚本，否则变量通常在脚本内设置为局部变量。（参见第 810 页的“变量”。）

要提取变量的值，请在变量前加上美元符号。你可以将变量用双引号括起来，美元符号将被 shell 解释为变量展开。如果变量被单引号括起来，则不会执行变量展开。

## 示例 14.3

```
1 names="John Doe" or declare name="John Doe"  # local variable
2 export NAME="John Doe"  # global variable
3 echo "$name" "$NAME"  # extract the value
```

### 14.2.2 read 命令

read 命令是内置命令，用于从终端或文件读取输入（参见表 14.1）。read 命令读取一行输入直到遇到换行符。行尾的换行符在读取时会被转换为空字节。如果没有提供名称，读取的行将被分配给特殊内置变量 REPLY。你也可以使用 read 命令使程序在用户按下 Enter 之前停止。要了解如何最有效地使用 read 命令从文件读取输入行，请参见第 903 页的“循环命令”。read 的 -r 选项会导致反斜杠/换行符对被忽略；反斜杠被视为行的一部分。read 命令有四个选项来控制其行为：-a、-e、-p 和 -r。

## 表 14.1 read 命令

| 格式 | 含义 |
|---|---|
| read answer | 从标准输入读取一行并将其分配给变量 answer |
| read first last | 从标准输入读取一行到第一个空白或换行符，将输入的第一个词放入变量 first，其余行放入变量 last |
| read | 从标准输入读取一行并将其分配给内置变量 REPLY（Bash 和 Korn shell） |
| read -a arrayname | 将一组词读入名为 arrayname 的数组中ᵃ |
| read -e | 用于启用命令行编辑的交互式 shell；例如，如果编辑器是 vi，则可以在输入行上使用 vi 命令ᵃ |
| read -p prompt | 打印提示符，等待输入，并将输入存储在 REPLY 变量中ᵃ |
| read -r line | 允许输入包含反斜杠ᵃ |

a. 未在 bash 2.0 之前的版本中实现。

2. 选项 -a、-e 和 -p 仅在 bash 2.x 版本中可用。

