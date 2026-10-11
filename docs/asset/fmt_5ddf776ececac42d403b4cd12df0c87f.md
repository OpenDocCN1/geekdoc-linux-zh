
忽略关于 `gets` 函数很危险的警告信息；我正试图利用该函数的缺陷来向你展示如何使用 gdb 追踪错误。

要查看此程序的问题，请在命令行提示符中运行并测试：

```
./dbgst
Command: test
Segmentation fault
```

程序在显示 `Segmentation fault`（段错误）消息后崩溃。对于像这样这样短小的程序，你可能可以通过检查源代码找到原因。然而，在现实世界的应用中，你可能无法立即知道是什么导致了错误。这时，你就必须使用 gdb 来找到问题的根源了。

要定位一个 bug，请按照以下步骤操作：

- 1. 在 gdb 中加载程序。要在 gdb 中加载名为 `dbgst` 的程序，请输入：

  `gdb dbgst`

- 2. 通过输入 `run` 命令在 gdb 下开始执行程序。当程序提示输入时，输入一些输入文本。

程序像之前一样运行失败了。以下是 `dbgst` 程序发生的情况：

```
(gdb) run
Starting program: /home/naba/swdev/dbgst
Command: test
```

```
Program received signal SIGSEGV, Segmentation fault.
0x0408888a in gets () from /lib/tls/libc.so.6
(gdb)
```

- 3. 使用 `where` 命令确定程序崩溃的位置。

对于 `dbgst` 程序，该命令输出了以下输出：

`(gdb) where`

# 654 探索 Linux 下的软件开发工具

```
#0 0x4008888a in gets () from /lib/tls/libc.so.6
#1 0x080048d3 in read_input (s=0x0) at dbgst.c:22
#2 0x080048b6 in main ( ) at dbgst.c:10
(gdb)
```

输出显示了函数调用的序列。函数调用 #0 —— 最最近的一次调用是一个 C 库函数 `gets`。`gets` 调用源于 `read_input` 函数（位于 `dbgst.c` 的第 22 行），而该函数又是由 `dbgst.c` 文件第 10 行的 `main` 函数调用的。

- 4. 使用 `list` 命令检查源码。

在 `dbgst` 中，你可以从 `dbgst.c` 文件的第 22 行开始，如下：

```
(gdb) list dbgst.c:22
17
18
19 void read_input(char *)
20
21 printf("Command: ");
22 gets(s);
23
24
(gdb)
```

查看此列表后，你可以判断问题可能在于 `read_input` 的调用方式。然后你列出 `dbgst.c` 中第 10 行附近的代码（`read_input` 调用产生的地方：c:10）：

```
(gdb) list dbgst.c:10
5
6 int main(void)
7
8 char *input = NULL; /* Just a pointer, no
storage for string */
9
10 read_input(input);
11
12 /* Process command. */
13 printf("You typed: %s\n", input);
14
(gdb)
```

到此时，你可以将问题缩小到名为 `input` 的变量。该变量是一个数组，而不是一个 `NULL`（即零）指针。

## 在 gdb 中修复 bug

有时你可以直接在 gdb 中修复 bug。对于上一节中的示例程序，你可以在可以在程序在显示错误消息并崩溃后立即尝试此修复。由于示例是人为构造的，我在 `dbgst` 程序中定义了一个名为 `buf` 的额外缓冲区，如下：

```c
static char buf[256];
```

我可以通过将变量 `input` 设置为 `buf` 来修复未初始化指针的问题。以下 gdb 会话纠正了未初始化指针的问题（此示例紧接在程序运行并因段错误崩溃之后开始）：

```
(gdb) file dbgst
A program is debugged already. Kill it? (y or n) y
Load new symbol table from "dbgst"? (y or n) y
Reading symbols from dbgst...
(gdb) list
1 #include <stdio.h>
2 static char buf[256];
3 void read_input(char *s);
4
5 int main(void)
6 {
7 char *input = NULL; /* Just a pointer, no
8 for string */
9
10 read_input(input);
11 (gdb) break 9
12 Breakpoint 1 at 0x0408888a: dbgst.c, line 9.
13 (gdb) run
14 Starting program: /home/naba/swdev/dbgst
15 Breakpoint 1, main () at dbgst.c:10
16 read_input(input):
17 (gdb) set input=buf
18 (gdb) cont
19 Continuing.
20 Command: test
21 You typed: test
22 (gdb) q
Program exited normally.
```

当 `dbgst` 程序显示错误消息并崩溃后，它返回了用户输入的内容。然而，在这个示例中，`main` 调用 `read_input` 时传入了一个未初始化的指针——这就是这个简单程序中的 bug。

使用 gcc 配合 `-g` 选项编译程序：

```bash
gcc -g o dbgst dbgst.c
```

忽略关于 `gets` 函数很危险的警告信息；我正试图利用该函数的缺陷来向你展示如何使用 gdb 追踪错误。

要查看此程序的问题，请在命令行提示符中运行并测试：

```
./dbgst
Command: test
Segmentation fault
```

程序在显示 `Segmentation fault`（段错误）消息后崩溃。对于像这样这样短小的程序，你可能可以通过检查源代码找到原因。然而，在现实世界的应用中，你可能无法立即知道是什么导致了错误。这时，你就必须使用 gdb 来找到问题的根源了。

要定位一个 bug，请按照以下步骤操作：

- 1. 在 gdb 中加载程序。要在 gdb 中加载名为 `dbgst` 的程序，请输入：

  `gdb dbgst`

- 2. 通过输入 `run` 命令在 gdb 下开始执行程序。当程序提示输入时，输入一些输入文本。

程序像之前一样运行失败了。以下是 `dbgst` 程序发生的情况：

```
(gdb) run
Starting program: /home/naba/swdev/dbgst
Command: test
```

```
Program received signal SIGSEGV, Segmentation fault.
0x0408888a in gets () from /lib/tls/libc.so.6
(gdb)
```

- 3. 使用 `where` 命令确定程序崩溃的位置。

对于 `dbgst` 程序，该命令输出了以下输出：

`(gdb) where`

# 654 探索 Linux 下的软件开发工具

```
#0 0x4008888a in gets () from /lib/tls/libc.so.6
#1 0x080048d3 in read_input (s=0x0) at dbgst.c:22
#2 0x080048b6 in main ( ) at dbgst.c:10
(gdb)
```

输出显示了函数调用的序列。函数调用 #0 —— 最最近的一次调用是一个 C 库函数 `gets`。`gets` 调用源于 `read_input` 函数（位于 `dbgst.c` 的第 22 行），而该函数又是由 `dbgst.c` 文件第 10 行的 `main` 函数调用的。

- 4. 使用 `list` 命令检查源码。

在 `dbgst` 中，你可以从 `dbgst.c` 文件的第 22 行开始，如下：

```
(gdb) list dbgst.c:22
17
18
19 void read_input(char *)
20
21 printf("Command: ");
22 gets(s);
23
24
(gdb)
```

查看此列表后，你可以判断问题可能在于 `read_input` 的调用方式。然后你列出 `dbgst.c` 中第 10 行附近的代码（`read_input` 调用产生的地方：c:10）：
