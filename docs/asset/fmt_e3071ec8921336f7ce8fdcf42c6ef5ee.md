
| `quit` | 退出 `gdb` |
| `run` | 开始运行当前加载的可执行文件 |
| `set variable VAR=VALUE` | 将变量 `VAR` 的值设置为 `VALUE` |
| `shell CMD` | 执行 UNIX 命令 `CMD`，而无需离开 `gdb` |
| `step` | 在当前函数中前进一行，进入其他函数（如果有） |
| `watch VAR` | 每当变量 `VAR` 的值发生变化时，显示该变量的值 |
| `where` | 显示调用序列。使用此命令来定位你的程序在哪里崩溃。 |
| `x / F ADDR` | 以 `F` 字母指定的格式检查地址 `ADDR` 处内存位置的内容，其中 `F` 可以是 `o`（八进制）、`x`（十六进制）、`d`（十进制）、`u`（无符号十进制）、`t`（二进制）、`f`（浮点数）、`a`（地址）、`i`（指令）、`c`（字符）或 `s`（字符串）。你可以在格式字母后附加一个表示数据类型大小的字母。大小字母为 `b`（字节）、`h`（半字，2 字节）、`w`（字，4 字节）和 `g`（巨型字，8 字节）。通常，`ADDR` 是变量或指针的名称。 |

### 使用 gdb 查找错误

为了理解如何使用 `gdb` 查找错误，你需要查看一个示例。使用简单的例子来说明这个过程最容易，因此我从一个相当人为构造的包含典型错误的程序开始。

以下是该人为构造的程序，我将其保存在文件 `dbg tst.c` 中：

```c
#include <stdio.h>
static char buf[256];
void read_input (char *s);
int main(void)
{
  char *input = NULL; /* Just a pointer, no storage for string */
  read_input (input);
  /* Process command. */
  printf( "You typed: %s\n", input);
  /* ... */
  return 0;
}
void read_input (char *s)
{
  printf ("Command: ");
  gets (s);
}
```

此程序的 `main` 函数调用 `read_input` 函数以从用户获取一行输入。`read_input` 函数期望一个字符数组，在其中返回用户输入的内容。然而，在此示例中，`main` 调用 `read_input` 时使用的是一个未初始化的指针——这就是这个简单程序中的错误。

使用 `gcc` 并带有 `-g` 选项来构建程序：

```
gcc -g -o dbg tst dbg tst.c
```

忽略关于 `gets` 函数危险的警告信息；我试图利用该函数的缺点来展示如何使用 `gdb` 追踪错误。

要查看此程序的问题，请运行它并在 `Command` 提示符处输入 `test`：

```
./dbg tst
Command: test
Segmentation fault
```

程序在显示 `Segmentation fault` 消息后终止。对于这个非常小的程序，你通过检查源代码可能就能找到原因。然而，在实际应用中，你可能不会立即知道导致错误的原因。这时你必须使用 `gdb` 来找出问题的根源。

要使用 `gdb` 定位错误，请遵循以下步骤：

1. **在 `gdb` 中加载程序。要在 `gdb` 中加载名为 `dbgtst` 的程序，请输入以下内容：**

```
gdb dbgtst
```

2. **通过输入 `run` 命令在 `gdb` 下开始执行程序。当程序提示输入时，输入一些文本。**

程序如前一样失败。以下是 `dbgtst` 程序发生的情况：

```
(gdb) run
Starting program: /home/naba/sdewd/dbgtst
Command: test

Program received signal SIGSEGV, Segmentation fault.
0x400802b6 in gets () from /lib/tls/libc.so.6
(gdb)
```

3. **使用 `where` 命令确定程序在哪里死亡。**

对于 `dbgtst` 程序，该命令产生以下输出：

```
(gdb) where
#0  0x400802b6 in gets () from /lib/tls/libc.so.6
#1  0x08048474 in read_input (s=0x0) at dbgtst.c:16
#2  0x08048436 in main () at dbgtst.c:7
(gdb)
```

输出显示了函数调用序列。函数调用 `#0` —— 最近的一次 —— 是调用 C 库函数 `gets`。`gets` 调用源自 `read_input` 函数（在文件 `dbgtst.c` 的第 16 行），而后者又被 `dbgtst.c` 文件第 7 行的 `main` 函数调用。

4. **使用 `list` 命令检查可疑源代码的行。**

在 `dbgtst` 中，你可以从 `dbgtst.c` 文件的第 16 行开始，如下所示：

```
(gdb) list dbgtst.c:16
     11      return 0;
     12    }
     13    void read_input(char *s)
     14    {
     15      printf("Command: ");
     16      gets(s);
     17    }
     18
(gdb)
```

查看此列表后，你可以看出问题可能是 `read_input` 的调用方式。然后你列出 `dbgst.c` 中第 7 行周围的代码（`read_input` 调用的来源）：

```
(gdb) list dbgst.c:7
2         static char buf[256];
3         void read_input(char *s);
4         int main(void)
5        {
6            char *input = NULL; /* Just a pointer, no
          storage for string */
7            read_input(input);
8            /* Process command. */
9            printf("You typed: %s\n", input);
10           /* .... */
11           return 0;
(gdb)
```

此时，你可以将问题缩小到名为 `input` 的变量。该变量是一个数组，而不是一个 NULL（即零）指针。

### 在 gdb 中修复错误

有时你可以直接在 `gdb` 中修复错误。对于前一部分中的示例程序，你可以尝试在程序显示错误消息后死亡后立即应用此修复。由于该示例是人为构造的，我在 `dbgst` 程序中定义了一个额外的名为 `buf` 的缓冲区，如下所示：

`static char buf[256];`

我可以通过将变量 `input` 设置为 `buf` 来修复未初始化指针的问题。以下与 `gdb` 的会话纠正了未初始化指针的问题。（此示例紧随程序运行并因段错误而死亡之后。）

```
(gdb) file dbgst
A program is being debugged already.  Kill it? (y or n) y
Load new symbol table from "/home/naba/sw/dbgst"? (y or n) y
Reading symbols from /home/naba/sw/dbgst...done.
(gdb) list
1          #include <stdio.h>
2          static char buf[256];
3          void read_input(char *s);
4          int main(void)
5         {
6            char *input = NULL; /* Just a pointer, no
          storage for string */
7            read_input(input);
8            /* Process command. */
```

9           printf("You typed: %s\n", input);

10         /***/

(gdb) break 7

断点 2 位于 0x804842b: 文件 dbgtest.c, 第 7 行。

(gdb) run

正在启动程序：/home/naba/sw/dbgtest
