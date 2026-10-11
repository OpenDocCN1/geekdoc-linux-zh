
echo "向你致敬，表示尊重！"
else
echo "欢迎参加本课程！"
fi

kali@kali:~$ chmod +x ./elif.sh

kali@kali:~$ ./elif.sh
What is your age: 65
Hats off to you, respect!

示例 152 - 在 Bash 中使用 elif 语句

在这个例子中，代码执行流程稍微复杂一些。按照操作顺序，如果输入的年龄小于十六岁，则执行 *then* 分支；如果年龄大于六十岁，则进入 *elif* 分支（并显示“向你致敬”消息）；只有当年龄大于十六岁但小于六十岁时，*else* 分支才会执行。

## 5.4 布尔逻辑操作

布尔逻辑运算符，¹¹⁸ 如 *AND*（**&&**）和 *OR*（**||**）有些神秘，因为 Bash 以多种方式使用它们。

一种常见用途是在*命令列表*中，这些是由运算符控制流程的命令链。“**|**”（管道）符号是命令列表中常用的运算符，它将一个命令的输出传递给另一个命令的输入。类似地，布尔逻辑运算符根据前一个命令是否成功（返回 *True* 或 *0*）或失败（返回 *False* 或非零值）来执行命令。

让我们先看看 *AND*（**&&**）布尔运算符，它仅在前一个命令成功（或返回 *True* 或 *0*）时执行命令：

kali@kali:~$ user2=kali

kali@kali:~$ grep $user2 /etc/passwd && echo "$user2 found!"
kali:x:1000:1000::,/home/kali:/bin/bash
kali found!

kali@kali:~$ user2=bob

kali@kali:~$ grep $user2 /etc/passwd && echo "$user2 found!"

示例 153 - 在命令列表中使用 AND（**&&**）布尔运算符

在这个例子中，我们首先将我们要搜索的用户名赋值给 *user2* 变量。接下来，我们使用 **grep** 命令检查某个用户是否列在 */etc/passwd* 文件中，如果是，**grep** 返回 *True* 并执行 **echo** 命令。但是，当我们尝试搜索我们已知在 */etc/passwd* 文件中不存在的用户时，我们的 **echo** 命令没有执行。

¹¹⁸ (MIT). https://lilbguides.mit.edu/c.php?g=175963&p=1158594

在命令列表中使用时，OR（||）运算符是 AND（&&）的反义；它仅在前一个命令失败（返回 False 或非零值）时执行下一个命令：

kali@kali:~$ echo $user2
bob

kali@kali:~$ grep $user2 /etc/passwd && echo "$user2 found!" || echo "$user2 not found!"
bob not found!

示例 154 - 在命令列表中使用 OR（||）布尔运算符

在上面的例子中，我们将之前的命令向前推进了一步，添加了 OR（||）运算符，随后是第二个 **echo** 命令。现在，当 **grep** 没有找到匹配的行并返回 *False* 时，OR（||）运算符之后的第二个 **echo** 命令会被执行。

这些运算符还可以用于测试中，以比较变量或其他测试的结果。这样使用时，**AND**（&&）结合两个简单条件，如果它们*都*为真，则组合结果为成功（或 *True* 或 0）。

考虑这个例子：

kali@kali:~$ cat ./and.sh
#!/bin/bash
# and example

if [ $USER == 'kali' ] && [ $HOSTNAME == 'kali' ]
then
	echo "多个语句为真！"
else
	echo "没什么可看的..."
fi

kali@kali:~$ chmod +x ./and.sh

kali@kali:~$ ./and.sh
多个语句为真！

kali@kali:~$ echo $USER && echo $HOSTNAME
kali
kali

示例 155 - 使用 and（&&）布尔运算符在 Bash 中测试多个条件

在这个例子中，我们使用 **AND**（&&）测试多个条件，由于两个变量比较都为真，整个 *if* 语句成功，因此 *then* 分支执行。

在测试中使用时，OR（||）布尔运算符用于测试一个或多个条件，但*只有一个*条件为真即可算作成功。

让我们看一个例子：

kali@kali:~$ cat ./or.sh
#!/bin/bash
# or example

if [ $USER == 'kali' ] || [ $HOSTNAME == 'pwn' ]

then
	echo "一个条件为真，这行将被打印"
else
	echo "你没运气！"
fi

kali@kali:~$ chmod +x ./or.sh

kali@kali:~$ ./or.sh
一个条件为真，这行将被打印

kali@kali:~$ echo $USER && echo $HOSTNAME
kali
kali

示例 156 - 使用 or（||）布尔运算符在 Bash 中测试多个条件

在这个例子中，我们使用 **OR（||）** 测试多个条件，由于其中一个变量比较为真，整个 *if* 语句成功，因此 *then* 分支执行。

## 5.5 循环

在计算机编程中，*循环*¹¹⁹ 帮助我们完成需要重复运行直到满足特定标准的任务。迭代对于渗透测试人员特别有用，因此我们建议非常仔细地阅读本节。

在 Bash 中，两种最主要的循环命令是 *for*¹²⁰ 和 *while*。¹²¹ 我们将查看两者。

### 5.5.1 For 循环

*For* 循环非常实用，并且在 Bash 单行命令中工作得很好。¹²² 这种类型的循环用于对列表中的每个项目执行一组给定的命令。让我们简要查看其一般语法：

for var-name in <list>
do
	<要执行的操作>
done

示例 157 - for 循环的一般语法

*For* 循环将按顺序获取 *list* 中的每个项目，将该项目分配为变量 *var-name* 的值，执行 *do* 和 *done* 之间给定的操作，然后返回顶部，获取列表中的下一个项目，并重复步骤，直到列表用尽。

让我们看一个更实际的例子，它将快速打印 10.11.1.0/24 子网中的前 10 个 IP 地址。¹²³

kali@kali:~$ for ip in $(seq 1 10); do echo 10.11.1.$ip; done
10.11.1.1
10.11.1.2
10.11.1.3
10.11.1.4
10.11.1.5
10.11.1.6
10.11.1.7
10.11.1.8
10.11.1.9
10.11.1.10

示例 158 - 在 Bash 中使用 for 循环的示例

在这个 Bash 单行命令（示例 158）中，我们使用 **seq** 命令打印一系列数字，在此情况下是 1 到 10。每个数字随后被赋值给 *ip* 变量，然后随着 *for* 循环多次运行，每个 IP 地址显示在屏幕上，直到序列结束。

重写之前 *for* 循环的另一种方法是使用范围进行*花括号扩展*¹²⁴。¹²⁵ 使用范围的花括号扩展通过给出范围的首尾值来编写，可以是数字或字符的序列。这被称为“序列表达式”。

kali@kali:~$ for i in {1..10}; do echo 10.11.1.$i;done
10.11.1.1
10.11.1.2
10.11.1.3
10.11.1.4
10.11.1.5
10.11.1.6
10.11.1.7
10.11.1.8
10.11.1.9
10.11.1.10

示例 159 - 在 Bash 中使用范围进行花括号扩展

这种类型的循环有很大的潜力。将 IP 地址显示在屏幕上可能看起来没什么用，但我们可以使用相同的循环来使用 **nmap**¹²⁷ 运行端口扫描¹²⁶（我们在另一个模块中详细讨论）。我们也可以尝试使用 **ping** 命令查看是否有任何 IP 地址响应 ICMP 回显请求，¹²⁸ 等等。

¹²³ (Cisco, 2016), https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html
¹²⁴ (GNU, 2019), https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html
¹²⁵ (Bash Hackers Wiki, 2014), http://wiki.bash-hackers.org/syntax/expansion/brace
¹²⁶ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Port_scanner
¹²⁷ (Nmap, 2019), http://nmap.org/
¹²⁸ (Firewall.cx, 2018), http://www.firewall.cx/networking-topics/protocols/icmp-protocol/152-icmp-echo-ping.html

### 5.5.2 While 循环

While 循环也比较常见，在表达式为真时执行代码。While 循环格式简单，并且像 *if* 一样，使用方括号（[]）进行测试：

while [ <某测试> ]
do
	<执行一个操作>
done

示例 160 - while 循环的一般语法

让我们用 *while* 循环重新创建之前的例子：

kali@kali:~$ cat ./while.sh
#!/bin/bash
# while loop example

counter=1

while [ $counter -lt 10 ]
do
	echo "10.11.1.$counter"
	((counter++))
done

kali@kali:~$ chmod +x ./while.sh
kali@kali:~$ ./while.sh
10.11.1.1
10.11.1.2
10.11.1.3
10.11.1.4
10.11.1.5
10.11.1.6
10.11.1.7
10.11.1.8
10.11.1.9

示例 161 - 在 Bash 中使用 while 循环

这不是我们期望的输出。这是一个常见的错误，称为“*差一*”¹²⁹ 错误。在上面的例子中，我们使用了 *-lt*（小于）而不是 *-le*（小于或*等于*），因此我们的计数器只到了九，而不是原本打算的十。

((counter++)) 行使用双括号 ((...))¹³⁰ 结构同时执行算术扩展和求值。在这种情况下，我们用它来将 *counter* 变量增加 1。让我们重写 *while* 循环并再次尝试该例子：

kali@kali:~$ cat ./while2.sh
#!/bin/bash
# while loop example 2

¹²⁹ [Stack Overflow, 2019], https://stackoverflow.com/questions/2939869/what-is-exactly-the-off-by-one-errors-in-the-while-loop

¹³⁰ [Advanced Bash-Scripting Guide, 2014], http://tldp.org/LDP/abs/html/dblparens.html

