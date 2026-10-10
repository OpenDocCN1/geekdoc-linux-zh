
```c
/********************************************
* C Programming in Linux (c) David Haskins 2008
* chapter1_3.c
********************************************/

#include <stdio.h>

int main(int argc, char *argv[]) 
{
    int i=0;

    printf("Content-type:text/plain\n\n");
    printf("Hello, you are still learning C!\n");
    printf("Number of arguments to the main function:%d\n", argc);
    for(i=0;i<argc;i++)
    {
        printf("argument number %d is %s\n", i, argv[i]);
    }
    return 0;
}
```

打开网络浏览器，输入 URL `http://localhost/cgi-bin/hello3?david+haskins`，你会发现 web 内容可以由 C 程序生成。

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_18_0.png)

### 1.4 第四个 Hello 程序

`main` 函数签名的一个鲜为人知的特性是它可以接受三个参数，我们现在将看到的是最后一个参数：`char *env[]`。它也是一个字符串指针列表，但在这种情况下，这些是程序运行时可用的系统环境变量。

```c
/********************************************
* C Programming in Linux (c) David Haskins 2008
* chapter1_4.c
********************************************/
#include <stdio.h>

int main(int argc, char *argv[], char *env[])
{
    int i=0;

    printf("Content-type:text/plain\n\n");
    printf("Hello, you are still learning C!\n");
    printf("Number of arguments to the main function:%d\n", argc);
    for(i=0;i<argc;i++)
    {
        printf("argument number %d is %s\n", i, argv[i]);
    }
    i = 0;
    printf("Environment variables:\n");
    while(env[i])
    {
        printf("env[%d] = %s\n", i, env[i]);
        i++;
    }
    return 0;
}
```

使用 `gcc -o hello4 chapter1_4.c` 进行编译，并以超级用户身份将程序复制到 `/srv/www/cgi-bin`（OpenSuse）或 `/usr/lib/cgi-bin`（Ubuntu）。你可以从终端中通过 `./hello4` 运行此程序，你会看到一长串环境变量。在浏览器中输入 `http://localhost/cgi-bin/hello4` 时，你会看到一组完全不同的变量。

> 维基百科对“环境变量”的定义如下：
>
> “在所有 Unix 和类 Unix 系统中，每个进程都有自己的一套私有环境变量。默认情况下，当创建一个进程时，它会继承其父进程的副本环境，除了父进程在创建子进程时所做的明确更改........ 所有 Unix 操作系统变种以及 DOS 和 Microsoft Windows 都有环境变量；然而，它们并不都使用相同的变量名。运行的程序可以访问环境变量的值以用于配置目的。环境变量的示例包括..... `PATH`, `HOME`... “

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_20_0.png)

我们将很快发现，`QUERY_STRING` 是我们与程序通信的重要环境变量，在这种情况下，我们看到它的值是 “david+haskins”，即我们在 URL 中输入的 “?” 之后的所有内容。向诸如 `hello4` 这样的通用网关接口（CGI）程序发送信息的有效方式，但我们应该将其限制为一个字符串。在我们的例子中，我们使用了 “+” 连接两个字符串。如果我们输入：“david haskins”，浏览器会对其进行转义，我们会看到：

```
QUERY_STRING=david%20haskins
```

我们将稍后学习如何将复杂的输入值集合传输给我们的程序。

### 1.5 Hello World 总结

我们看到，一个带有少量输入和一些输出的简单程序实际上是非常强大的，因为它揭示并暴露了我们计算机内部的大量工作原理。

尽管我们才刚刚开始，但已经遇到了许多我们将反复使用的关键概念：

- 函数和参数
- 作为数据类型的数字（整数）和字符字符串
- 列表或数组
- 使用 `for` 和 `while` 的循环

我们特意采取了巨大的飞跃，从编写仅在“终端屏幕”中运行的程序，过渡到可以在互联网浏览器中可见的程序。

这样做的原因是，编写与用户交互的程序（在 `Windows`、`Gnome` 或 `KDE` 等窗口系统中）过程极其复杂，而且你不太会经常被要求这样做。

互联网浏览器如今已成为我们几乎所有操作的事实接口模式，因此我们不妨从一开始就理解如何使用它。

在后续的所有章节中，我们将遵循这一模式：从某些基本技术开始，然后将其应用于基于 Web 的系统。

实际上，并没有太多真正的现实世界 C 语言通用网关接口编程在进行中，但确实有大量基于 C 和 `C++` 的代码作为 `Apache` 模块和 `Microsoft IIS` `ISAPI` `Dlls` 运行。也许很多人不知道，`Ebay` 的大部分代码是用 C / `C++` 编写的。

为什么？因为它具有极致的速度，而他们在全球实时市场中与抢购者的业务需要这种闪电般快速的核心，因此没有其他方法能获得这种性能。

# 2 数据和内存

## 2.1 简单数据类型

当我们编写程序时，在声明和描述变量以表征我们想要包含在信息处理中的事物类型时，必须对世界的本质做出决定或断言。

这个过程具有深刻的哲学意义；我们做出**本体论**断言，认为此物或彼物存在；当我们选择特定的数据类型或数据类型集合来描述这些事物的属性时，我们做出**认识论**断言。这是沉重的话题，伴随着巨大的责任，不可轻率行事。

作为一个实际例子，我们可能声明一个看起来像地理数据库记录开头的东西。

```c
/********************************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter2_1.c
 * ******************************************************************/

#include <stdio.h>
#define STRINGSIZE 256

int main(int argc, char *argv[])
{
    char town[STRINGSIZE] = "Guildford";
    char county[STRINGSIZE] = "Surrey";
    char country[STRINGSIZE] = "Great Britain";
    int population = 66773;
    float latitude = 51.238599;
    float longitude = -0.566257;
    printf("Town name: %s  population:%d\n",town,population);
    printf("County: %s\n",county);
    printf("Country: %s\n",country);
    printf("Location latitude: %f longitude: %f\n",latitude,longitude);
    printf("char = %d byte int = %d bytes float = %d bytes\n",
    sizeof(char),sizeof(int),sizeof(float) );
    printf("memory used:%d bytes\n",
    ((STRINGSIZE * 3) * sizeof(char) + sizeof(int) + (2 * sizeof(float)));
    return 0;
}
```

在此我们执行以下操作：

- 断言我们在此应用程序中遇到的所有字符字符串都将限制在 255 个字符以内，因此我们通过**预处理器**语句来**定义**这一点——这些语句以 `#` 开头。
- 断言城镇与郡相关联，郡与国在某些层级方式上相关联。
- 断言人口以整数计数——没有半个人。
- 断言位置将以特定的变体（`WGS84`）进行记录，这是描述地球表面位置的一种基于经纬度的惯例，该惯例使用小数来表示度、分和秒。

每个这样的语句都会在其声明所在函数的**作用域**内分配**内存**。每个**数据声明**将占用一定量的以**字节**为单位的内存，并为该部分内存赋予一个标签，即*变量名*。每种数据类型都有指定的大小，且 `sizeof()` 库函数将返回此整数。在这种情况下，是 $3 \times 256$ 个字符、一个整数和两个浮点数。确切大小取决于机器，但可能是 780 字节。

在数据声明所在的函数之外，这些数据是无法访问的——这就是声明的**作用域**。如果我们在 `main()` 函数外部声明，它的作用域将是**全局**的，其他函数就可以访问它。C 语言允许你这样做这种危险的操作，如果你愿意的话，所以请小心。

通常，我们会密切关注数据的作用域，并将**只读副本**或指向数据的**带标签的内存地址**传递给程序中可能需要对其执行操作甚至修改操作的部分。这些带标签的内存地址被称为**指针**。

我们在输出中使用 `printf` 系列库函数（`sprintf` 用于创建字符串，`fprintf` 用于写入文件等），它们都使用共同的**格式字符串**参数来指定数据的表示方式。

- `%c` 字符
- `%s` 字符串
- `%d` 整数
- `%f` 浮点数 等等

参数中剩余的变量序列将按照指定顺序放入格式字符串中。

在 C 语言中，**初始化**你声明的任何数据是个好主意，因为为它们分配的内存内容未被清除，可能包含任意旧的垃圾数据。

编译命令：`gcc -o data1 chapter2_1.c -lc`

调用时程序的输出：`./data1`

```text
Town name: Guildford population: 66773
County: Surrey
Country: Great Britain
Location latitude: 51.238598 longitude: -0.566257
char = 1 byte int = 4 bytes float = 4 bytes
memory used: 780 bytes
```

## 关于 make 有用工具的一个说明

到现在为止，你可能已经厌倦了输入所有这些编译器命令，因此有一个名为 `make` 的工具，它在一个名为 `Makefile` 的文件上运行，该文件位于存储代码的文件夹中。以下是迄今为止示例的 Makefile：

```makefile
#Makefile
all: chap1 chap2
chap1: 1-1 1-2 1-3 1-4
1-1:
	gcc -o hello1 chapter1_1.c -lc
1-2:
	gcc -o hello2 chapter1_2.c -lc
1-3:
	gcc -o hello3 chapter1_3.c -lc
1-4:
	gcc -o hello4 chapter1_4.c -lc
chap2: 2-1 2-2
2-1:
	gcc -o data1 chapter2_1.c -lc
2-2:
	gcc -o data2 chapter2_2.c -lc
clean:
	rm hello* data* *~
```

要编译所有内容，输入 `make all`。

要编译 `chapter2_1.c` 的目标 `2-1`，输入 `make 2-1`。

每个 `make` 目标后的制表符对于 `make` 的语法至关重要。

代码包中包含用于整本书的 `Makefile`。

## 2.2 什么是字符串？

像 `Java` 和 `C++` 这样的编程语言拥有字符串数据类型，隐藏了看似简单事物下面的一些复杂性。

字符字符串的一个基本属性是，它是由长度不确定的单个字符元素组成的序列。

我们可以键入键盘的大多数单个字符都由简单的数值 `ASCII` 代码表示，C 数据类型 `char` 用于存储字符数据。

字符串存储为以 `NULL` 结尾的字符数组，因此数组必须足够大以容纳字符序列加上一个字符。请记住，数组成员总是从零开始计数。

在这个例子中，我们可以看到 5 个单个字符被声明并初始化为值，以及一个设置为 "" 的空字符数组。

请注意单引号 `'` 用于字符周围，而双引号 `"` 用于字符字符串周围的差异。

```c
/******************************************** */
* C Programming in Linux (c) David Haskins 2008
* chapter2_2c                          * */
/******************************************** */

#include <stdio.h>

int main(int argc, char *argv[], char *env[])
{
    char c1 = 'd';
    char c2 = 'a';
    char c3 = 'v';
    char c4 = 'i';
    char c5 = 'd';
    char name[6] = "";

    sprintf(name, "%c%c%c%c%c%c", c1, c2, c3, c4, c5);
    printf("%s\n", name);
    return 0;
}
```

编译命令：`gcc -o data2 chapter2_2c -lc`。

调用时程序的输出：`./data2`

```text
david
```

### 2.3 字符串可以“意味着”什么

任何事物——赋予**变量**的**名称**及其**含义**或**用途**完全在于观察者的心中。试试这个：

```c
/****...*****
 * C Programming in Linux (c) David Haskins 2008
 * chapter2_3.c
 *  *
/*****...*****/
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[], char *env[])
{
	printf("Content-type:text/html\n\n");
	printf("<html>\n");
	printf("<body bgcolor=\"%s\"\n",argv[1]);
	printf("</body>\n");
	printf("</html>\n");
	return 0;
}
```

编译命令：`gcc -o data3 chapter2_3.c -lc`

作为超级用户，将程序复制到你的 `public_html/cgi-bin` 目录（或 `/srv/www/cgi-bin` (`OpenSuSe`) 或 `/usr/lib/cgi-bin` (`Ubuntu`)）。

在浏览器中输入：`http://localhost/cgi-bin/data3?red`

你应该会看到以下内容：

![图像描述](img/ad23766cfc9c69ba4f733f8b935cc3d8_28_0.png)

或者如果发送任何参数，你会得到令人惊讶的结果：

![图像描述](img/ad23766cfc9c69ba4f733f8b935cc3d8_28_1.png)

我们在这里做的是使用字符串参数 `argv[1]` 作为 HTML `body` 标签内的背景颜色代码。我们将 `Content-type` 规范更改为 `text/html`，奇迹般地，现在我们的程序正在生成 HTML 内容。一种语言在另一种语言表达内部。Web 浏览器理解一组有限的颜色术语，颜色也可以通过十六进制代码定义，例如 `#FFFFFF`（白色）、`#FF0000`（红色）、`#00FF00`（绿色）、`#0000FF`（蓝色）。

这个有趣的练习不仅仅是一个小把戏；一个程序可以在另一种语言中生成另一个程序的想法非常强大，这是整个互联网力量背后的原因。当我们从这个**通用网关接口程序**生成 HTML（或 `XML` 或任何其他内容）时，我们正在创建**动态内容**，可以链接到实时、变化的数据，而不是**静态**预编辑的网页。在实践中，大多数网站都有动态和静态内容的混合，但在这里我们只是在非常简单的层面上看到这是如何做到的。

在这本书中，我们将使用浏览器作为我们程序的推荐界面，因此我们将生成 HTML 和二进制图像流 Web 内容，纯粹作为一种手段来使程序的力量立即显现。在终端屏幕上盯着代码看并不是什么令人印象深刻的事情，编写窗口类型应用程序也不那么简单。
