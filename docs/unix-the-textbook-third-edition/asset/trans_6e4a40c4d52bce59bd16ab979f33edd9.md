

```
then
    echo -n "$user:   "
    grep "^""echo $user:":" /etc/passwd | cut -f5 -d':'
fi
done
exit 0
$ ./user_info dheckman ghacker sarwar
dheckman:  Dennis R. Heckman
ghacker:   George Hacker
sarwar:    Syed Mansoor Sarwar
$
```

## 12.6.3 while 语句

while 语句，也称为 while 循环，允许根据表达式的条件重复执行一段代码。以下是该语句的简要说明。

```
SYNTAX
while expression
do
    command-list
done

Purpose: To execute commands in command-list as long as expression evaluates to true
```

表达式会被求值，如果求值结果为真，则 command-list 中的命令会被执行，然后再次对表达式求值。这种表达式求值和执行 command-list 的序列，被称为一次迭代，会重复进行，直到表达式求值为假。此时，控制流会退出 while 语句并执行 done 之后的语句。图 12.5 描述了 while 语句的语义。

为了使循环表现良好，即最终终止并允许脚本中其余代码的执行，表达式中导致真值的变量和/或条件必须在 command-list 中的命令中得到正确处理。表达式始终求值为真的循环被称为非终止循环或无限循环。无限循环通常是由于设计和/或编程不当造成的，是不期望的，因为它们会持续占用 CPU 时间而没有任何有用的任务。然而，一些应用程序确实需要无限循环。例如，为 HTTP 服务等互联网服务提供服务的服务器都是无限期运行的程序，等待客户端请求。例如在 HTTP 服务的情况下，客户端请求通过 Web 浏览器（即 HTTP 客户端）如 Mozilla Firefox 发出。一旦服务器接收到客户端请求，它会处理请求，向客户端发送响应，然后等待下一个客户端请求。终止具有无限循环的进程的唯一方法是通过使用 kill 命令杀掉它。或者，如果进程在前台运行，按下

![](img/02e070097d401d3bf7de4bf1c470b267_522_0.png)

图 12.5 while 语句的语义。

<Ctrl+C> 也能奏效，除非进程被设计为忽略 <Ctrl+C>。在这种情况下，你需要通过按下 <Ctrl+Z> 将进程放到后台，然后使用 kill -9 命令终止它。有关进程的详细信息请参见第 10 章。

while_demo 文件中的脚本展示了 while 循环的简单用法。当你运行此脚本时，secretcode 变量被初始化为 agent007，并且会提示你进行猜测。你的猜测存储在本地变量 yourguess 中。如果你的猜测不是 agent007，while 循环的条件为真，do 和 done 之间的命令将被执行。此程序会礼貌地显示一条信息告知你猜错了，并提示你再次猜测。你的猜测再次存储在 yourguess 变量中，并对循环条件进行测试。此过程会一直持续，直到你输入 agent007 作为猜测。此时，循环条件变为假，控制流退出 while 语句。done 之后的 echo 命令会执行，祝贺你成为优秀基因库的一员！

```
$ cat while_demo
#!/bin/sh
secretcode=agent007
echo "Guess the code!"
echo -e "Enter your guess: \c"
read yourguess
```

```
while [ "$secretcode" != "$yourguess" ]
do
	echo "Good guess but wrong. Try again!"
	echo -e "Enter your guess: \c"
	read yourguess
done
echo "Wow! You are a genius!!"
exit 0
$ ./while_demo
Guess the code!
Enter your guess: star wars
Good guess but wrong. Try again! Enter your guess: columbo
Good guess but wrong. Try again! Enter your guess: agent007
Wow! You are a genius!!
$
```

## 12.6.4 until 语句

until 语句的语法与 while 语句相似，但其语义不同。而 while 语句的循环体在表达式求值为真时执行，在 until 语句中，循环体在表达式求值为假时执行。以下是该语句的简要说明。

```
SYNTAX
until expression
do
	command-list
done

Purpose: To execute commands in command-list as long as expression evaluates to false
```

图 12.6 说明了 until 语句的语义。until_demo 文件中的代码执行与 while_demo 文件中的脚本相同的任务（参见第 12.6.3 节），但它使用 until 语句而不是 while 语句。因此，do 和 done 之间的代码（循环体）只要你的猜测不是 agent007 就会被执行。

```
$ cat until_demo
#!/bin/sh
secretcode=agent007
echo "Guess the code!"
echo -n "Enter your guess: "
read yourguess
until [ "$secretcode" = "$yourguess" ]
do
echo "Good guess but wrong. Try again!"
echo -n "Enter your guess: "
```

