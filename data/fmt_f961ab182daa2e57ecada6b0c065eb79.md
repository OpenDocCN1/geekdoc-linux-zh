
同样，假设你正在测试一个新的程序库 `libnew.so`（`.so` 是共享库的正常扩展——关于此主题的更多内容请见第 24 章“使用库”），目前存储在 `/home/fred/lib`，在将其作为系统库之前。假设头文件存储在 `/home/fred/include`。因此，为了链接 `libnew.so` 并帮助 `gcc` 找到头文件，你的 `gcc` 命令应该类似于：

```
$ gcc myapp.c -L/home/fred/lib -I/home/fred/include -lnamenew
```

`-l` 选项告诉链接器从指定的库中提取目标代码。在示例中，我想链接 `libnew.so`。一个长期的 UNIX 惯例是库命名为 `lib{something}`，`gcc` 和许多编译器依赖这一惯例。如果你在链接库时没有使用 `-l` 选项，链接步骤将失败，`gcc` 会对 `function_name` 的未定义引用进行抱怨。

## 使用 GNU cc

第 3 章

默认情况下，`gcc` 使用共享库，因此如果你必须链接到静态库，则必须使用 `-static` 选项。这意味着将仅使用静态库。接下来的示例创建了一个链接到静态 `ncurses` 库的可执行文件。第 27 章“使用 ncurses 进行屏幕操作”讨论了使用 `ncurses` 进行用户界面编程：

```
$ gcc cursesapp.c -lncurses -static
```

当你链接到静态库时，生成的二进制文件比使用共享库要大得多。那么，为什么要用静态库呢？一个常见原因是为了确保用户能够运行你的程序——对于共享库来说，代码需要在运行时动态链接，而不是在编译时静态链接。如果程序所需的共享库没有安装在用户的系统上，你将收到错误并且无法运行程序。

`Netscape` 浏览器就是 perfect完美例子。`Netscape` 依赖于 `Motif`，这是一种昂贵的 X 编程工具包。大多数 Linux 用户都负担不起在系统上安装 `Motif`，因此 `Netscape` 实际上在你的系统上提供了两个版本的浏览器：一个链接到共享库的 `netscape-dyn-Motif`，另一个是静态链接的 `netscape-statMotif`。`netscape` “执行文件”本身是一个壳脚本，它可以检查你是否安装了 `Motif` 共享库，并根据需要启动其中一个二进制文件。

### 错误检查与警告

`gcc` 拥有一整类用于错误检查和生成警告的命令行选项。这些包括 `-ansi`、`-pedantic`、`-pedantic-errors` 和 `-Wall`。首先，`-pedantic` 告诉 `gcc` 发出 ANSI/ISO 标准 C 要求的所有警告。任何使用弃用扩展（例如 `gcc` 支持的扩展）的程序都将被拒绝。`-pedantic-errors` 的行为类似，不同在于它抛出错误而不是警告。最后，`-ansi` 会关闭不符合标准的 GNU 扩展。然而，这些选项中的没有任何一个能保证你的代码在通过其中任何一个选项进行编译且没有错误时，是 100% 符合 ANSI/ISO 标准的。

考虑列表 3.2，这是一个非常糟糕的编程格式示例。它将 `main()` 声明为返回 `void`，而实际上 `main()` 返回 `int`，并且它使用 GNU 扩展 `long` 来声明一个 64 位整数。

#### 列表 3.2 非 ANSI/ISO 源代码

```c
1 |
2 | Listing 3.2
3 * pedant.c use -ansi, -pedantic or -pedantic-errors
continues...
```

#### 列表 3.2 续

```c
/* */
#include <stdio.h>
void main(void)
{
    long int i = 0L;
    fprintf(stdout, "*This is a non-conforming C program\n");
}
```

使用 `gcc pedant.c -o pedant`，这段代码在没有任何抱怨的情况下完成了编译。首先，尝试使用 `-pedantic` 编译它：

```
$ gcc -pedantic pedant.c -o pedant
```

再次没有抱怨。这里的教训是，`-pedantic` 强制 `gcc` 发出标准要求的诊断信息。它并不能保证你的代码符合 C 标准。尽管 `main()` 的声明故意是错误的，程序仍然编译成功。现在，使用 `-pedantic-errors`：

```
$ gcc -pedantic-errors pedant.c -o pedant
pedant.c: In function `main'
pedant.c:9: warning: ANSI C does not support `long long'
```

尽管输出了警告，代码仍然被编译。然而，使用 `-pedantic-errors` 时它没有编译，`gcc` 在抛出错误诊断后停止了：

```
$ gcc -pedantic-errors pedant.c -o pedant
pedant.c: In function `main'
pedant.c:9: ANSI C does not support `long long'
$ ls
```

```
a.out* hello.c helper.h killerapp.c
hello.c killerapp* pedant.c
```

重申一下，`-ansi`、`-pedantic` 和 `-pedantic-errors` 编译器并不保证代码符合 ANSI/ISO 标准。它们只是在沿途中与你作斗。指出 `gcc` 的 info 文件中关于使用 `-pedantic` 的注释是很有意义的：

“此选项的设计目的并不是为了有用；它的存在仅仅是为了满足那些否则会声称 GNU GCC 未支持 ANSI 标准的刻板主义者。某些用户尝试使用 `-pedantic'` 来检查程序是否符合严格的 ANSI C 标准。他们很快就会发现它并没有完全达到他们的要求：它发现了一些非 ANSI 做法，但并非全部——只有那些 ANSI C 要求提供诊断的做法。”

### 优化选项

代码优化是尝试提高性能。权衡是编译时间延长以及编译期间内存使用的增加。

`-O0` 选项告诉 `gcc` 减小代码大小和执行时间。它等同于 `-O1`。在此级别执行的优化类型取决于目标处理器，但始终包含至少三个跳转和延迟栈弹出。线程跳转尝试减少跳转操作的数量；延迟栈弹出发生在编译器在函数返回时让参数在栈上堆积，然后一次性弹出，而不是在每个被调用的函数返回时就逐个弹出参数。

`-O2` 优化包含了所有一级优化，加上涉及处理器指令调度的额外微调。在此级别上，编译器会尽力确保处理器在等待其他指令的结果或来自缓存或主内存的数据时，有指令可以执行。该实现是高度特定于处理器的。`-O3` 选项包含了所有 `-O2` 优化、循环展开以及其他特定处理器的特性。

根据你想要的低级优化程度，使用 `-ffastmath`、`-finline` 和 `-unroll`。`-ffastmath` 和 `-finline` 的实现高度特定于处理器。`-O3` 选项包含了所有 `-O2` 优化。

（注：此处原文似乎存在文本重复的异常，已根据逻辑进行翻译处理）

最后，正如我在本章开头提到的，`gcc` 允许你同时优化代码并插入调试信息。优化后的代码会带来调试挑战，因为你声明的变量在优化后的程序可能未被使用、流控制可能会跳转到意想不到的地方、带有常值的语句可能不会执行，而循环内部的语句可能会因为循环被重排而在其他地方执行。不过，我个人的倾向是在考虑优化之前彻底地调试程序。当然，每个人的情况可能有所不同。

#### 注意

但是，请不要将“稍后进行优化”理解为“在设计过程中忽略效率”。在本章的语境下，优化指的是我在本节中讨论的 `gcc` 编译器。良好的设计和高效的算法对整体性能的影响远大于任何编译器优化。事实上，如果你花时间创建一个整洁的设计并使用快速的算法，你可能不需要进行优化，尽管尝试一下也无害处。

### GNU C 扩展

`GCC` 以多种方式扩展了 ANSI 标准。如果你不介意编写明显的非标准代码，其中一些扩展可能非常有用。关于所有复杂的细节，我将引导读者查阅 `gcc` 的 info 页面。这里涵盖的扩展是 Linux 系统头文件和源代码中经常看到的那些。

例如，为了提供 64 位存储单元，`gcc` 提供了 `long long` 类型：

```
long long long_int_var;
```
