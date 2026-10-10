
从列表 33.4 可以看出，应用程序的性能相比列表 33.2（优化前）有了显著提高（插入排序提升了五倍）。函数 `bubbleSort` 仅看到适宜的四倍提升。

列表 33.4 针对优化应用程序的 gprof 示例扁平化分析输出

| Flat profile: |
| 每个样本计数为 0.01 秒 | |
| % cumulative self self total |
| time seconds seconds calls ms/call ms/call name |
| 76.47 | 0.78 | 0.78 | 1 | 780.00 | 780.00 | bubbleSort |
| 23.53 | 1.02 | 0.24 | 1 | 240.00 | 240.00 | insertSort |
| 0.00 | 1.02 | 0.00 | 2 | 0.00 | 0.00 | insert_list |

这清楚地说明了 `gprof` 工具（以及 `gcc` 优化器）的用途。你还可以看到 `-02` 优化级别是如何改进源码的。

# gprof可用选项

现在你已经掌握了 `gprof` 的基本用法，可以查看提供的各种选项。虽然 `gprof` 提供了很多，但本节在这里讨论了其中一些更有用的。要查看完整的选项列表，请参考 `gprof` 帮助。

# 源码注释

`gprof` 工具可以根据执行频率对源码进行注释。然而，必须为此目的构建映像。在指定 `-pg` 的同时必须指定 `-g` 和 `-a` 选项：

```
gcc -o sort sort.c -g -pg
```

这将产生一个包含分析信息（通过 `-pg` 选项）以及调试信息（通过 `-g` 选项）的映像。执行映像并检查输出输出如下：

```
gprof -A -1 sort gmon.out
```

你将得到列表 33.5.-A 选项告诉 `gprof` 输出带注释的源码列表。-1 选项指定输出函数执行分析，如下所示：

**列表 33.5** 针对排序应用程序的 gprof 示例源码注释（不完整）

```
#include <stdio.h>

#define MAX_ELEMENTS 10000

void insertSort(int list[], int size) {

    int i, j, temp;

    for (i = 1; i <= size-1; i++) {

        temp = list[i];

        for (j = i - 1; j >= 0 && list[j] > temp; j--) {

            list[j+1] = list[j];

        }

        list[j+1] = temp;

    }

}
```

`-x` 选项也可以用于 `gprof` 以扩展行。

# 忽略私有函数

`-b` 选项可以用于忽略静态声明的私有函数。这可能提供不了太大帮助。

# 推荐函数排序

为了推荐函数排序，可以使用...
.................................33. g.

# 列表 33.7 gprof 示例简短输出

```
Flat profile:

每个样本计数为 0.01 秒

% cumulative self self total

time seconds seconds calls ms/call ms/call name

71.59 | 3.10 | 3.10 | 1 | 780.00 | 780.00 | bubbleSort

28.41 | 1.23 | 1.23 | 1 | 240.00 | 240.00 | insertSort

0.00 | 0.00 | 0.00 | 2 | 0.00 | 0.00 | insert_list

Call graph

index % time | self | children | called | name

[1] | 100.0 | 0.00 | 2.11 | 1/1 | <spontaneous> main [1] |

| | | 1.44 | 0.00 | | bubbleSort [2] |

| | | 0.67 | 0.00 | | insertSort [3] |

| | | 0.00 | 0.00 | 2/2 | init_list [4] |

| | | 1.44 | 0.00 | 1/1 | main [1] |

[2] | 68.2 | 1.44 | 0.00 | 1 | bubbleSort [2] |

| | | 0.67 | 0.00 | 1/1 | main [1] |

[3] | 31.8 | 0.67 | 0.00 | | insertSort [3] |

| | | 0.00 | 0.00 | 2/2 | main [1] |

[4] | 0.0 | 0.00 | 2 | init_list [4]
```

# 第 33 章使用 GNU gprof 进行性能分析

运行此脚本将对 `sort` 程序的五次调用生成单一扁平性能分析（flat profile）。这使用 `gprof` 的 `-sum` 选项将收集到的 `gmon.out` 文件汇总成单个摘要文件 `gmon.sum`。扁平性能分析中的每个/调用（per/call）测量值可以作为更准确的函数计时依据。

## 注意事项

使用 `gprof` 进行性能分析是一个采样过程，可能会受到统计不准确的影响。回想列表 33.7，每个样本计数为 0.01 秒。这就是采样周期。采样时间越接近该周期，性能分析的误差就越大。因此，建议提高性能分析的准确性（参见上一个节，“提高 gprof 准确性”）。当启用 `gprof` 时，它确实会在镜像执行程序中引入额外的代码，这也会影响其行为和性能。因此，仅仅通过测量代码的性能你就会影响它。在使用性能和覆盖率工具时，应该始终记住这一点。

## 总结

本章讨论了使用 GNU 的 `gprof` 进行性能分析，并识别了一些提供的最实用的选项。你学习了如何构建一个供 `gprof` 使用的应用程序并从中获取性能分析数据，包括针对各种 `gprof` 数据产品的选项，以及从缓存角度提高应用程序性能的建议。

## 参考文献

[GNugprof] The GNU Profiler, Jay Fenanson and Richard Stallman 详见于 http://www.gnu.org/software/binutils/manual/gprof-2.9.1/html_mono/gprof.html。

# 34 章 高级调试主题

本章内容

- 使用开源工具进行内存调试
- 交叉引用工具
- 跟踪工具
- 其他技术

## 引言

本最后一章查看了调试 GNU/Linux 应用程序的一些高级技术，并向你展示了如何调整这些技术。它查看了多种用于内存调试和交叉引用的开源工具，以及其他工具和技术。

## 内存调试

你可以从最难调试的问题开始本章，即动态内存问题。这些问题可能表现为无效使用已释放的缓冲区、缓冲区溢出（buffer overruns）或内存泄漏。溢出往往会导致隐蔽的错误，其结果行为可能不是确定性的，并且在新的运行或编译后可能会变为不同的行为。泄漏往往会导致程序冻结或性能严重下降，产生不同的行为。

本节回顾了许多可以帮助你发现程序中内存问题的开源解决方案。

## VALGRIND

Valgrind 是一个用于调试和性能分析的工具套件。该套件中最著名的工具之一被称为 memcheck；它可以帮助发现内存问题（如内存泄漏）。Valgrind 还包含其他工具，如 cachegrind，它可以根据程序的缓存利用率对程序进行注释，以及 massif，这是一个堆分析器（heap profiler）。

获取 Valgrind 工具套件最简单的方法是通过 apt 命令：

```
$ sudo apt-get install valgrind
```

安装后，你将拥有名为 `valgrind` 的二进制文件，其中包含了调试工具套件。越界内存错误不仅常见，而且往往会产生难以追溯到越界错误的问题。当发生越界写入时，另一个对象会被损坏，因此影响可能与越界错误无关。现在是时候看看 Valgrind 的几种用法了。Valgrind 最重要的用途之一是 memcheck。该工具专门监控运行应用程序中的内存使用和分配。你从列表 34.1 显示的示例程序开始。该程序包含特定的错误。然后你可以使用 memcheck 来找到它们。

### 列表 34.1 带有内存错误的示例程序 (test.c)

```
1: #include <stdio.h>

2: #include <stdlib.h>

3: #include <string.h>

4: 

5:     int main()

6: {

7:     char *buffer;

8: 

9:     buffer = (char *)malloc(5);

10: 

11:    strcpy(buffer, "0123456");

12: 

13:    printf("buffer is %s\n", buffer);

14: 

15:    return 0;

16: }
```
