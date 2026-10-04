

## 728 探索 Fedora Core 中的软件开发工具

| 表 1-4（续表） | |
| :--- | :--- |
| 命令 | 功能 |
| watch VAR | 每当变量 VAR 的值发生变化时，显示该值。 |
| where | 显示调用序列。使用此命令定位程序崩溃的位置。 |
| x/F ADDR | 检查内存内容（位于 ADDR 的位置，格式由字母 F 指定，F 可以 o（八进制）；x（十六进制）；d（十进制）；u（无符号十进制）；b（二进制）；f（浮点数）；a（地址）；i（指令）；c（字符）；或 s（字符串）。你可以在格式字母后附加一个表示数据类型大小的字母。尺寸字母有 b（字节）；h（半字，2 字节），w（字，4 字节）以及 g（巨字，8 字节）。通常情况下，ADDR 是变量或指针的名称）。 | |

## 使用 gdb 查找 bug

为了理解如何使用 gdb 查找 bug，你需要看一个示例。通过简单的示例来展示这一过程是最容易的，因此我从一个包含典型 bug 的刻造程序开始。

以下是刻造的程序，我将其存储在文件 dbgtst.c 中：

```c
#include <stdio.h>
static char buf[256];
void read_input(char *s);

int main(void) {
    char *input = NULL; /* 只是一个指针，没有存储字符串的内存 */

    read_input(input);

    /* 处理命令。 */
    printf("You typed: %s\n", input);

    /* ... */
    return 0;
}

void read_input(char *s) {
    printf("Command: %s");
    gets(s);
}
```

## 探索 Fedora Core 中的软件开发工具 729

该程序的主函数调用 `read_input` 函数从用户处获取行输入。`read_input` 函数期望一个字符数组来存放用户输入的内容。然而，在这个示例中，`main` 使用一个未初始化的指针调用了 `read_input` —— 这就是该程序中的 bug。

使用 gcc 的 `-g` 选项编译程序：

```bash
gcc -g o dbgtst dbgtst.c
```

忽略关于 `gets` 函数危险的警告信息；我正试图利用该函数的缺陷来展示如何使用 gdb 跟踪错误。

要查看此程序的问题，请在命令行中运行并测试它：

```bash
./dbgtst
Command: test
Segmentation fault
```

程序在显示 Segmentation fault（段错误）消息后崩溃。对于像这样的小型程序，你可能通过检查源代码找到原因。但在实际应用中，你可能无法立即知道是什么导致了错误。这时，你就必须使用 gdb 来寻找问题的原因了。

要使用 gdb 定位 bug，请遵循以下步骤：

1.  在 gdb 中加载程序。要在 gdb 中加载名为 dbgtst 的程序，请输入：
    `dbgtst`

2.  通过输入 `run` 命令在 gdb 中开始执行程序。当程序提示输入时，输入一些文本内容。

程序像之前一样失败了。以下是 `dbgtst` 程序发生的情况：
```gdb
(gdb) run
Starting program: /home/naba/rhls4e/dbgtst
Command: test

Program received signal SIGSEGV. Segmentation fault.
0x0b6a4f6 in gets () from /lib/tls/libc.so.6
(gdb)
```

3.  使用 `where` 命令确定程序崩溃的位置。

对于 `dbgtst` 程序，该命令产生如下输出：

```gdb
(gdb) where
#0 0x00b8a4f6 gets () from /lib/tls/libc.so.6
#1 0x0080483dc in read (s=0) at dbgtst.c:22
#2 0x00804839 in main () at dbgtst.c:10
```

输出显示了函数调用序列。函数调用 #0 —— 最近的一次调用 —— 是 C 库函数 `gets`，`gets` 起源于 `read_input` 函数（位于 dbgtst.c 的第 22 行），该函数是由 dbgtst.c 文件第 10 行的 `main` 函数调用的。

4.  使用 `list` 命令检查可疑源代码行。

在 `dbgtst` 中，你可以从 dbgtst.c 文件的第 22 行开始，如下：

```gdb
(gdb) list dbgtst.c:22
17
18
19    void read_input(char *s)
20    {
21        printf("Command: %s");
22        gets(s);
23
24    }
```

在查看此列表后，你可以判断问题可能出在 `read_input` 被调用的地方。然后你列出 dbgtst.c 中第 10 行附近（`read_input` 调用源源处）的行：

```gdb
(gdb) list dbgtst.c:10
5
6    int main(void)
7    {
8        char *input = NULL; /* 只是一个指针，没有存储字符串的内存 */
9        string */
10    read_input(input);
11
12    /* 处理命令。 */
13    printf("You typed: %s\n", input);
14
15    /* ... */
16    return 0;
}
```

