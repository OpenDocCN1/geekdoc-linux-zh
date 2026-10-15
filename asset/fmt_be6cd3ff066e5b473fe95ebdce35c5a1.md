
通过宏，你只需要对 `Makefile` 进行细微更改，就可以使用多个 C 编译器编译程序。例如，通过使用 `CC` 宏并将第 846 页中所有的 `gcc` 替换为 `$(CC)`，你需要为 `CC` 赋值一个值以使用你选择的编译器：

```bash
$ cat Makefile
```

```makefile
# compute 的 Makefile
#
CC=gcc
compute: compute.o calc
$(CC) -o compute.o calc

compute.o: compute.c h
$(CC) -c -O3 compute.c

calc: calc.c
$(CC) -c calc.c

clean:
rm *.o
```

此示例显示了编译器/加载器标志与编译器/加载器是相同的。在更复杂的情况下，你可能需要为 Linux 可用的不同编译器创建宏。你可以通过替换 `CC` 变量来指定 Portland Group 的编译器 `gpc`。

你可以通过在命令行指定宏来覆盖 `Makefile` 中的宏。以下命令为所有对象文件添加调试符号：

```bash
$ make CFLAGS=g ...
```

![](img/0f75ae90508d45878c00a5b098fe29d4_1173_0.png)

![](img/0f75ae90508d45878c00a5b098fe29d4_1173_1.png)

# 调试 C 语言

C 编译器对程序中允许的结构类型非常慷慨。遵循 UNIX “没有消息就是好消息”以及“用户知道什么是最好的”的哲学，`gcc` 像许多其他 Linux 工具一样，接受几乎任何逻辑上可能的结构，并根据语言的定义进行调试。尽管这种方法为程序员提供了极大的灵活性控制力，但可能会使调试变得困难。

图 27-4 显示了 `badtabs.c`，它是之前讨论过的 `tabs.c` 程序的缺陷版本。它包含一些错误且无法正常运行。本节使用该程序来阐明调试技术。

图 27-4. `badtabs.c` 程序（行号不是源代码的一部分；箭头指向程序中的错误。）

# 注释

| 预处理器指令 | 函数原型 | 主函数 |
|---|---|---|
| `/* 将标准输入中的制表符转换为空格 */` / `/* 在保持列的同时输出标准输出 */` / `#include <stdio.h>` / `#define TABSIZE 8` | `/* findstint 的原型 */` / `int findstint(int);` | `/* 从 stdin 读取的字符 */` / `int c; int posn = 0;` |

```c
#include <stdio.h>

int main() {

    /* 从 stdin 读取的字符 */
    int c;
    int posn = 0;

    /* 制表符停止位的列位置 */
    while ((c = getchar()) != EOF) {
        switch(c) {
            case '\t':
                c = findstint(posn);
                for (int i = 0; i < c; i++)
                    putchar(' ');
                break;
            case '\n':
                putchar(c);
                posn = 0;
                break;
            default:
                putchar(c);
                posn++;
                break;
        }
    }

    return 0;
}
```

```c
/* c 是一个制表符 */
```

```c
/* c 是一个换行符 */
```

```c
/* c 是其他任何内容 */
```

```c
/* 计算下一个制表符停止位的增量大小 */
int findstint(int *col) {
    int colindex, retval;
    retval = (TABSIZE - (*col % TABSIZE));
    /* 增加参数（当前列位置）到下一个制表符停止位 */
    *col = retval;
    return retval;
}
/* main 获取填充所需的空格数量 */
```

在接下来的示例中，编译 `badtabs.c` 然后使用来自 `testtabs` 的输入运行它。检查输出发现，`TAB` 字符没有被替换相应数量的 `SPACES`：

```bash
$ gcc -o badtabs badtabs.c
$ cat tabs
abcTABxyz
$ badtabs < testtabs
abc xyz
```

调试 C 程序的一种方法是在源代码的关键点插入打印语句。要了解更多关于 `badtabs.c` 运行时的行为，你可以将 `switch` 语句的内容替换如下：

```c
case '\t': /* c 是一个制表符 */
printf(stderr, "before to call findstop, posn is %d", posn);
inc = findstop(&posn);
printf(stderr, "after to call findstop, posn is %d", posn);
for (int i = 0; i < inc; i++) {
    switch (c = getchar()) {
    case '\t':
    case '\n':
        /* c 是一个换行符 */
        printf(stderr, "got a newline\n");
        putchar(c);
        posn = 0;
        break;
    default:
        /* c 是其他任何内容 */
        printf(stderr, "got another character\n");
        putchar(c);
        posn++;
        break;
    }
}
```

此代码中的 `printf` 语句将消息发送到标准错误。因此，如果你重定向此程序的标准输出，它将与发送到标准错误的输出交替出现。下一个示例演示了该程序在输入文件 `testtabs` 上的操作。

```bash
$ gcc -o badtabs badtabs.c
$ badtabs < testtabs > testspaces

got another character
got another character
got another character
before call findstop, posn is 3
after call findstop, posn is 3
got another character
got another character
got another character
got a newline
$ cat testspaces
abcTabYz
```

`printf` 语句提供了关于执行过程的额外信息。`posn` 变量在 `findstop` 中没有增加，这可能会引导你发现程序中的错误。如果没有，你可能尝试通过在 `findstop` 中插入打印语句来“围堵”错误代码。

对于你已经大致知道要写什么的简单程序，添加打印语句来跟踪执行可以帮助你快速发现问题。

# `gcc` 编译器选项

`gcc` 编译器包含许多帮助你调试的功能，例如警告。大多数属于不会停止程序编译的性质。然而，如果你使用 `-Wall` 选项编译，`gcc` 会识别出几个问题。警告信息不会停止编译，但它们可能指示潜在错误。例如，`badtabs.c` 程序在语法上是正确的；但是，如果你使用 `-Wall` 选项编译，`gcc` 会显示表 27-2 中列出的警告。产生这些警告的结构通常很容易修复和避免。

## 表 27-2

| 选项 | 报告的 |
|---|---|
| `-Wimplicit` | 函数或参数未显式声明 |
| `-Wreturn-type` | 没有返回值的函数 |
| `-Wunused` | 变量已声明但未使用 |
| `-Wcomment` | 通常用于开始注释的字符 `"/"` 出现在注释内部 |
| `-Wformat` | 某些输入输出语句包含格式符合符 |

```bash
$ gcc -Wall badtabs.c
badtabs.c:11: warning: return type defaults to 'int'
badtabs.c: In function 'main':
badtabs.c:34: warning: control reaches end of nonvoid function
badtabs.c:46:25: warning: "/" within comment
badtabs.c: In function 'findstop':
badtabs.c:40: warning: unused variable 'colindex'
badtabs.c:47: warning: control reaches end of nonvoid function
```

接下来的几段文字将讨论剩余的警告。大多数不会在 `badtabs` 的执行中引起问题。你通常可以通过重写产生此类警告的代码部分来生成程序。

`badcls` 的第 40 行包含了函数 `findstop` 中局部变量 `colindex` 的定义。一条警告信息引用了该处，因为 `colindex` 变量从未被使用。删除其声明即可消除该警告。

最后一个警告引用了第 47 行，源于前面提到的注释不当的问题。编译器之所以发出警告信息，是因为它在 `findstop` 中看到了一个 `return` 语句（编译器忽略了注释文本）。由于函数 `findstop` 返回 `int` 类型，它期望在到达函数末尾之前找到 `return`。当注释被正确终止时，该警告就会消失。

`gcc` 编译器提供了许多 `W` 选项。`Wall` 类未涵盖的选项通常涉及可移植性；修改导致这些警告的代码可能并不合适。警告通常出现在使用不同的 C 语言方编写程序时，或者某些结构可能无法在其他（特别是较旧的）C 编译器上运行时时。`pedantic-errors` 选项会将警告转换为错误，如果程序包含会生成警告的项目，会导致构建失败。要了解更多关于这些及其他警告选项，请参阅 `gcc` info 页面。

## 符号调试器

有许多调试器可以解决那些打印语句和编译器警告选项等符号调试方法无法处理的问题。这些调试器包括 `gdb`、`xxgdb`、`kdbg`、`ddd`、`dups`，它们在网络上均可用（参见附录 B）。高级符号调试器允许你通过 C 语言语句分析程序的执行情况。它们还提供了一个低级视图，用于分析机器指令级别的程序执行。除了 `fogdb` 之外，这些调试器每一个都提供了 GUI。

调试器允许你监控和控制程序的执行。你可以在检查执行环境状态的同时，逐行步进程序。

## 核心转储 (Core dumps)

调试器还允许你检查核心文件（命名为 `-core`）。当程序执行期间发生严重错误时，操作系统可以创建一个核心文件，其中包含错误发生时程序状态和系统的信息。该文件汇总了程序所使用的计算机内存转储（以前称为 core memory，现在的术语是 dump）。为了节省磁盘空间，你的系统可能不会自动保存核心文件。你可以使用 `ulimit` 来允许保存核心文件。如果你正在运行 `bash`，以下命令允许将无限大小的核心文件保存到磁盘：

- `ulimit -c unlimited`

每当操作系统转储核心时，都会提示你。你可以使用符号调试器从核心文件中读取信息，以识别程序中发生错误的行，检查该点的变量值等。由于核心文件通常很大，请在不再需要它们时务必删除这些文件。

## `gdb`: 符号调试器

本节解释了如何使用 GNU 调试器。其他符号调试器提供了不同的接口，但操作方式相似。为了充分利用符号调试器来调试程序，你必须使用 `-g` 选项编译程序，该选项由 `gcc` 提供。

### 提示：始终使用 `-g`

即使在发布软件时，使用 `-g` 选项也是好主意。包含调试符号会让二进制文件变大一点。调试符号不会让程序运行变慢，但它们确实能更容易找到用户发现的问题。

### 提示：在调试器中避免优化标志

在为调试编译程序时，请将优化标志限制为 `-O0` 或 `-O2`。由于调试和优化的目标本质上不同，避免结合这两种操作可能是最好的。

### 提示：优化应该是有效的

完全关闭优化有时可以消除错误。然而，这种方式消除错误不应被视为永久解决方案。当启用优化时，编译器可能会自动初始化变量并为你执行某些检查，从而产生更稳定的代码。正确的代码在至少使用 `-O0` 选项编译时应该可以正常工作，在 `-O2` 选项下几乎肯定可以。`-O3` 选项通常包含实验性优化：它在所有情况下可能都不会生成正确的代码。

以下示例在从 C 程序 `tabs.c` 创建可执行文件 `tabs` 时使用了 `-g` 选项：

```bash
$ gcc -g tabs.c -o tabs
```

`tabs` 的输入包含在文件 `testtabs` 中，该文件只有一行：

```bash
$ cat testtabs
```

调用调试器时无法为 `tabs` 指定文件。相反，你必须在用 `run` 命令开始执行时调用调试器并指定输入文件。

`list` 命令显示源代码的前十行。`subseqlist` 命令显示接下来的十行源代码。

## `$ gdb tabs`

```text
GNU gdb Red Hat Linux (6.3.0-1.114h)
Copyright 2004 Free Software Foundation, Inc.
(gdb)
2 / * 保持列的同时的标准输出 *
3
4 #include <stdio.h>
5 #define TABSIZE 8
6
7 / * 函数 findstop 的原型 /
8 int findstop(int);
9
10 int main()
11 {
12 (gdb)
13 int c; /* 从 stdin 读取的字符 *
14 int posn = 0; /* 字符的列位置 *
15 int inc; /* 制表停止列索引 */
16
17 while (c = getchar(i) != EOF)
18 switch(c)
19 {
20 case '\t': /* c 是制表符 *
21 inc = findstop(posn);
22 for ( ; inc > 0; inc--)
23 (gdb)
```

调试器最重要的功能之一是在受控环境中运行程序。你可以随时停止程序运行。检查任何参数或变量的状态是非常用的。例如，你可以给 `break` 命令提供源代码行号、内存地址或函数名作为参数。该命令告诉 `gdb` 在每次调用函数 `findstop` 时停止调试器：

```text
(gdb) break findstop
Breakpoint 1 at 0x0804854: file tabs.c, line 41.
(gdb)
```

调试器通过显示断点编号、断点的十六进制地址以及相应的源行号来确认请求。调试器在你创建断点时按升序对断点进行编号。

本文档由未注册的 ChmMagic 创建，请访问 http://www.bisenter.com 进行注册。感谢。

- `obscure` 隐藏
- `Running` 程序
- `stack` 检查栈
- `status` 状态查询
- `support` 支持设施
- `tracepoints` 在不停止程序的情况下跟踪程序执行
- `userdefined` 用户定义命令

输入 `"help"` 后跟类名，可以列出该类中的命令列表。
输入 `"help"` 后跟命令名，可以查看完整文档。
如果缩写没有歧义，允许使用命令名称缩写。
`(gdb)`

正如列表后的说明中所解释的那样，在输入 `help` 后跟命令类名称或命令名称，将显示更多信息。以下列表显示了数据数据中的命令：

```
(gdb) help data
Examining data.
```

命令列表：

- `append` 将目标代码/数据追加本地文件
- `call` 在程序中调用函数
- `delete` 取消在程序单步执行时显示某些表达式
- `delete` 删除内存区域
- `disable display` 禁用在程序单步执行时显示某些表达式
- `disable mem` 禁用内存区域
- `disassemble` 反汇编内存的特定段
- `display` 每当程序单步执行时打印表达式的值
- `print` 打印表达式 `EXP` 的值
- `printobject` 请求一个对象打印自身
- `print` 打印 `"print format string"`
- `type` 打印类型的定义: `"TYPE"`
- `restore` 将 `FILE` 内容恢复到目标内存
- `set` 评估表达式 `EXP` 并结果赋值给变量 `VAR`
- `set variable` 评估表达式 `EXP` 并结果赋值给变量 `VAR`
- `endisplay` 取消在程序单步执行时显示某些表达式
- `whatis` 打印表达式 `EXP` 的数据类型
- `x` 检查内存: `x/FMT ADDRESS`

```
(gdb)
```

接下来的命令请求关于命令 `whatis` 的信息，该命令接受变量名或其他表达式作为参数：

```
(gdb) help whatis
Print data type of expression EXP.
```
