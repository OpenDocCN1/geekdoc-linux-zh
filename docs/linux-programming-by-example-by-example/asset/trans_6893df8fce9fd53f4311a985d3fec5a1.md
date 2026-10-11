

    (*a)++;
}

int main(void)
{
    int i = 0;
    while(i < 10) {
        inc(&i);
        printf("%d", i);
    }
    printf("\n");

    return 0;
}

在这个简单的示例中，你不太可能看到速度或代码大小的显著增加或减少，但这应该说明了如何使用 `inline` 关键字。

2. 本示例展示了如何使用 `attribute` 关键字和 `noreturn` 属性，以及如何用例范围（case ranges）。

![](img/be588b36b489136ce784030a08a1d3d4_57_0.png)

## 示例

noreturn.c

```c
/*
 * noreturn.c
 */
#include <stdio.h>

void die_now(void) __attribute__ ((noreturn));

int main(void)
{
    int i = 0;

    while(1) {
        switch(i) {
        case 0 ... 5:
            printf("i = %d\n", i);
            break;
        default:
            die_now();
        }
        ++i;
    }
    return 0;
}

void die_now(void)
{
    printf("dying now\n");
    exit(1);
}
```

请注意，在编写包含如本程序中 `while` 循环那样的无限循环代码时，要确保存在一个逃生出口，例如当循环计数器达到特定值时跳出循环。不过，对于我们的目的而言，它完美地说明了用例范围扩展是如何工作的。该程序的输出为

![](img/be588b36b489136ce784030a08a1d3d4_58_0.png)

## 输出

```
$ ./noreturn
i = 0
i = 1
i = 2
i = 3
i = 4
i = 5
dying now
```

用例范围扩展的行为与普通 case 语句完全相同。当 `i` 变为 6 时，程序流到达 `default` 块，执行 `die_now`，程序终止。

3. 最后一个示例说明了在结构体上使用 packed 属性的效果。程序仅打印结构体及其组成成员的大小。

![](img/be588b36b489136ce784030a08a1d3d4_58_1.png)

## 示例

packme.c

```c
/*
 * packme.c Using gcc's packed attribute
 */
#include <stdio.h>

/* a "packed" structure */
struct P {
    short s[3];
    long l;
    char str[5];
} __attribute__ ((packed));

/* a normal unpacked structure */
struct UP {
    short s[3];
    long l;
    char str[5];
};

int main(void)
{
    struct P packed;
    struct UP unpacked;

    /* print the size of each member for comparison */
    fprintf(stdout, "sizeof char str[5] = %d bytes\n", sizeof(char) * 5);
    fprintf(stdout, "    sizeof long = %d bytes\n", sizeof(long));
    fprintf(stdout, " sizeof short s[3] = %d bytes\n", sizeof(short) * 3);

    /* how big are the two structures */
    fprintf(stdout, "    sizeof packed = %d bytes\n", sizeof packed);
    fprintf(stdout, "    sizeof unpacked = %d bytes\n", sizeof unpacked);

    return 0;
}
```

使用 GNU 扩展 C 语言的任何功能都不需要特殊的编译命令。编译并执行后，该程序的输出为

![](img/be588b36b489136ce784030a08a1d3d4_60_0.png)

## 输出

```
$ gcc packme.c -o packme
$ ./packme
sizeof char str[5] = 5 bytes
        sizeof long = 4 bytes
sizeof short s[3] = 6 bytes
        sizeof packed = 15 bytes
        sizeof unpacked = 20 bytes
```

这两个元素被定义为具有相同的成员。唯一的区别是结构体 P 添加了 packed 属性。输出清楚地表明，每个结构体的成员都需要 15 字节的存储。在 x86 架构上，普通的未打包结构体 UP 多占了五个字节，而打包结构体 P 的大小是其成员大小之和。虽然节省的 5 字节内存看起来不多，但想象一下如果你有一个包含 1,000,000 个这样的元素的数组（在某些应用中并非不切实际）——这将意味着节省了将近 5 兆字节的 RAM。这是一个巨大的差异！

> **注意**
> 普通结构体中的填充（padding）很可能是为了使 str 和 s 在适当的边界上对齐的结果，分别为它们的“实际”大小增加了三和两个字节。ANSI 允许 C 语言的实现者将结构体填充到主机架构的自然字长。因此，尽管 packed 属性有一些明显的好处，但其代价是牺牲了可移植性。

## 使用 egcs

egcs 是实验性（或增强型）GNU 编译器套件。它最初是 gcc 开发的一个实验性步骤，旨在加速 gcc 的开发并开放 gcc 的开发环境。egcs（发音为 eggs，c 发哑音）项目的其他目标包括为 gcc 添加新语言、新优化和新目标（主机处理器架构）。

1999 年 4 月，GNU 项目正式任命 egcs 指导委员会为 gcc 的官方维护者。gcc 自那以后被重命名为 GNU 编译器集合。这段历史教训的要点在于，在某个时间点，egcs 很可能会与 gcc 合并。然而，在此期间，egcs 是一个独立的产品。它也是至少两个发行版中默认的 C/C++ 编译器，因此了解它与 gcc 的区别及增强功能非常重要。有关 egcs 的更多信息，请访问网站 http://egcs.cygnus.com/。

**注意**
*egcs* 当前发布的 1.1.2 版本似乎是 *egcs* 本身的最后一个版本。根据 *egcs* 的网站，下一个发布版本将是 *gcc* 的 *2.95* 版本。

*egcs* 与 *gcc* 完全向后兼容，因此本章关于 *gcc* 的所有内容也适用于 *egcs*。事实上，尽管内核开发团队并未正式认可这样做，你可以使用 *egcs* 无故障地编译 *Linux* 2.2.x 内核，并且它应该能运行得非常好。*egcs* 代表了相对于标准 *gcc* 编译器 2.7.2.3 的重大改进。下一节介绍了其中一些改进。

### 对 *gcc* 的增强

*egcs* 相对于 *gcc* 的大多数增强功能影响的是编译器本身的操作，而非其命令行接口，因此它们远远超出了本书的范围。然而，命令行接口中发生了一些变化，本节将涵盖这些变化。

添加了几个新的警告。`-Wundef` 和 `-Wno-def` 在 `#if` 预处理器指令尝试评估未定义的标识符时生成警告。`-Wsign-compare` 使 *egcs*（和 *gcc*）在代码比较有符号和无符号值时发出警告。`-Wall` 标志已被扩展，用于使 *egcs* 在整数被隐式声明时发出警告。类似地，警告标志 `-Wimplicit-function-declarations` 捕获函数的隐式声明。

调试和优化改进也已进行。例如，除了优化开关 `-O` 的数值参数外，你现在可以使用 `-Os` 来选择代码大小优化而非代码速度优化。选择 *大小* 或 *速度* 优化主要取决于你需要高性能还是节省磁盘空间。如今，既然 RAM 和磁盘空间都相当便宜，选择速度而非 *大小* 很容易。然而，程序的 *大小* 必须从磁盘占用以及执行时所需的内存量来考虑。在磁盘和 RAM 紧张的情况下，选择减小大小而不是提高速度，因为如果程序无法放入磁盘或内存中，那么世界上最快的程序也是无用的。

`-fstack-check` 开关在缺乏此功能的系统上检查栈溢出。为了增强调试能力，添加了新的 *性能分析* 标志。性能分析使你能确定代码执行得有多快，最频繁调用哪些函数，最频繁使用哪些变量，并识别未使用的代码部分（通常称为 *死代码*）或变量。利用这些信息，你可以修改源代码以使程序 *更高效*；*egcs* 还具有对 Checker 内存检查工具的内建支持。此处列出了额外的处理器特定标志：

- `-fprofile-arcs`—使 *egcs* 能够统计函数执行的次数。
- `-ftest-coverage`—为 *gcov* 代码覆盖率分析工具创建数据文件。
- `-fbranch-probabilities`—改进 *egcs* 对代码分支的预测。

最后，`--help` 选项的输出得到了显著改进。

## 接下来是什么

在本章中，你学习了如何使用 GNU C 编译器 *gcc*，以及由于其与 *gcc* 的相似性，如何学习 *egcs*。你构建的大多数程序，即使是单文件程序，都需要很长的编译器调用命令。这种灵活性可能会让你手指疲惫，且输入起来繁琐，因此下一章将向你展示如何使用另一个出色的 UNIX/Linux 工具 *make* 来自动化软件构建过程。在基本理解这两个工具后，你就准备好进入系统编程主题，通过实例开始编程 Linux。

