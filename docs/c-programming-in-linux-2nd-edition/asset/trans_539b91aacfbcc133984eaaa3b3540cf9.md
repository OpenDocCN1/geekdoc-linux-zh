

# 程序结构分析：

```c
printf("Hello, you are learning C!!\n");
```

调用库函数 printf 时传入了一个参数，即一个以 `\n`（换行符）结尾的字符串。

```c
printf("Number of arguments to the main function:%d\n", argc);
```

调用库函数 printf 时传入了两个参数：一个以 `\n` 结尾的字符串，其中包含 `%d` 作为第二个参数 `argc`（一个 int 类型）的占位符。

```c
for(i=0; i<argc; i++)
```

这是一个“for 循环”，我们通过计数器整数 `i` 反复执行某些操作。`i` 在每次迭代（循环）中递增（通过表达式 `i++`），只要 `i` 保持小于 `argc` 的值，循环就继续执行。

```c
printf("argument number %d is %d\n", i, argv[i]);
```

调用库函数 printf 时传入了三个参数：一个以 `\n` 结尾的字符串，其中包含 `%d` 作为第二个参数 `i`（一个 int 类型）的占位符，以及 `%s` 作为第三个参数 `argv[i]` 的占位符。`argv[i]` 是名为 `argv[]` 的字符字符串指针数组的第 i 个成员。

### 1.3 第三个 Hello 程序

让我们进入实战，在网页中运行这个程序。额外添加第一个输出 printf 语句 `"Content-type:text/plain\n\n"`，它告诉服务器将要传输哪种 MIME 类型。

使用 `gcc -o hello3 chapter1_3.c` 进行编译，并将编译后的文件 `hello3` 复制到你的 `public_html/cgi-bin` 目录中（或者在本地机器上以超级用户身份将程序复制到 `/srv/www/cgi-bin`（OpenSuse）或 `/usr/lib/cgi-bin`（Ubuntu））。

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

“main” 函数签名的一个鲜为人知的特性是它可以接受 **三个** 参数，我们现在将看到的是最后一个参数：`char *env[]`。它也是一个字符串指针列表，但在这种情况下，这些是程序运行时可用的 **系统环境变量**。

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

使用 **`gcc -o hello4 chapter1_4.c`** 进行编译，并以超级用户身份将程序复制到 `/srv/www/cgi-bin`（OpenSuse）或 `/usr/lib/cgi-bin`（Ubuntu）。你可以从终端中通过 `./hello4` 运行此程序，你会看到一长串环境变量。在浏览器中输入 `http://localhost/cgi-bin/hello4` 时，你会看到一组完全不同的变量。

> **维基百科对“环境变量”的定义如下**：
> 
> “在所有 Unix 和类 Unix 系统中，每个进程都有自己的一套私有环境变量。默认情况下，当创建一个进程时，它会继承其父进程的副本环境，除了父进程在创建子进程时所做的明确更改........ 所有 Unix 操作系统变种以及 DOS 和 Microsoft Windows 都有环境变量；然而，它们并不都使用相同的变量名。运行的程序可以访问环境变量的值以用于配置目的。环境变量的示例包括..... PATH, HOME... “

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_20_0.png)

我们将很快发现，**QUERY_STRING** 是我们与程序通信的重要环境变量，在这种情况下，我们看到它的值是 “david+haskins”，即我们在 URL 中输入的 “?” 之后的所有内容。向诸如 hello4 这样的 **通用网关接口**（CGI）程序发送信息的有效方式，但我们应该将其限制为一个字符串。在我们的例子中，我们使用了 “+” 连接两个字符串。如果我们输入：“david haskins”，浏览器会对其进行转义，我们会看到：

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
- 使用 “for” 和 “while” 的循环

我们特意采取了巨大的飞跃，从编写仅在 “终端屏幕” 中运行的程序，过渡到可以在互联网浏览器中可见的程序。

这样做的原因是，编写与用户交互的程序（在 Windows、Gnome 或 KDE 等窗口系统中）过程极其复杂，而且你不太会经常被要求这样做。

互联网浏览器如今已成为我们几乎所有操作的事实接口模式，因此我们不妨从一开始就理解如何使用它。

在后续的所有章节中，我们将遵循这一模式：从某些基本技术开始，然后将其应用于基于 Web 的系统。

实际上，并没有太多真正的现实世界 C 语言通用网关接口编程在进行中，但确实有大量基于 C 和 C++ 的代码作为 Apache 模块和 Microsoft IIS ISAPI Dlls 运行。也许很多人不知道，Ebay 的大部分代码是用 C / C++ 编写的。

为什么？因为它具有极致的速度，而他们在全球实时市场中与抢购者的业务需要这种闪电般快速的核心，因此没有其他方法能获得这种性能。

# 2 数据和内存

### 2.1 简单数据类型

当我们编写程序时，在声明和描述变量以表征我们想要包含在信息处理中的事物类型时，必须对世界的本质做出决定或断言。

这个过程具有深刻的哲学意义；我们做出 **本体论** 断言，认为此物或彼物存在；当我们选择特定的数据类型或数据类型集合来描述这些事物的属性时，我们做出 **认识论** 断言。这是沉重的话题，伴随着巨大的责任，不可轻率行事。

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

