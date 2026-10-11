
## 教程

### Bash 大师课

![](img/628186dda7facdc011bf39c938de3975_29_0.png)

### 这是一个旋转木马！

发送多个文件要求我们熟悉 `for` 循环；它执行其命令体，直到传入的参数列表耗尽：

```bash
for file in `ls *.mp3` ; do
    echo "\$emailTitle File \$fileNow of \$fileCount"
    echo "\$file"
    fileNow=$((fileNow+1))
done
```

`for` 也可用于处理数字和/或数字范围。这是通过修改 $ 运算符或传入完整列表或声明来实现的 – 以下脚本输出两个数字序列：

```bash
for ((a=1; a<=10; a++)); do
    echo \$a;
done

for a in {1..10}; do
    echo \$a;
done
```

`for` 循环非常适合所有 shell 脚本需要处理一组预定义命令的情况。实际上，很少有程序享受在调用时已知任务集的特权 – 在大多数情况下，迭代必须进行直到任务完成。

遗憾的是，使用基于硬件的 `for` 循环示例并不吸引人，因为复用它们很困难。因此，我们将坚持混合示例 – 第一个示例计算一组输入数字的总和：

```bash
myval=22
accu=0
while [ \$myval != "q" ]; do
    read myval
    if [ \$myval != "q" ]; then
        let accu=accu+myval
    fi
done

echo \$accu
```

`while` 是头控循环的实现：如果这样的循环需要至少执行一次，开发者必须相应地设置参数。尾控循环在这种情况下提供了有吸引力的替代方案 – 该程序的另一种实现可以像这样：

```bash
accu=0
until [ [ \$myval == "q" ] ]; do
    read myval
    if [ \$myval != "q" ]; then
        let accu=accu+myval
    fi
done

echo \$accu
```

这段代码对于习惯 C 或 BASIC 的开发者来说可能看起来有点令人不安：在 Bash 中，尾控循环也是从循环控制表达式开始的。请注意，这只是一个语法差异 – 循环行为最好通过以下摘自 C 标准的片段来描述：

```c
do { statement(s); } while( condition );
```

### 不要重复自己

一遍又一遍地说同样的话很无聊；并非没有理由，许多（如果不是大多数）海盗船长肩上都有一只鹦鹉，向迟钝或醉酒的下属重复命令。

玩笑归玩笑：重复代码是第一类反模式。它导致了难以维护的程序，并在维护过程中产生错误。

这个问题最好通过函数来解决。让我们从查看 lineMaker 开始 – 它生成一行包含一些 ASCII 艺术的内容：

```bash
#!/bin/bash

anotherF() {
    echo "- - - - - - - - - - - - - - - - - -"
}

function drawline {
    anotherF
    anotherF
}

drawline
```

Bash 使处理函数变得有趣，因为它提供了两种语法变体；我们的代码片段使用 anotherF 的那一种，而另一种在 drawline 中演示。实际上运行代码可以像 drawline 是 Bash shell 命令集的一部分一样完成。

当然，函数可以通过负责调用它们的代码进行修改。这是通过参数实现的 – 让我们通过稍微修改划线程序来演示其用法：

```bash
function drawline {
    anotherF
    anotherF
    echo \$1
    echo \$1
}
```

```bash
drawline a b c d
```

调用此代码的新版本将导致以下结果：

```bash
tamhan@TAMHAN14:~/Desktop/bashspace$ ./runner.sh
-----------------------------------------
4
a
```

运行的函数可以访问一个名为 `#` 的变量 – 它包含传入参数的数量。然后可以通过名为 1, 2, 3 等变量访问实际参数。访问其内容涉及使用上一部分中讨论的 $4 运算符。

Bash 的 `return` 命令具有误导性，因为它不能用于向调用者返回实际值 – 相反，它仅限于处理数字状态码。返回值的一种有趣方法涉及使用“参数变量”：

```bash
function myfunc() {
    local _res=$1
    local myresult='Hello World'
    eval $_res=""$myresult""
}

myfunc result
echo $result
```

> “ 请注意，函数必须位于其第一次调用上方 – 如果不是这种情况，Bash 将在执行时抛出错误 ”

上述代码相当棘手，因为它使用了 eval 命令：它指示 Bash 首先解析传入的字符串，并在第二步中继续运行结果。因此 `$_res` 被转换为变量名，而包含 `&myresult` 的字符串保持不变。

请注意，函数必须位于其第一次调用上方 – 如果由于某种原因并非如此，Bash 将在执行时抛出错误。此外，请记住函数可以随时被覆盖 – 以下产物将产生非常奇怪的输出（见图）：

```bash
. . .
function drawline {
   anotherF
}
. . .

function drawline {
   echo "Ouch"!
}
```

![](img/628186dda7facdc011bf39c938de3975_30_0.png)

```bash
drawline a b c d
```

此外，你应该始终记住函数调用并不是特别快。虽然 Bash 允许创建递归函数，但不建议这样做 – 诸如计算阶乘之类的任务最好由 C 或 Fortran 处理。

### ShellCheck

Bash 的语法复杂得足以让经验丰富的程序员驻足：由于该语言在运行时被解释，错误通常只在为时已晚时才发现。

静态分析为此问题提供了解决方案。ShellCheck 是一个方便打包的程序，它检查你的 shell 脚本中一些众所周知的故障来源。

普通用户可以通过互联网访问该产品：在任意浏览器中打开 https://www.shellcheck.net，并将你的 shell 脚本粘贴到文件中。如果你希望更经常地使用该产品，可以通过 apt-get 本地安装它：

```bash
tamhan@TAMHAN14:~$ sudo apt-get install shellcheck
[Sudo] password for tamhan:
```

然后可以从命令行部署 ShellCheck – 非常机敏的开发者甚至会在每次保存文件后自动调用它。

### 结论与展望

虽然 Bash 脚本 – 承认 – 乍一看相当奇怪，但脚本语言仍然提供了完整的循环和选择命令集。这意味着 Bash 脚本是一种或多或少图灵完备的语言，理论上可以用于解决各种高级问题。

在实践中，由于各种原因，不建议这样做。首先，语法不宽容。其次，Bash 缺少各种高级结构，如指针和关联数组：这使得解决高级任务变得不必要地复杂。

幸运的是，Bash 将用其他语言编写的程序视为一等公民。本教程的下一部分将介绍各种链式命令和应用程序的方法 – 敬请期待，强大的力量在等着你！

### 使用现代保护编译软件

![](img/628186dda7facdc011bf39c938de3975_31_0.png)

**Toni Castillo Girona**

拥有软件工程学士学位，并担任西班牙加泰罗尼亚地区一所公立大学的 ICT 研究支持专家。他经常在他的博客上撰写有关 GNU/Linux 的内容：[disbaues.ups.es](http://disbaues.ups.es)

#### 资源

- Smashing the Stack for fun and profit
- http://tbit.ly/29pZpIF
-
- Debian Hardening
- https://wiki.debian.org/"Hardening"
-
- GDB Quick Reference
- http://tbit.ly/29o6CIn
-
- Running Shell-Code
- http://tbit.ly/29gYJ3a
-
- Relocation Read-Only
- http://tbit.ly/29a7Ov7

强化 GNU/Linux ELF 二进制文件可以防止基于内存破坏的攻击接管整个系统

**软件安全是一个复杂的专业知识领域。** 我们已告别了通过粉碎堆栈来获利轻而易举的鼎盛时期。如今，GNU/Linux 发行版开箱即带有针对内存破坏的现代保护，使得此类攻击的可能性降低。然而，即使开启这些保护，安全研究人员总是能找到利用软件缺陷的晦涩方法。强化你的二进制文件可以帮助你防止大多数这些攻击。GNU C 库和编译器提供了一些这些保护，而内核本身实现了其他保护。这些保护包括：DEP/NX、ASLR、Stack-Canaries、PIE 和 Full RELRO。现代 gcc 版本还包含一些有用的保护，例如将任何对 *strcpy* 系列函数的调用替换为长度受限的对应项（*strncpy*）。

##### NX 位

非执行位（NX）确保注入到 ELF 二进制文件非可执行段中的外来代码不会被执行。现代 64 位处理器开箱即包含此保护，并且 Linux 内核支持它。打开一个新的终端并运行此命令以了解你的处理器是否支持 NX：

```bash
cat /proc/cpuinfo |grep 'flags:head -1|grep --color=auto '(nx)'
```

此位可以在编译时通过向编译器传递 `-z execstack` 标志来清除。否则，默认情况下它是设置的。

拿起你喜欢的文本编辑器，写下这段代码：

```c
#include <stdio.h>
char shellcode[] =
"\x31\xc8\x31\xc9\x89\xc6\x31\xcd\xc8\x89"
"\x89\xf1\x5e\x89\xf6\x89\x89\xcb\x89"
"\xcb\x89\x89\x89\x88\x88\x88\x88\x89"
"\xc6\x88\xf7\xb8\xc7\xe8\x89\xc6\x89"
"\xcd\x89\xf1\xd6\x89\x89\x9d\x88\xc6"
"\x88\xe8\xc6\x88\xf1\xff\x1f\xff\x0b\x1f";
int main(int argc, char **argv) {
int *ret;

ret = (int *)ret + 2;
*(ret) = (int)shellcode;
}
```

这是一个执行 shell-code 的众所周知的技术。shell-code 存储在 *shellcode* 指向的地址中。该地址属于 .data 段。首先，像这样编译它：

```bash
$ gcc -m32 nx.c -o nx
```

如果你执行该二进制文件，你会得到一个段错误：

```bash
./nx
Segmentation fault
```

再次编译它，但这次清除 NX 位：

```bash
gcc -m32 -z execstack nx.c -o nx
./nx
sh-4.2$
sh-4.2$
```

shell-code 被执行，你获得了一个 shell。除了能够在编译时清除 NX 位外，你还可以使用 *execstack* 实用程序在现有的 ELF 二进制文件中这样做。在你的发行版中安装它：

```bash
#apt-get install execstack
```

在不清除 NX 位的情况下编译我们的示例并运行它：你会得到之前的段错误。但嘿，你现在有 *execstack*，所以你可以施展一些魔法：

```bash
# execstack -s nx
# ./nx
sh-4.2$
```

很酷：你可以随心所欲地使用 *execstack* 设置或清除 NX 位。现在

![](img/628186dda7facdc011bf39c938de3975_31_1.png)
