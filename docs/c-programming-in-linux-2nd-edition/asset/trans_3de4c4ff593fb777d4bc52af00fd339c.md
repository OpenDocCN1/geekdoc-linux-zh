
## 3.4 数据结构

有时我们希望将一组变量作为一个组进行管理，例如从一个数据库记录中提取所有值，并将整个记录传递到程序的各个部分进行处理。为了实现这一点，我们可以将数据分组为结构体。

这个程序使用结构体（struct）来定义一个名为“玩家”的实体的一组属性。主函数包含一个由 5 个玩家组成的数组的声明和实例化。我们依次将每个数组成员的指针传递给一个函数，以对每个玩家进行排名。该函数使用 switch 语句来检查每个玩家名字的第一个字母，从而进行任意排名。然后，我们依次将每个数组成员的指针传递给一个用于打印详情的函数。

```c
/** *****************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter3_3.c
 * ******************************************************/
#include <stdio.h>
#include <string.h>
struct player
{
    char name[255];
    char role[255];
    int ranking;
};
void rank(struct player *p)
{
    switch(p->name[0])
    {
        case 'P': p->ranking = 4;break;
        case 'H': p->ranking = 1;break;
        case 'R': p->ranking = 2;break;
        case 'J': p->ranking = 5;break;
        case 'B': p->ranking = 3;break;
    }
}
void show(struct player *p)
{
    printf("Name:%s Role:%s Ranking:%d<br>\n",
        p->name,p->role,p->ranking);
}
int main(int argc, char *argv[], char *env[])
{
    struct player myteam[5] = { {"Pele", "Striker",0 },
                        {"Beckham", "male model" ,0 },
                        {"Roddick","tennis man",0 },
                        {"Haskins","swimmer",0 },
                        {"Jagger", "singer",0 } };
    int i=0;
    printf("Content-type:text/html\n\n");
    for(i=0;i<5;i++) rank ( &myteam[i] );
    for(i=0;i<5;i++) show ( &myteam[i] );
    return 0;
}
```

结果如下所示，通常是在浏览器中查看：

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_40_0.png)

这是一种非常强大且相当高级的技术，但你需要了解它。**结构体**的概念直接导出了**类**和**对象**的概念。

我们可以看到，使用结构体极大地简化了将数据元素在程序中传递以执行不同工作的业务任务。如果我们更改结构体的定义，它仍然可以正常工作，我们只需添加代码来处理新属性，而不必更改执行工作的函数的参数列表或签名。

结构体的定义实际上并不创建任何数据，只是设定了我们可实例化的正式形状。在主函数中，我们可以以所示形式表达这种实例化，创建一个由符合我们定义的序列组成的数据元素列表。

你大概可以看出，带有附加函数或方法的结构体本质上就是 Java 中的类，在 C++ 中也是如此。**面向对象语言**从这里开始，实际上，许多早期被称为“面向对象”的系统实际上只是使用 C 语言结构体构建的。

例如，如果你查看 Apache 服务器开发头文件，你会发现很多结构体，比如在 httpd.h 的这个片段中：

```c
struct server_addr_rec {
    /** The next server in the list */
    server_addr_rec *next;
    /** The bound address, for this server */
    apr_sockaddr_t *host_addr;
    /** The bound port, for this server */
    apr_port_t host_port;
    /** The name given in "<VirtualHost>" */
    char *virthost;
};
```

不要担心这一切意味着什么——只需注意到这是一种非常常见且非常强大的技术，并且数据结构的設計，就像与其密切相关的数据库表的设计一样，是你作为程序员需要理解的核心、关键且至关重要的任务。

你做出哲学决定，认为**世界就是这样**并且可以以这种方式建模。这是一个沉重的责任——在哲学中，这项工作被称为**本体论**（存在什么？）和**认识论**（我们如何知道它？）。我打赌你从未想过这是你在做的事情！

### 3.5 函数、指针和结构体 – 结论

我们使用一些简单的数据类型来表示一些信息，并将输入传输到程序中，以及组织和显示一些视觉输出。

我们使用嵌入在输出字符串中的 HTML 使输出在网页浏览器中可见。

我们学习了创建函数库以供重复使用。

我们学习了数据结构和使用指针在程序中传递它们的方法。

**练习：**

使用 C 库函数创建一个程序，该程序：

- 以写入模式打开一个文件，
- 将命令行参数写入文件
- 关闭文件
- 以读取模式打开文件
- 读取内容
- 关闭文件
- 将其打印到屏幕上

这将给你寻找信息、查找合适的库函数以及在线或从书中查找示例的经验。

## 4 逻辑、循环和流程控制

### 4.1 C 流程控制的语法

我们可以使用以下 C 构造来控制程序执行。
当我们可以计数通过一个序列或系列时：

```c
for( 初始值; 继续直到 ; 增量变化 )
{ 做这个; 做那个; 做另一个; }
```

当我们在等待某个条件改变时：

```c
while( 这是真的 )
{ 做这个; 做那个; 做另一个; }
```

或者如果我们想至少做一次某事然后测试：

```c
do { 做这个; 做那个; 做另一个; }
while( 这是真的 )
```

当我们有一个单一选项要测试时：

```c
if( 这是真的 )
{ 做这个; 做那个; 做另一个; }
else
{ 做这个; 做那个; 做另一个; }
```

当我们要测试更多选项时：

```c
if( 这是真的 )
{ 做这个; 做那个; 做另一个; }
else if ( 这是真的 )
{ 做这个; 做那个; 做另一个; }
else
{ 做这个; 做那个; 做另一个; }
```

当我们要基于整数或单个字符值测试更多选项时：

```c
switch( 基于一个整数或字符值 )
{
case 0: 做这个; 做那个; 做另一个; break;
case n: 做这个; 做那个; 做另一个; break;
default: 做这个; 做那个; 做另一个; break;
}
```

### 4.2 控制发生什么以及顺序

这部分完全是关于**如果**、**那么**、**否则**、**真**和**假**的——这是我们表达和控制程序执行的基本构件。这可能是非常枯燥和琐碎的材料，因此为了使其更易于理解，我们将解决一个你将在进行任何复杂交互式网页工作时需要解决的问题。

我们将构建一个我们可以使用的东西，以提供类似于 Java .servlet 中典型的 `getParameter("ITEM1")` 方法或 PHP 中 `$_REQUEST["ITEM1"]` 函数所能获得的功能。

在第 1 章中，我们看到可以通过传递给 main 函数的隐式参数访问环境变量。我们还可以使用库函数 `getenv()` 来请求任何命名环境变量的值。

```c
/************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter4_1.c                                    *
***********************************************/
#include <stdio.h>
#include <string.h>
int main(int argc, char *argv[], char *env[])
{
  printf("Content-type:text/html\n\n<html><body bgcolor=#29abe2>\n");
  char value[256] = "";
  strncpy(value,(char *) getenv("QUERY_STRING"),255);
  printf("QUERY_STRING : %s<BR>\n", value );
  printf("<form>\n");
  printf("<input type=\"TEXT\" name=\"ITEM1\">\n");
  printf("<input type=\"TEXT\" name=\"ITEM2\">\n");
  printf("<input type=\"SUBMIT\">");
  printf("</form></body></html>\n");
  return 0;
}
```

在这里，我们显示 **QUERY_STRING**，这是程序从包含所有命名表单元素的 NAME=VALUE 对的 HTML 表单接收到的完整内容。

默认情况下，HTML 表单使用 **GET** 方法，除非在 action 属性中另有指定，否则会将所有表单数据传回包含该表单的程序或页面。这些数据包含在 QUERY_STRING 中，作为由 & 字符分隔的变量 = 值对序列。

> 注意，在 HTML 中，值是用引号括起来的，因此要在 C 字符串中嵌入这些值，我们必须用特殊符号 \ 对字符进行“转义”，例如 “\"ITEM1\"” 。此外，我们在每个 HTML 输出部分的末尾使用“\n”或显式换行符，以便当我们在浏览器中选择“查看源代码”时，我们得到一些格式合理的文本，而不是整个页面显示为一条长单行。

在浏览器中调用此程序，我们会看到一个表单，并可以在框中输入一些数据：

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_44_0.png)

提交表单后，我们看到：

![](img/ad23766cfc9c69ba4f733f8b935cc3d8_44_1.png)

为了对 QUERY_STRING 做出很多意义并找到其中的特定值，我们将不得不*解析*它，将其分解为其组成部分，为此我们需要一些**条件逻辑**（if, else 等）和一些**循环**来计数变量中的字符。理想情况下，应创建一个基本函数来执行此任务，因为这是你

