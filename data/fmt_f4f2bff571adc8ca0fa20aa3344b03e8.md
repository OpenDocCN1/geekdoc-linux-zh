
| 选项 | 功能 |
| --- | --- |
| `NO_GLOB (-F)` | 禁用文件名生成。 |

# 156 ZSH-Shell 配置

| 选项 | 功能 |
| --- | --- |
| `NO_HIST_CLOBBER` | 在历史记录的输出重定向中不添加叹号。 |
| `NO_HUP` | shell 退出时不向正在运行的作业发送 `HUP` 信号。 |
| `NO_LIST_BEEP` | 在补全歧义时不蜂声。 |
| `NO_NOMATCH (-3)` | 如果用于文件名生成的模式没有匹配项，则保持其在参数列表中的状态不变，而不是显示错误。这也适用于初始 `~` 或 `=` 的文件扩展。 |
| `NO_PROMPT_CR (-V)` | 在行编辑器打印提示符（`prompt`）之前不打印回车符。 |
| `NO_RCS (-f)` | 仅加载 `/etc/zshrc`。不加载 `~/.zshrc`、`/etc/profile`、`.profile`、`/etc/zshrc`、`/etc/zlogin`、`.zlogin` 或登录文件。 |
| `NO_SHORT_LOOPS` | 禁止 `select`、`if` 和函数构造的短形式。 |
| `NOTIFY (-5)` | 立即报告后台作业的状态，而不是等待显示提示符。 |
| `NO_UNSET (-u)` | 替换时将未设置参数视为错误。 |
| `NULL_GLOB (-G)` | 如果用于文件名生成的模式没有匹配项，则从参数列表中删除该模式而不是报告错误。（覆盖 `NOMATCH`。） |
| `NUMERIC_GLOB_SORT` | 如果文件名通过文件名生成模式匹配，则按数字顺序而非字母顺序进行排序。 |
| `OVERSTRIKE` | 以覆盖模式（`overstrike mode`）启动行编辑器。 |
| `PATH_DIRS (-Q)` | 即使对包含斜杠的命令名也执行路径搜索。 |
| `PRINT_EXIT_VALUE (-C)` | 打印非零状态程序的退出值。 |
| `PROMPT_SUBST` | 在提示符中扩展表达式。 |
| `PUSHD_IGNORE_DUPS` | 忽略重复的 `pushd` 操作。 |
| `PUSHD_SILENT (-E)` | 静默 `pushd` 操作。 |
| `PUSHD_HOME (-D)` | 像参数赋值一样扩展表达式。 |
| `RC_EXPAND (-P)` | 在提示符中扩展。 |
| `RC_EXACT (-S)` | 确切匹配扩展。 |
| `RM_SILENT (-H)` | 静默 `rm` 操作。 |
| `SH_STDIN (-s)` | 从标准输入读取。 |
| `KEYBOARD_LINE (-M)` | 使用单行编辑。 |
| `KEYBOARD_HACK (-L)` | 使用大括号。 |

# 第 4 章 编译器与库：info

尽管有所有编译器和工具的帮助页（`man` pages），通过 `info` 系统可以获得更详细的信息。这些是 `GNU`。

You invoke the main menu of an `info` document by entering the command `info`.

```
$ info
```

You use the `SPACEBAR` to page down the menu. When you find a topic you want, press the `M` key. This opens up a line at the bottom of the screen where you can type in the name of the menu item. On pressing `ENTER`, that document is displayed. Pressing `B` pages you back to the beginning, and `U` takes you up to the previous menu. The command `info info` will bring up a tutorial on how to use `info`.

![](img/3db93a7d263e3b589612548bc59abfdb_177_0.png)

Unix 操作系统与 C 语言之间存在特殊的关系。C 语言是为了编程 Unix 操作系统而开发的，而 Unix 操作系统的代码实际上是用 C 语言编写的。Linux 与此也有类似的特殊关系。大多数 Linux 系统都包含了 `GNU` 版本的 C 编译器。C 语言是一种非常复杂的语言，具有许多功能。本节将简要描述 C 语言的基础，并使用它们构建一个实用的示例。通过示例程序，我们可以检查编译 C 程序的不同方法。

C 程序由一组包含变量声明和语句的函数定义组成。执行始终从名为 `main` 的函数开始。程序在函数之间进行。例如，`printf` 函数是一个经常被调用的函数。

C 函数的定义由头部和函数体组成。头部包含了函数的返回值、函数名以及封装在括号中的参数变量。如果函数没有返回值或参数变量，则使用 `void` 关键字代替。

# C 编译器：gcc 161

你通过首先创建源代码来创建一个 C 程序。源代码文件是一个文本文件，你可以使用任何标准编辑器（如 `Vi`、`Emacs` 或 `Crisprite`）来创建它。你只需要输入函数定义，然后编译源代码文件。

除了函数定义外，C 程序通常还包含所谓的预处理器命令。当你编译 C 程序时，源代码首先由一个预处理器实用程序读取，该程序会生成一个修改后的程序版本，供 C 编译器进行处理。预处理器执行类似于文字处理的操作，生成源代码文件的编辑后的形式。源代码文件中的预处理器命令充当编辑命令，指示预处理器进行哪些更改。所有预处理命令都以井号 (`#`) 符号开头。`#include <stdio.h>` 就是一个预处理器命令。在下一个示例中，`#include` 预处理器命令执行文件插入，将 `stdio.h` 文件的内容与 `greet.c` 源代码合并，生成一个包含 `stdio.h` 内容的 C 程序版本。

`stdio.h` 文件代表标准输入输出。它包含了对 C 程序库中函数的引用。当生成以下 `greet.c` 程序的最终可执行文件时，它将链接到预编译库，这些库中包含了 `printf` 的目标代码。你需要 `stdio.h` 中的引用以确保正确的连接。

## greet.c

```c
#include <stdio.h>
void main(void) {
    printf("Hello, how are you\n");
}
```

你在 Linux 系统上通过 `gcc` 命令调用 `GNU` 编译器。`gcc` 命令反过来调用了四个其他组件。第一个是预处理器。C 程序包含特殊的预处理器命令，它们在代码发送给编译器之前对其进行修改。第二个组件是编译器本身。编译器将处理代码并生成程序的汇编代码版本。第三个组件是汇编器。汇编器将使用程序的汇编代码版本生成目标代码版本。第四个组件是链接器。链接器使用程序的目标代码生成一个可执行文件。它的默认名称是 `a.out`。通常，你应该为可执行文件指定一个自定义名称。`-o` 选项接受文件名作为参数。该文件名将作为可执行文件的名称，而不是默认的 `a.out`。

`gcc` 尽可能接受源代码、目标代码和汇编代码文件，以及多个选项。`gcc` 通过文件扩展名识别文件。

| 扩展名 | 说明 |
| --- | --- |
| `.c` | 源代码文件 |
| `.o` | 目标代码文件 |
| `.s` | 汇编代码文件 |
| `.C` | C++ 文件 |
| `.cpp` | C++ 文件 |

在下一个示例中

```bash
$ gcc greet.c -o greet
$ greet
Hello, how are you
```

`gcc` 工具具有许多选项，可以在任何组件处停止编译过程。这些是用于预处理器的 `-P`、用于汇编器的 `-S` 以及用于编译器的 `-c`。`-P` 选项在预处理器处理完源代码后生成源代码的副本。这个预处理器版本的源文件保存在扩展名为 `.P` 的文件中。例如，`greet.c` 文件的预处理器版本将保存在名为 `greet.P` 的文件中。`-S` 选项生成程序的汇编代码版本。汇编代码版本保存在扩展名为 `.s` 的文件中。`greet.c` 文件的汇编代码版本将保存在名为 `greet.s` 的文件中。`-c` 选项仅生成目标代码文件，而不是带有 `.o` 扩展的可执行文件。`greet.c` 的目标代码版本将保存在名为 `greet.o` 的文件中。在下一个示例中，用户生成了程序的汇编代码版本，然后生成了目标代码版本。

```bash
$ gcc -S greet.c
$ gcc -c greet.c
$ ls
greet.c greet.o
```

| 选项 | 功能 |
| --- | --- |
| `-S` | 输出汇编代码。（编译文件的汇编代码版本扩展名为 `.s`。示例将生成一个名为 `greet.s` 的文件。） |
| `-P` | 输出预处理结果。 |
| `-c` | 仅创建目标代码文件。（编译文件的目标代码版本扩展名为 `.o`。） |
| `-g` | 为使用符号调试器准备好编译后的程序。 |
| `-o filename` | 指定可执行文件名为。（默认是 `a.out`。） |
