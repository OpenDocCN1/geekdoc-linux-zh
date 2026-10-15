
# 13. `for`、`while` 还有 `until` 差在哪

## Shell 十三问之 13：`for` what？`while` 与 `until` 差在哪？

终于，来到了 Shell 十三问的最后一问了……长长吐一口气~~~~

最后要介绍的是 Shell Script 设计中常见的`循环`（`loop`）。所谓的`loop`就是 Script 中的一段在一定条件下反复执行的代码。

Bash Shell 中常用的`loop`有如下三种：

- `for`
- `while`
- `until`

## 1. `for` loop

`for` loop 是从一个清单列表中读进变量的值，并依次循环执行`do`到`done`之间的命令行。例：

```bash
for var in one two three four five
do
    echo -----------------
    echo '$var is '$var
    echo
done
```

> 上例的执行结果将会是：
>
> 1. `for` 会定义一个叫`var`的变量，其值依次是`one`、`two`、`three`、`four`、`five`。
> 2. 因为有 5 个变量值，因此，`do`与`done`之间的命令行会被循环执行 5 次。
> 3. 每次循环均用`echo`产生 3 个句子。而第二行中不在 hard quote 之内的`$var`会被替换。
> 4. 当最后一个变量值处理完毕，循环结束。

我们不难看出，在`for` loop 中，变量值的多寡决定循环的次数。然而，变量在循环中是否使用则不一定，得视设计需求而定。

倘若`for` loop 没有使用`in`这个 keyword 来制定变量清单的话，其值将从`$@`（或`$*`）中继承：

```bash
for var; do
    ......
done
```

> **Tips：**
>
> 若你忘记了`positional parameter`，请温习第九章……

`for` loop 用于处理“清单”（list）项目非常方便，其清单除了明确指定或从`positional parameter`取得之外，也可以从`变量替换`或者`命令替换`取得……（再一次提醒：别忘了命令行的“重组”特性。）

然而，对于一些“累计变化”的项目（整数的加减），`for`也能处理：

```bash
for ((i = 1; i
```

## 2. `while` loop

除了`for` loop，上面的例子我们也可改用`while` loop 来做到：

```bash
num=1
while [ "$num" -le 10 ]; do
    echo "num is $num"
    num=$(($num + 1))
done
```

`while` loop 的原理与`for` loop 稍有不同：它不是逐次处理清单中的变量值，而是取决于`while`后面的命令行的 return value：

- 若为 true，则执行`do`与`done`之间的命令，然后重新判断`while`后的 return value。
- 若为 false，则不再执行`do`与`done`之间的命令而结束循环。

> 分析上例：
>
> 1. 在`while`之前，定义变量`num=1`。
> 2. 然后测试（`test`）`$num`是否小于或等于 10。
> 3. 结果为 true，于是执行`echo`并将`num`的值加 1。
> 4. 再作第二轮测试，此时`num`的值为`1+1=2`，依然小于或等于 10，因此为 true，循环继续。
> 5. 直到`num`为`10+1=11`时，测试才会失败……于是结束循环。

我们不难发现：**若`while`的测试结果永远为 true 的话，那循环将一直永久执行下去**：

```bash
while :; do
    echo looping...
done
```

上面的`:`是 Bash 的 null command，不做任何动作，除了返回 true 的 return value。因此这个循环不会结束，称作死循环。

死循环的产生有可能是故意设计的（如跑 daemon），也可能是设计的错误。

若要结束死循环，可通过 signal 来终止（如按下`ctrl-c`）。（关于 process 与 signal，等日后有机会再补充，十三问略过。）

## 3. `until` loop

一旦你能够理解`while` loop 的话，那就能理解`until` loop：**与`while`相反，`until`是在 return value 为 false 时进入循环，否则结束。**因此，前面的例子我们也可以轻松地用`until`来写：

```bash
num=1
until [ ! "$num" -le 10 ]; do
    echo "num is $num"
    num=$(($num + 1))
done
```

或者：

```bash
num=1

until [ "$num" -gt 10 ]; do
    echo "num is $num"
    num=$(($num + 1))
done
```

Okay，关于 Bash 的三个常用的 loop 暂时介绍到这里。

## 4. Shell loop 中的 `break` 与 `continue`

在结束本章之前，再跟大家补充两个 loop 有关的命令：

- `break`
- `continue`

这两个命令常用在复合式循环里，也就是`do ... done`之间又有更进一层的 loop，当然，用在单一循环中也未尝不可啦……^_^

`break`用来中断循环，也就是强迫结束循环。若`break`后面指定一个数值`n`的话，则从里向外中断第`n`个循环，预设值为`break 1`，也就是中断当前循环。在使用`break`时，需要注意的是，它与`return`及`exit`是不同的：

- `break`是结束 loop；
- `return`是结束 function；
- `exit`是结束 script/shell。

而`continue`则与`break`相反：强迫进入下一次循环动作。

若你理解不来的话，那你可简单地看成：在`continue`在`done`之间的句子略过而返回到循环的顶端……

与`break`相同的是：`continue`后面也可以指定一个数值`n`，以决定继续哪一层（从里往外计算）的循环，预设值为`continue 1`，也就是继续当前的循环。

在 Shell Script 设计中，若能善用 loop，将能大幅度提高 Script 在复杂条件下的处理能力。请多加练习吧……

## Shell 十三问的总结语

好了，该是到了结束的时候了。婆婆妈妈地跟大家啰嗦了一堆 Shell 的基础概念。

目的不是要告诉大家“答案”，而是要带给大家“启发”……

在日后的关于 Shell 的讨论中，我或许经常用“连接”的方式指引十三问中的内容。

以便我们在进行技术探讨时，彼此能有一些讨论的基础，而不至于各说各话、徒费时力。

但更希望十三问能带给你更多的思考与乐趣，至为重要的是通过实践来加深理解。

是的，我很重视**实践**与**独立思考**这两项学习要素。

若你能够掌握其中的真谛，那请容我说声：**恭喜十三问你没白看了** ^_^

P.S. 至于补充问题部分，我暂时不写了。而是希望：

1. 大家补充题目。
2. 一起来写心得。

Good luck and happy studying！

## Shell 十三问原作者`网中人`签名中的 Bash fork bomb

最后，Markdown 整理者补上本书的原作者`网中人`的个性签名：

> **君子博学而日叁省乎己，则知明而行无过矣。**

一个能让系统 Shell 崩溃的 Shell 片段：

```bash
:() { :|:& }; :
```

原来是一个 Bash 的 fork 炸弹：参考：[`en.wikipedia.org/wiki/Fork_bomb`](http://en.wikipedia.org/wiki/Fork_Bomb)

整理后的代码：

```bash
:() {
    :|:&
}
:
```

> 代码分析：
>
> （即除最后一行外）
>
> 定义了一个 Shell 函数，函数名是`:`。
>
> 而这个函数体执行一个后台命令`:`|`:`。
>
> 即冒号命令（或函数，下文会解释）的输出通过管道再传给冒号命令做输入。
>
> 最后一行执行“`:`”命令。

在各种 Shell 中运行结果分析：

> 这个代码只有在 **Bash** 中执行才会出现不断创建进程而耗尽系统资源的严重后果；
>
> 在 `ksh`（Korn Shell）、`sh`（Bourne Shell）中并不会出现；
>
> 在 `ksh88` 和传统 Unix Bourne Shell 中冒号不能做函数名；
>
> 即便是在 Unix-Center FreeBSD 系统中的`sh`和`pdksh`（`ksh93`手边没有，没试）中冒号可以做函数名，但还是不会出现那个效果。
>
> 原因是`sh`、`ksh`中内置命令的优先级高于函数，所以执行“`:`”，总是执行内置命令“`:`”而不是刚才定义的那个恐怖函数。
>
> 但是在 **Bash** 中就不一样，Bash 中函数的优先级高于内置命令，所以执行“`:`”结果会导致不断的递归，而其中有管道操作，这就需要创建两个子进程来实现，这样就会不断地创建进程而导致资源耗尽。

众所周知，Bash 是一款极其强大的 Shell，提供了强大的交互与编程功能。

这样的一款 Shell 中自然不会缺少“函数”这个元素来帮助程序进行模块化的高效开发与管理。于是产生了由于其特殊的特性，Bash 拥有了 fork 炸弹。

Jaromil 在 2002 年设计了最为精简的一个 fork 炸弹的实现。

> 所谓 fork 炸弹是一种恶意程序，它的内部是一个不断在 fork 进程的无限循环。
>
> fork 炸弹并不需要有特别的权限即可对系统造成破坏。
>
> fork 炸弹实质是一个简单的递归程序。
>
> 由于程序是递归的，如果没有任何限制，这会导致这个简单的程序迅速耗尽系统里面的所有资源。
