
在`leak.c:15`处。

### 7.5.4 dmalloc

与 Electric Fence 和`mpatrol`一样，`dmalloc`是另一种内存调试工具。与其他工具不同，`dmalloc`不需要开发者链接库。相反，它使用`LD_PRELOAD`环境变量来拦截对`malloc`和`free`的调用。`dmalloc`提供了有关内存泄漏的详细信息，并用于检测内存损坏。

`dmalloc`的源码位于`www.gnu.org/software/dmalloc/`。

### 7.5.5 valgrind

`valgrind`是从`http://valgrind.org`获取的内存调试工具。`valgrind`根据 GPL 免费。与其他内存调试工具要求开发者编译并链接库不同，`valgrind`允许在不需要编译的情况下调试。`valgrind`可以报告内存使用、堆使用、多线程应用程序中可能竞态条件以及 L1 和 L2 缓存缺失。

在示例程序上运行`valgrind`的结果如下：

```
$ gcc leak.c -o leak -g

$ valgrind -v --leak-check=full ./leak

==2593==

==2593 4 bytes in 1 blocks are definitely lost in loss record 1 of 1

==2593 at 0xFFB97994: malloc (vg_replace_malloc.c:130)

==2593 by 0x10000430: main (leak.c:15)

==2593==

LEAK SUMMARY:

==2593 definitely lost: 4 bytes in 1 blocks.

==2593 possibly lost: 0 bytes in 0 blocks.

==2593 still reachable: 0 bytes in 0 blocks.
```

`valgrind`在示例 7-6 的第 15 行发现了未释放的内存。注意，程序使用了`-g`选项进行编译，以便`valgrind`获取正确的符号和地址。此外，注意不需要与示例程序链接任何额外的库。

### 7.5.6 Rational Purify

Linux 版 Rational Purify 由 IBM 商业出售。Rational Purify 可以检测内存错误，如泄漏和无效内存访问。与其他内存调试工具仅适用于 C 和 C++ 程序不同，Rational Purify 也适用于 Java 编写的应用程序。Rational Purify 帮助检测导致内存被对象引用持有的 Java 垃圾回收问题。

# 472 第 7 章 • 测试与调试

这些不再需要的内存，或其他来自 JDK 或第三方库的其它内存问题。当与另一个名为 Rational Quantify 的产品结合使用时，可以获得准确的分析数据，用于发现性能瓶颈。Rational Purify 和 Rational Quantify 都拥有专利的代码插入（OCI）技术，用于对 C/C++ 程序进行插桩，以检查逻辑错误并创建分析数据。你可以在`www.ibm.com/software/awdtools/purifyplus/unix`找到更多关于 Rational Purify 的信息。

### 7.5.7 Insure++

`Insure++`是来自`www.parasoft.com`的商可用内存调试工具。它支持运行在 x86 平台上的 Linux 以及 IBM 的 POWER (`ppc`) 平台。在编译和链接应用源代码时，`Insure++`可以实现详细的代码覆盖。该工具生成插桩的对象文件，然后将其传递给实际编译器，从而生成插桩的应用程序代码。`Insure++`可以检测内存损坏、内存泄漏、内存分配错误、变量初始化错误、变量定义冲突、指针错误、库错误、I/O 错误和逻辑错误。

## 7.6 静态程序检查器

在应用迁移过程中，原始代码的更改可能会引入潜在错误，例如引用空指针或拼写错误（会导致无限循环且无法被检测到的错误）。这些错误在编译和链接阶段也可能无法被发现。与构建过程结合使用的静态代码检查器¹⁰可以帮助检测此类错误，创建一个主动的环境，从而在功能测试和系统测试期间消除未来的问题。

### 7.6.1 Splint
`Splint`是一个用于静态检查 C 程序编程错误的工具，例如潜在的内存泄漏、引用空指针、未使用的声明、类型不一致、忽略返回值以及可能存在的无限循环。`Splint`提供的另一个重要功能是检查应用程序中潜在的缓冲区溢出场景。

> 10 有10 种静态程序检查器，例如`Flawfinder` (`www.dwheeler.com/flawfinder/`) 和`Coverity` (`www.coverity.com`)。

### 7.6.2 CodeSonar
`CodeSonar`是一种商用的源代码分析器，它对代码进行深度静态分析并识别许多类型的 bug。这些包括空指针解引用、除零错误、缓冲区溢出、缓冲区下溢、重复释放、释放后使用以及非堆内存的释放。`CodeSonar`进行全程序分析，考虑了由于不同文件中不同函数之间的交互产生的影响。它可以检测出通过手动分析难以识别的复杂 bug。要了解更多`CodeSonar`，请访问`www.grammatech.com`。

你可以在`www.splint.org/links.html`找到开源和商用形式的其他静态分析器列表。

## 7.7 线程跟踪工具
通过一个名为 NPTL trace tool¹¹的开源项目，可以使用新的 POSIX 线程库 (`NPTL`) 以尽可能最小的侵入性来跟踪线程执行。该工具旨在帮助多线程应用程序的开发者，可以生成描述线程行为的跟踪信息，并为理解竞态条件、死锁和锁内容等复杂情况提供帮助。

跟踪工具在被跟踪的应用开始执行时启动，在应用停止时立即停止。生成的跟踪信息可以用文本或图形格式查看。截至本文编写，该工具仅提供测试版本 (`0.8.1`)。它目前跟踪 15 个最常见的 POSIX 线程例程和对象¹²。跟踪工具目前支持的平台包括 IA32、IA64 和 PowerPC 架构。

> 11 `http://nptltracetool.sourceforge.net`
> 12 条件变量、互斥锁、屏障和线程

该工具要求用户下载`glibc`源码并对`NPTL`库应用多个补丁。这些补丁包含 NPTL trace tool 分发包中，并添加了必要的跟踪钩以跟踪线程执行。尽管该工具处于开发的早期阶段¹³，它展示了开源社区对 Linux 进步所出的贡献。

## 7.8 性能监控工具
在新迁移的应用程序发布之前，需要检查其在 Linux 平台上的应用性能和行为。熟悉 Linux 上提供的性能监控工具，以发现问题或性能瓶颈。其中一些工具已包含在标准 Linux 发行版中；另一些是你可以从网上下载的开源工具。

我们从两个视角——内部和外部来处理应用调优。顾顾义，内部视角处理应用程序内部的函数；外部视角处理应用程序运行的环境。两者对客户对应用程序的感知都有直接影响；性能良好的应用程序将比性能缓慢的应用程序拥有更多的用户。接下来我们将讨论这两个视角。

### 7.8.1 内部视角
应用调优的第一个视角是内部视角。内部视角让我们能够观察应用程序内部。使用分析工具是查看应用程序的最佳方式。分析工具可以告诉你你的程序在何处花费了时间，以及哪些函数调用了哪些函数。这些信息可以显示程序中哪些函数比你预期的要慢。你可以对慢速函数进行代码分析，以确定它们是否可以优化。

#### 7.8.1.1 gprof
Linux 提供了一个名为`gprof`的分析工具¹⁴。我们使用`gprof`并展示一个示例。

> 13 在此阶段请务必谨慎使用。
> 14 `www.gnu.org/software/binutils/gprof.html`

使用`-pg`标志编译以启用性能分析：

```bash
$ gcc gprof_1.c -o gprof_1 -lpthread -D_REENTRANT -pg
```

运行程序：

```bash
$ ./gprof_1
non recursive = 165580141
recursive = 165580141
```

程序`gprof_1`会生成一个名为`gmon.out`的文件。`gprof`会解释`gmon.out`¹¹⁵并以可读的形式打印分析信息。

对应用程序运行`gprof`：

```bash
$ gprof ./gprof_1 > outfile
```

```
$ cat outfile ---
```

```
--- 一部分信息被省略 ---
```
