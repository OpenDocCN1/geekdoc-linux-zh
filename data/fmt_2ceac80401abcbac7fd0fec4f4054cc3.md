
```c
for (int i = 0; i < MAX_ELEMENTS; i++) {
    list[i] = rand() % 100;
}
}
int main() {
    int list[MAX_ELEMENTS];
    input_list(list);
    insertSort(list, MAX_ELEMENTS);
    bubblesort(list, MAX_ELEMENTS);
    return 0;
}
```

## 624 GNU/Linux 应用程序编程

## 列表 33.3 gprof 示例调用图输出

| index % time | self | children | called | name |
|---|---|---|---|---|
| [1] | 100.0 | 0.00 | 2.11 | 1/1 | <spontaneous> main [1] |
| | | 1.44 | 0.00 | 1/1 | bubbleSort [2] |
| | | 0.67 | 0.00 | 2/2 | insertSort [3] |
| | | 0.00 | 0.00 | | insert_list [4] |
| [2] | 68.2 | 1.44 | 0.00 | 1/1 | main [1] |
| | | | | 1 | bubbleSort [2] |
| [3] | 31.8 | 0.67 | 0.00 | 1/1 | main [1] |
| | | | | | insertSort [3] |
| [4] | 0.0 | 0.00 | 0.00 | 2/2 | main [1] |
| | | | 0.00 | 2 | insert_list [4] |

`index` 列是分配给每个元素的唯一数字。`% time` 列表示在给定函数及其子调用中花费的时间占总时间的百分比。`self` 列是花费在函数本身的时间，而 `children` 列是花费在各个子函数中的时间量。请注意，在第一行中，`children` 为 2.11（两个排序函数之和）。这说明排序函数耗尽了所有时间，而 `main` 函数本身没有花费任何有意义的时间。`called` 字段标识了该函数被父函数调用的次数。第一个数字是特定父函数调用该函数的次数，第二个数字是该子函数总共被调用的次数。最后，`name` 列表示函数的名称。在第一行中使用了 `<spontaneous>`（自）。这意味着无法确定父函数（很可能是 C 语言启动初始化）。

现在你已经有了应用程序的性能基准，可以重新构建应用程序并查看如何改进它。在这个示例中，你使用 `-O2` 优化构建来查看它在多大程度上改进了这个简单的应用程序：

```bash
$ gcc -o sort.c -pg -O2
$ ./sort
$ gprof sort gmon.out | more
```

从列表 33.4 可以看出，应用程序的性能相比列表 33.2（优化前）有了显著提高（插入排序提升了五倍）。`bubbleSort` 函数仅看到适度的四倍提升。

## 列表 33.4 优化后应用程序的 gprof 示例扁平分析输出

扁平化分析 (Flat profile):
每个采样计数 0.01 秒。

| % | cumulative | self | | calls | total |
|---|---|---|---|---|---|
| time | seconds | seconds | ms/call | ms/call | name |
| 76.47 | 0.78 | 0.78 | 1 | 780.00 | 780.00 | bubbleSort |
| 23.53 | 1.02 | 0.24 | 1 | 240.00 | insertSort |
| 0.00 | 1.02 | 0.00 | 2 | 0.00 | 0.00 | init_list |

这清楚地说明了 `gprof` 工具（以及 `gcc` 优化器）的用途。你还可以看到 `-O2` 优化级别是如何改进源码的。

## gprof 可用选项

现在你已经掌握了 `gprof` 的基本用法，可以查看提供的各种选项。虽然 `gprof` 提供了许多选项，但本节在此讨论了其中一些更有用的选项。选项的完整列表请参见 `gprof` 帮助。

## 源码注释

可以使用 `gprof` 工具根据执行频率对源码进行注释。然而，必须为此目的构建映像。在指定 `-pg` 的同时必须指定 `-g` 和 `-a` 选项：

```bash
gcc -o sort sort.c -g -pg
```

这将产生包含分析信息（通过 `-pg` 选项）以及调试信息（通过 `-g` 选项）的映像。执行映像并检查生成的输出，如下：

```bash
gprof -A -1 sort gmon.out
```

你将得到列表 33.5。`-A` 选项告诉 `gprof` 输出带注释的源码列表。`-1` 选项指定输出函数执行分析，如下所示：

## 列表 33.5 排序应用程序的 gprof 示例源码注释（不完整）

```c
#include <stdio.h>
#define MAX_ELEMENTS 10000
void insertSort(int list[], int size ) {
    int i, j, temp;
    for (i = 1; i <= size-1; i++) {
        temp = list[i];
        for (j = i-1; j >= 0 && (list[j] > temp); j--) {
            list[j+1] = list[j];
        }
        list[j+1] = temp;
    }
}
```

`-x` 选项也可用于 `gprof` 将计数扩展到源码行。

## 忽略私有函数

对于私有函数，可以通过 `-a` 选项忽略这些统计信息。花费在私有函数的时间归属于调用者，该私有函数不会出现在扁平分析或调用图中。

## 推荐的排序

`gprof` 工具可以建议一种排序方式，以改进在连续内存系统上的 TLB 性能。对于具有多路缓存的系统，这可能不会太大改进。

为了建议排序方式（使用列表 33.1），执行以下命令：

```bash
$ gcc -o sort sort.c -pg
./sort
$ gprof sort gmon.out
```

然后得到的列表显示在列表 33.6 中。

## 列表 33.6 gprof 排序

```
insertSort
bubbleSort
init_list
```

`-b` 选项用于减少输出，如列表 33.7 所示。

## 列表 33.7 gprof 简要输出

扁平化分析：
每个采样计数 0.01 秒。

| % | cumulative | self | | calls | total |
|---|---|---|---|---|---|
| time | seconds | seconds | ms/call | ms/call | name |
| 76.47 | 0.78 | 0.78 | 1 | 780.00 | 780.00 | bubbleSort |
| 23.53 | 1.02 | 0.24 | 1 | 240.00 | insertSort |
| 0.00 | 1.02 | 0.00 | 2 | 0.00 | 0.00 | init_list |

调用图
index % time | self | children | called | name |
|---|---|---|---|---|
| [1] | 100.0 | 0.00 | 2.11 | 1/1 | <spontaneous> main [1] |
| | | 1.44 | 0.00 | 1/1 | bubbleSort [2] |
| | | 0.67 | 0.00 | 2/2 | insertSort [3] |
| | | 0.00 | 0.00 | | insert_list [4] |
| [2] | 68.2 | 1.44 | 0.00 | 1/1 | main [1] |
| | | | | 1 | bubbleSort [2] |
| [3] | 31.8 | 0.67 | 0.00 | 1/1 | main [1] |
| | | | | | insertSort [3] |
| [4] | 0.0 | 0.00 | 0.00 | 2/2 | main [1] |
| | | | 0.00 | 2 | insert_list [4] |

## 列表 33.8 分析应用程序的多次调用

```bash
#!/bin/bash
for i in 'seq 1 5'; do
  ./sort
  mv gmon.out gmon.out.$i
done
gprof -sum sort gmon.out.*
gprof -b --no-graph sort gmon.sum
```
