
```
$ trace ./bad
execve("./bad", ["* 20 vars */]) = 0
uname({sys="Linux", node="camus", ...}) = 0

open("myfile.txt", O_RDONLY)      = -1 ENOENT (No such file or
directory)
read(-1, 0xfffe20, 128)           = -1 EBADF (Bad file descriptor)
stat64(1, {st_mode=S_IFCHR|0620, st_dev=makedev(136, 0), ...}) = 0
```

# 第31章 代码加固

```
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS,
-1, 0) = 0x4017000
write(1, "read \300\357\377\2778Z\10\n", 14) = 14
close(-1) = -EBBADF (Bad file descriptor)
munmap(0x4017000, 4096) = 0
exit_group(-1) = ?
```

执行该程序后，你可以看到 `execve` 系统调用被用于实际启动你的程序。随后你在执行后不久看到一个 `open` 调用，它与你的源代码匹配（第 11 行，列表 31.4）。你可以在右侧看到 `open` 系统调用返回了 `-1`，错误为 `ENOENT`（文件不存在）。这让你立即知道你的应用程序发生了什么。尝试的 `read` 也失败了，错误为坏的文件描述符（因为 `open` 调用失败了）。

`strace` 工具不仅可以用于理解程序的运行，还可以用于理解你可能没有源代码的程序的运行。从系统调用的角度，你可以在某种程度上理解二进制应用程序在做什么。

## 总结

代码加固可能会增加你的开发时间，但它通常会缩短你的调试时间。通过在设计时预判故障，你可以自动提高软件的可靠性和质量，因此这项技术是必须掌握的。本章讨论了各种代码加固技术，以及有助于创建更好的软件并理解其运行的非编码方法。

## 资源

- Linux 和 UNIX 编程 HOWTO，地址：http://www.dwheeler.com/secure-programs/Secure-Programs-HOWTO/index.html。
- Electric Fence `malloc()` 调试器，地址：http://perens.com/FreeSoftware/
- Splint 源代码检查工具，地址：http://www.splint.org/
- Flawinder 源代码检查器，地址：http://www.dwheeler.com/flawinder/
- RATS 源代码检查器，地址：http://www.fortifysoftware.com/security-resources/rats.jsp。
- ITS4 静态漏洞扫描器，地址：http://www.cital.com/its4。

# 第32章 使用 GNU gcov 进行覆盖测试

## 本章内容

- 理解 GNU 的 `gcov` 工具
- 探索 `gcov` 的不同用途
- 为 `gcov` 编译软件
- 理解 `gcov` 的各种数据产品
- 使用 `gcov` 说明问题并进行优化

## 引言

本章探索了 `gcov` 实用程序，并演示了如何使用它来帮助测试以及支持软件剖析分析和优化。你将学习如何构建用于 `gcov` 的软件，然后理解所提供的各种类型的数据。最后，本章研究了在执行覆盖测试时需要避免的事项。

# 什么是 gcov？

本章首先概述了 `gcov` 能为你做什么。`gcov` 工具是一个覆盖测试工具。当它与应用程序一起编译时，`gcov` 工具会监控执行中的应用程序，并识别哪些源代码行已经执行，哪些行尚未执行。此外，`gcov` 还可以识别特定行的执行次数，这对于性能剖析（确定应用程序花费大部分时间的地方）非常有用。因为 `gcov` 可以告诉你哪些行没有被执行，所以它对于确定代码未被测试覆盖很有用。与测试套件配合使用，`gcov` 可以识别所有源代码行是否已充分覆盖 [FSF02]。

本章讨论了与 GNU 3.2.2 版本编译器工具链绑定的 `gcov` 使用。

# 准备镜像

首先看一眼如何为 `gcov` 准备镜像。在接下来的章节中你将获得更多关于 `gcov` 选项的细节，但本节作为一个介绍。你可以使用列表 32.1 显示的简单泡排序源文件作为示例。

## 列表 32.1 说明 gcov 工具的示例源文件（位于 CD-ROM 的 `/ch32/bubblesort.c` 中）

```
1:   #include <stdio.h>
2:
3:   void bubblesSort(int list[], int size )
4:
5:   {
6:      int i, j, temp, swap = 1;
7:
8:      while (swap) {
9:          swap = 0;
10:
11:         for (i = (size-1); i >= 0; i--) {
12:
13:         for (j = 1; j <= i; j++) {
14:
15:             if (list[j-1] > list[j]) {
16:
17:              temp = list[j-1];
18:              list[j-1] = list[j];
19:              list[j] = temp;
20:              swap = 1;
21:
22:         }
23:
24:     }
25:
26:     }
27:
28:    }
29:
30:    }
31:    int main() {
32:    {
33:        int theList[10]={10, 9, 8, 7, 6, 5, 4, 3, 2, 1};
34:        int theList[10]={10, 9, 8, 7, 6, 5, 4, 3, 2, 1};
35:        int i;
36:
37:    /* Invoke the sort algorithm */
38:        bubbleSort(theList, 10);
39:
40:    /* Print out the list */
41:        for (i = 0; i < 10; i++) {
42:            printf("%d\n", theList[i]);
43:        }
44:    }
```

`gcov` 工具与编译器工具链配合使用。这意味着你想要进行覆盖测试的应用程序必须使用特定的选项编译。如下：

`gcov` 实用程序在执行后会产生关于应用程序的统计。现在，你可以运行 `gcov` 来查看测试结果，例如：

```bash
$ gcc -f-coverage ... 
$ ./bubblesort
$ gcov bubblesort.c
```

`gcov` 实用程序在执行后会产生文件。通过查看 `gcov` 产生的文件，你可以看到以下信息：

`gcov` 产生的文件包含了关于应用程序的统计。现在，你可以运行 `gcov` 来查看测试结果，例如：

```bash
$ gcc -f-coverage ... 
$ ./bubblesort
$ gcov bubblesort.c
```

`gcov` 产生的文件包含了关于应用程序的统计。现在，你可以运行 `gcov` 来查看测试结果，例如：

```bash
$ gcc -f-coverage ... 
$ ./bubblesort
$ gcov bubblesort.c
```

`gcov` 产生的文件包含了关于应用程序的统计。现在，你可以运行 `gcov` 来查看测试结果，例如：

```bash
$ gcc -f-coverage ... 
$ ./bubblesort
$ gcov bubblesort.c
```

# 612 GNU/Linux 应用程序编程

```bash
$ gcov -b bubblesort.c
100.00% of 17 source lines executed in file bubblesort.c
100.00% of 12 branches executed in file bubblesort.c
100.00% of 12 branches taken at least once in file bubblesort.c
100.00% of 2 calls executed in file bubblesort.c
Creating bubblesort.c.gcov.
$
```
