
| 1 | 标准输出 (`stdout`) |

| 2 | 标准错误 (`stderr`) |

**图 12–5** 标准 I/O 通道的文件描述符值。

例如，`printf()` 库函数总是使用文件描述符 1 输出，而 `scanf()` 总是使用文件描述符 0 输入。当文件引用被关闭时，文件描述符会被释放，并可能被随后的 `open()` 重新分配。大多数 I/O 系统调用都需要文件描述符作为第一个参数，以便它们知道要在哪个文件上操作。

一个文件可以被打开多次，因此与它关联多个文件描述符（图 12–6）。

![](img/c5abad49cf9e1868c7e739095c9b9b05_468_0.png)

**图 12–6** 多个文件描述符，一个文件。

每个文件描述符都有自己的私属性，这些属性与文件无关，包括：

- 文件偏移量
- 状态标志
- 访问模式

例如，`printf()` 库函数总是使用文件描述符 1 输出，而 `scanf()` 总是使用文件描述符 0 读取输入。当文件引用被关闭时，文件描述符会被释放，并可能被随后的 `open()` 重新分配。大多数 I/O 系统调用都需要文件描述符作为第一个参数，以便它们知道要在哪个文件上操作。

### 12.3.2 第一个示例：reverse

为了说明这些系统调用的用法，我将使用一个名为 `reverse.c` 的小型工具程序（12-8）。它既是一个演示工具，也是编写工具的一个很好的示例。

```
工具：reverse -c [fileName]
reverse 反转输入的行并将其显示到标准输出。如果没有指定文件名，则反转标准输入。当使用 -c 选项时，reverse 还会反转每行的字符。
```

12-8 `reverse` 程序描述。

以下是 `reverse` 运行的示例：

```
$ gcc reverse.c -o reverse ...编译程序。
$ cat test ...列出测试文件。
Christmas is coming,
The days that grow shorter,
Remind me of seasons I knew in the past.
$ ./reverse_test ...反转文件。
Remind me of seasons I knew in the past.
The days that grow shorter,
Christmas is coming,
$ ./reverse-c test ...同时也反转行。
tpsap eht ni wen I snosaes fo em dimeR
retrohs worg taht syd ehT
gnomoc si samtrC
$ cat test | ./reverse ...将输出传递给 reverse。
Remind me of seasons I knew in the past.
The days that grow shorter,
Christmas is coming,
$ 
```

### 12.3.3 reverse 如何工作

`reverse` 工具对其输入进行两次扫描。在第一次扫描中，它记录文件中每行的起始偏移量，并将这些信息存储在数组中。在第二次扫描中，它按反序跳转到每行的开头，从原始输入文件中将其复制到标准输出。

如果没有指定名称，`reverse` 在第一次扫描中从标准输入读取，并将其复制到临时文件中供第二次扫描使用。程序结束后，临时文件将被删除。

12-9 给出了程序流程的概述，并列出了每个操作相关的函数列表，以及每个步骤使用的系统调用列表。

# 第 12 章 • 系统编程

| 步骤 | 动作 | 函数 | 系统调用 |
|---|---|---|---|
| 1 | 解析命令行。 | `CommandLine`, `processOptions` | `open` |
| 2 | 如果从标准输入读取，则创建一个临时文件来存储输入；否则打开输入文件进行读取。 | `pass1` | `open` |
| 3 | 分块读取文件，并将每行的起始偏移量存储在数组中。从标准输入读取时，将每个分块拷贝到临时文件。 | `pass1`, `trackLines` | `read`, `write` |
| 4 | 再次从输入文件读取（向后读取），将每行复制到标准输出。如果选择了 -c 选项，则反转行内容。 | `pass2`, `processLine`, `reverseLine` | `lseek` |
| 5 | 关闭文件，如果是临时文件则删除。 | `pass2` | `close` |

**12–9** `reverse.c` 中使用的算法描述。

接下来的几页提供了 **`reverse`** 的 `reverse.c;` 源代码完整列表。我建议你快速浏览一遍，然后阅读随后的系统调用描述。该代码也可以在网上获取；更多信息请参见前言。

## 12.3.4 reverse.c: 列表

```c
#include <fcntl.h> /* 用于文件模式定义 */
#include <stdio.h>
#include <stdlib.h>

/* * 枚举 */
enum { FALSE, TRUE }; /* 标准假和真值 */
enum { STDIN, STDOUT, STDERR }; /* 标准 I/O 通道索引 */

/* #define 语句 */
#define BUFFER_SIZE 4096 /* 拷贝缓冲区大小 */
#define NAME_SIZE 12
#define MAX_LINES 100000 /* 文件最大行数 */

/* 全局变量 */
char *fileName = 0; /* 指向文件名 */
char tmpName[NAME_SIZE];
int charOption = FALSE; /* 如果使用了 -c 选项则置为 true */
```

# 普通文件管理

```c
21 int standardInput = FALSE; /* 如果从 stdin 读取则置为 true */
22 int lineCount = 0; /* 输入总行数 */
23 int lineStart [MAX_LINES]; /* 存储每行的偏移量 */
24 int fileOffset = 0; /* 输入中的当前位置 */
25 int fd; /* 输入的文件描述符 */
26
27 /***********************************************************************************
28
29 main(argc, argv)
30
31 int argc;
32 char* argv[];
33
34 {
35 parseCommandLine(argc,argv); /* 解析命令行 */
36 pass1(); /* 对输入进行第一遍扫描 */
37 pass2(); /* 对输入进行第二遍扫描 */
38 return (/* EXIT_SUCCESS */ 0); /* 完成 */
39 }
40
41 /*********************************************************************************/
42
43 parseCommandLine(argc, argv)
44
45 int argc;
46 char* argv[];
47
48 /* 解析命令行参数 */
49
50 {
51 int i;
52
53 for (i=1; i < argc; i++)
54 {
55 if(argv[i][0] == '-')
56 processOptions(argv[i]);
57 else if (fileName == 0)
58 fileName= argv[i];
59 else
60 usageError(i); /* 发生错误 */
61 }
62
63 standardInput = (fileName == 0);
64 }
65
66 /*********************************************************************************/
67
68 processOptions(str)
```
