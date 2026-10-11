
我现在将进入编写阶段，向你展示如何编写 Shell 脚本。该脚本的语言非常简单。请看以下脚本：

```bash
[gha@localhost ~]$ echo 'I am learning Linux'
I am learning Linux
```

这就是 Shell 脚本。现在我将在同一脚本中添加一个注释。

```bash
[gha@localhost ~]$ echo 'I am learning Linux' # I have added a comment to the code.
I am learning Linux
```

现在你需要使脚本可执行。请看以下内容：

```bash
[gha@localhost ~]$ ls -l Linux_learning
[gha@localhost ~]$ chmod 755 Linux_learning
```

文本 Linux_learning 是我保存该脚本的文件名。chmod 命令在 Linux 中用于使脚本可执行。

## 显示文本

大多数 Shell 命令都会产生特定的输出，这些输出会显示在你运行脚本的控制台监视器上。你可能需要添加文本消息，以帮助脚本用户了解脚本内部将发生的事情。你可以使用我在上一节中提到的 echo 命令来实现这一点。echo 命令可以显示简单的文本字符串。使用 echo 命令编写脚本有多种不同的技术。我将探索所有这些技术。

```bash
[gha@localhost ~]$ echo I am learning Linux shell scripting
I am learning Linux shell scripting
```

最值得注意的是，你不需要使用引号来包围字符串文本，这在其他编程语言中是常见的。然而，有时需要使用引号。你需要单引号或双引号来显示文本字符串。

```bash
[gha@localhost ~]$ echo 'I am learning Linux shell scripting.'
I am learning Linux shell scripting
```

在下一个示例中，使用引号将是不可避免的。

```bash
[gha@localhost ~]$ echo "Adam says, \"I am learning Linux shell scripting.\""
Adam says, "I am learning Linux shell scripting."
```

你可以看到，当你需要添加直接引语形式的文本时，你必须给文本添加引号。

## if-then 语句

许多 Linux Shell 脚本程序需要在脚本内部的不同命令之间进行某种逻辑流控制，这意味着 Shell 倾向于执行不同的命令。此外，它还保留了执行其他不同命令的能力，允许脚本根据其他不同命令的结果对命令进行循环。我们将它们称为结构化命令。它们也被称为条件语句。

结构化命令允许你改变程序操作的流程。当某些命令被特定的条件捕获时，一些命令会被执行，而另一些则被跳过。在其他编程语言中，if 语句后面的对象是系统用于评估真或假的等式。Bash Shell 的 if 语句不是这样工作的。相反，它执行在 if 行上定义的命令。如果该命令的退出状态被视为零，则列在 then 部分的命令将执行。如果该命令的退出状态是其他值，则 then 命令将被搁置，Bash Shell 会跳转到脚本中的下一个命令。

```bash
$ cat testing5
#!/bin/bash
# I am now testing the if statement for bash shell
if date
then
    echo "The structured command has completely worked"
fi

$ bash -f main.sh
Tue Jan 26 05:02:54 UTC 2021
The structured command has completely worked
```

该脚本在 if 行使用了 date 命令。如果该命令成功执行，echo 语句必须显示文本字符串。当你从命令行运行脚本时，你会得到与上述相同的结果。Shell 将执行 date 命令。由于退出状态为零，它还将执行列在 then 部分的 echo 语句。在下一个示例中，我将测试一个错误的命令，看看它是如何工作的。

```bash
$ cat testing2
#!/bin/bash
# It is time to run a test on a bad command
if hgjdksslh
then
    echo "it is not going to work"
fi
    echo "I cannot run the command because you're out of the if statement."

$ bash -f main.sh
    I cannot run the command because you're out of the if statement
```

由于上述命令是一个错误命令，它产生了一个非零的退出状态。Bash Shell 将跳过 then 部分中的 echo 语句。

## if-then-else 语句

if-then 语句提供了一种选项来确定命令是否成功。如果返回非零的退出状态码，Bash Shell 将转到下一个脚本命令。在这种情况下，如果我们能有另一组可以执行的命令就最好，这就是 if-then-else 语句发挥作用的地方。

如果 if 语句命令产生零退出状态码，则执行语句 then 部分的命令。如果返回非零的退出状态码，则执行语句 else 部分的命令。

```bash
$ cat testing4
#!/bin/bash
# I am now going to test the else section
testinguser=thisisabadtest
if grep $testinguser /etc/passwd
then
    echo "The files for user $testinguser are:"
    ls -a /home/$testinguser/b*
else
    echo "The user name $testinguser cannot be found on the system"
fi

$ ./test4
The user name thisisabadtest cannot be found on the system

$ bash -f main.sh
The user name thisisabadtest cannot be found on the system
```
有时，你可能需要检查脚本代码中的某些内容。与其使用单独的 if-then 语句，可以使用 else 语句的不同版本。这称为 elif，它通过后续的 if-then 语句继续 else 语句。它提供了一个不同的评估命令，这与第一个 if 语句非常相似。如果返回零的退出状态码，Bash Shell 将执行第二个 then 语句中的命令。

## 高级 if-then 功能

Linux 中有一个双括号命令，允许你在进行比较时整合一些高级数学公式。test 命令允许简单的比较操作。然而，双括号命令提供了更多数学符号，许多来自其他语言的程序员都在使用这些符号。

表达式项可以是任何形式的数学赋值或表达式。除了 test 命令使用的标准运算符外，双括号命令还提供了可供使用的额外运算符。

你还可以使用双括号命令的高级功能来进行字符串比较。双括号命令格式使用我们在 test 命令中使用过的标准字符串比较。它的不同之处在于模式匹配选项。你将能够定义需要与字符串值匹配的正则表达式。

```bash
$ cat testing2
#!/bin/bash
# I will now be using pattern matching
if [[ $MyUSER == r* ]]
then
    echo "Hello $MyUSER I know you from the days when you used to work in a restaurant in Europe."
else
    echo "Sorry, I have never seen you before. I don't know you."
fi

$ bash -f main.sh
Sorry, I have never seen you before. I don’t know you.
```

更常见的情况是，你可能会发现自己试图评估某些变量的值，以找出可能值集合中的特定值。在这种典型场景中，你可能会编写一个冗长的 if-then-else 语句，如下所示：

```bash
$ cat testing555
#!/bin/bash
# I am now looking for some possible values
if [ $MyUSER = "rich" ]
then
    echo "Welcome $MyUSER to the heavens on the earth."
    echo "Please enjoy your visit in plush green fields and lush green mountains. I wonder if you want to take a bath in the river beneath the valley."
elif [ $MyUSER = Jason ]
then
    echo "Welcome $MyUSER to the lakes of Madora."
    echo "Please enjoy your stay in the shining waters of Madora lakes. I hope you enjoy the resorts, the sun, the breeze, the food, and the drinks."
elif [ $MyUSER = Simra ]
then
    echo "Welcome $MyUSER to the lakes of Madora."
    echo "Please enjoy your stay in the shining waters of Madora lakes. I hope you enjoy the resorts, the sun, the breeze, the food, and the drinks."
elif [ $MyUSER = Linda ]
then
    echo "Don't forget to logout when you're done"
else
    echo "Sorry, you're not allowed here"
fi
```

## for 命令

在对一系列命令进行迭代时，编程中这是正常的做法。很多时候，你可能需要重复执行不同的命令。通常，你需要重复执行一堆命令，直到程序满足指定条件，例如处理目录内的文件或文本文件中的所有行。

Bash Shell 提供 for 命令来开发一个遍历值集的循环。每次迭代倾向于通过使用系列中的单个值来执行一组命令。for 命令最基本的使用之一是在 for 命令本身内部定义的列表中的值进行迭代。

```bash
$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
for mytest in Alabama Texas Alaska Virginia Arizona Ohio Arkansas South Dakota California North Dakota Colorado New Jersey Florida Michigan
```

