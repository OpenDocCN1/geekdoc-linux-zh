
默认情况下，在打印时，`dbug` 库会输出所有 `DEBUG_PRINT()` 语句。第一个参数是一个字符串，可用于将输出限制为仅使用该字符串的 `DEBUG_PRINT()` 宏。

最后，使用 `DEBUG_RETURN()` 宏（第 28 行）来代替普通的 `return` 语句以返回一个值。对于在 `void` 函数中使用，有对应的 `DEBUG_VOID_RETURN` 宏。

程序的其余部分由 `factorial()` 函数完成：

```c
#include <stdio.h>
#include "dbug.h"

int factorial(value)
register int value;
{
    DBUG_ENTER ("factorial");
    DBUG_PRINT ("find", ("find %d factorial", value));
    if (value > 1) {
        value *= factorial (value - 1);
    }
    DBUG_PRINT ("result", ("result is %d", value));
    DBUG_RETURN (value);
}
```

一旦程序被编译并与 `dbug` 库链接，它就可以正常运行。默认情况下，程序不会产生任何调试输出。不过，启用调试后，可以提供不同类型的输出：

```text
$ factorial 1 2 3
1
2
6

$ factorial -Wt 1 2 3
>factorial
|   >factorial
|   |   <factorial
1
>factorial
|   >factorial
|   |   <factorial
>factorial
|   >factorial
|   |   >factorial
|   |   |   <factorial
|   |   <factorial
|   <factorial
2

>factorial
|   >factorial
|   |   >factorial
|   |   |   <factorial
|   |   <factorial
|   <factorial
6
```

正常运行，无调试
显示函数调用跟踪，注意嵌套
常规输出位于 stdout
调试输出位于 stderr

```text
$ factorial -#d 1 2    #Show debugging messages from `DBUG_PRINT()`
?f?unc?: args: argv[2] = 1
factorial: find: find 1 factorial
factorial: result: result is 1
1
?f?unc?: args: argv[3] = 2
factorial: find: find 2 factorial
factorial: find: find 1 factorial
factorial: result: result is 1
factorial: result: result is 2
2
```

`-#` 选项控制 `debug` 库。它是“特殊的”，因为 `DBUG_PUSH()` 会接受整个字符串，忽略开头的 “-#” 字符，尽管如果你愿意，可以使用其他选项，只需将选项参数字符串传递给 `DBUG_PUSH()`（如果你使用 `getopt()`，这是可选的）。

控制字符串由一组选项和参数组成。每组选项和参数通过冒号字符与其他部分隔开。每个选项是一个字母，该选项的参数通过逗号与其分隔。例如：

```bash
$ myprog -#d,m;1:;f,check_salary,check_start_date -f infile -o outfile
```

*d* 选项启用 `DBUG_PRINT()` 输出，但仅当第一个参数字符串是 "mem" 或 "ipc" 之一时。（如果没有参数，则打印所有 `DBUG_PRINT()` 消息。）类似地，*f* 选项将函数调用跟踪限制为仅命名的函数：`check_salary()` 和 `check_start_date()`。

以下列出的选项和参数摘自 `debug` 库手册。方括号内的参数是可选的。我们只包含认为有用的那些；请参阅文档获取完整列表。

- *d*[*,*keywords*]
  - 启用带有指定 *keywords* 的宏的输出。空的关键词列表意味着选择所有关键词。
- *F*
  - 用包含导致输出的宏的源文件名标记每行调试器输出。
- *i*
  - 用该进程的进程 ID 标识发出每行调试或跟踪输出的进程。
- *L*
  - 用导致输出的宏的源文件行号标记每行调试器输出。
- *o*[\, file]
  - 将调试器输出流重定向到指定文件。默认输出流是 stderr。空参数列表会将输出重定向到 stdout。
- *t*[\, N]
  - 启用函数控制流跟踪。最大嵌套深度由 *N* 指定，默认为 200。

为了使讨论更完整，以下是 dbug 库定义的其他宏。

```c
DEBUG\_EXECUTE(string, code)
```

此宏类似于 `DEBUG_PRINT()`：第一个参数是通过 d 选项选择的字符串，第二个是要执行的代码：

```c
DEBUG\_EXECUTE("abort", abort());
```

```c
DEBUG\_FILE
```

这是类型为 `FILE *` 的值，用于与 `<stdio.h>` 例程一起使用。它允许你向调试文件流进行自定义输出。

```c
DEBUG\_LONGJMP(jmp\_buf env, int val)
```

此宏封装了对 `longjmp()` 的调用，接受相同的参数，因此 dbug 库将知道你执行了非局部跳转。

```c
DEBUG\_POP()
```

此宏弹出由 `DEBUG\_PUSH()` 创建的一层保存的调试状态。它比较晦涩；你很可能不会使用它。

```c
DEBUG\_SETJMP(jmp\_buf env)
```

此宏封装了对 `setjmp()` 的调用，接受相同的参数。它允许 dbug 库处理非局部跳转。

在另一种经历中，在我们工作的第一家初创公司中，[16] 我们在我们的产品中使用调试库。它在开发过程中是无价的，并且通过从最终构建中省略 `-DDEBUG`，我们能够构建一个生产版本，而其他源代码没有任何更改。

为了最大限度地利用调试库的好处，你必须在整个程序中一致地使用它。如果你从项目一开始就使用它，这更容易。但作为一个实验，我们发现借助一个简单的 awk 脚本，我们可以花费几个小时的工作将库整合到一个 30,000 行的程序中。如果你能承受额外的开销，最好将其保留在程序的生产构建中，这样你就可以在不必先重新编译的情况下使用它进行调试。

我们发现调试库是 GDB 等外部调试器的良好补充；它提供了一种*有组织且一致*的方式对 C 代码进行插桩。它还相当好地将我们前面章节中分别概述的许多技术结合起来。动态函数调用跟踪功能特别有用，并且对于帮助*学习*你不熟悉的程序行为证明是无价的。

## 15.5.2 内存分配调试器

忽略诸如糟糕的程序设计等问题，对于任何大规模、实用的应用程序，C 程序员最大的单一挑战是动态内存管理（通过 `malloc()`、`realloc()` 和 `free()`）。

大量用于调试动态内存的工具的存在证明了这一事实。这些工具提供的内容存在相当多的重叠。例如：

- 内存泄漏检测：分配后变得无法访问的内存。
- 未释放内存检测：分配但从未释放的内存。从未释放的内存并不总是错误，但检测这些情况允许你验证它们确实是正常的。
- 错误释放检测：内存被释放两次，或传递给 `free()` 的指针并非来自 `malloc()`。
- 已释放内存使用检测：已释放的内存正在通过悬空指针被使用。
- 内存越界检测：访问或存储到分配范围之外的内存。
- 警告未初始化内存的使用。（许多编译器可以对此发出警告。）
- 动态函数跟踪：当发生错误内存访问时，你会得到一个从内存使用位置到分配位置的 traceback。
- 通过使用环境变量来工工具控制。
- 用于原始调试信息的日志文件，可以后处理以生成有用的报告。

一些工具仅记录这些事件。其他工具则安排应用程序以可怕的方式死亡（通过 $SIGSEGV$），以便可以从调试器内部精确定位有问题的代码。此外，大多数工具旨在与 GDB 良好配合工作。

一些工具需要修改源代码，例如调用特殊函数，或使用特殊的头文件、额外的 #define 和静态库。其他工具通过使用特殊的 Linux/Unix 共享库机制来透明地安装自己作为标准库版本的 `malloc()` 和 `free()` 的替代物。

在本节中，我们查看三个动态内存调试器，然后提供指向其他几个工具的指引。

### 15.5.2.1 GNU/Linux mtrace

使用 glibc 的 GNU/Linux 系统提供两个函数，用于在运行时启用和禁用内存跟踪：

```c
#include <mcheck.h>
void mtrace(void);
void muntrace(void);
```

当调用 `mtrace()` 时，库查看环境变量 `MALLOC_TRACE`。预计该变量命名一个可写文件（无论是否存在）。库打开该文件并开始记录有关内存分配和释放的信息。（如果无法打开文件，则不进行记录。文件每次程序运行时被截断

[16] 尽管我们在第一家公司后本应吸取教训，但我们又去了一家第二家公司。从那以后，我们想通了并且通常避免初创公司。当然，你的经历可能不同。

