
最著名的库之一是标准 C 库，它包含一套 ANSI C 函数（字符串函数、数学函数等）。最流行的之一是 GNU C 库 (`libc`)，它是标准 C 库的 GNU 版本。标准 C 库也有轻量级版本，如 `newlib`、`uClinic` 和 `dietlib`（非常适合嵌入式应用）。

共享库或动态库也与应用程序镜像链接，但分为两个独立的阶段。在第一阶段（应用程序构建时），链接器会验证构建应用程序所需的所有符号（函数或变量）是否在应用程序或库中可用。共享库并不是将元素从库中拉取到应用程序镜像中（像静态库所做），而是在第二阶段（运行时），动态加载器将所需的共享库拉入内存，并将应用程序镜像与它们进行动态链接。这些步骤生成的镜像更小，因为共享库与应用程序镜像是独立的（见图 7.1）。

![](img/f7bd35eb87a62f74c6f23c07df847dff_94_1.png)

图 7.1 静态库与共享库的内存节省。

# 第 7 章 构建与使用库 75

共享库节省内存的代价是库必须在运行时进行解析。这需要少少的时间来确定哪些库是必要的，然后将它们带入内存。

接下来的章节将带你使用静态和共享方法构建几个库，以观察它们是如何构建的，以及程序为了支持这些库发生了什么变化。

## 构建静态库

首先，看看 GNU/Linux 中最简单的库开发类型。静态库与应用程序镜像静态链接。这意味着在构建镜像后，外部库不需要存在，镜像即可正常执行，因为它是生成镜像的一部分。

为了演示库的构建，请查看示例源文件。该示例使用 GNU/Linux 随机函数构建了一个简单的随机数封装库。首先查看我们库的 API。头文件 `randapi.h` 所示在列表 7.1 中。

### 列表 7.1 随机数封装 API 头文件（位于光盘的 `/source/ch7/statsrd/randapi.h`）

```
1:  /*
2:      * randapi.h
3:      *
4:      * 随机函数 API 文件
5:      *
6:      */
7:
8:
9:  #ifndef __RAND_API_H
10:     #define __RAND_API_H
11:
12:     extern void initRand( void );
13:
14:     extern float getSRand( void );
15:
16:     extern int getRand( int max );
17:
18: #endif /* __RAND_API_H */
```

# 76 GNU/Linux 应用程序编程

此 API 由三个函数组成。第一个函数 `initRand()` 是初始化函数，用于为封装库做好准备。在调用任何随机函数之前，必须调用它一次。函数 `getRand()` 返回一个 0.0 到 1.0 之间的随机浮点值。最后，函数 `getRand(x)` 返回一个 0 到 `(x-1)` 之间的随机整数。

虽然此功能可以在单个文件中实现，但为了演示，此示例将其拆分为两个文件。下一个文件 `initrand.c` 为封装 API 提供初始化函数（见列表 7.1）。

## GNU/Linux 应用编程

你现在有了一个名为 `libmyrand.a` 的新文件，这是你的静态库，包含两个对象：`initapi.o` 和 `randapi.o`。现在来看如何使用这个静态库来构建你的应用程序。考虑以下内容：

你使用 `gcc` 编译 `test.c` 文件，然后将 `test.o` 对象与 `libmyrand.a` 链接生成 `test` 映像文件。`-L` 选项告诉 `gcc` 可以在当前子目录中查找库（点代表目录）。注意，你也可以指定特定的子目录，例如 `-usr/mylibs`。`-l` 选项标识要使用的库。注意，`myrand` 并不是你的文件名，而是 `libmyrand.a`。当使用 `-L` 选项时，它会自动为指定的名称加上 `lib` 和 `.a`。因此，如果你指定了 `-ltest`，`gcc` 将寻找名为 `libtest.a` 的库。

既然你已经知道了如何创建库并使用它构建静态应用程序，你可以回到 `ar` 工具来查看它还具有哪些功能。你可以使用 `-t` 选项检查静态库以查看其中包含的内容：

```
$ ar -t libmyrand.a
initapi.o
randapi.o
$
```

如果需要，你还可以从静态库中移除对象。这是通过 `-d` 选项实现的，例如：

```
$ ar -d libmyrand.a initapi.o
$ ar -t libmyrand.a
randapi.o
$
```

需要注意的是，`ar` 在删除失败时实际上不会显示错误。为了在删除失败时显示错误消息，请如下所示添加 `-v` 选项：

```
$ ar -d libmyrand.a initapi.o
$ ar -dv libmyrand.a initapi.o
No member named 'initapi.o'
$
```

在第一种情况下，你尝试删除对象 `initapi.o`，但没有生成错误消息（尽管它在静态库中并不存在）。在第二种情况下，你添加了详细模式（verbose）选项并得到了相应的错误消息结果。

与其从静态库中移除对象，不如使用 `-x` 选项将其提取出来。

```
$ ar -xv libmyrand.a initapi.o
x - initapi.o
$ ls
initapi.o libmyrand.a
$ ar -t libmyrand.a
randapi.o
initapi.o
$
```

提取选项与详细模式 (`-v`) 结合，这样你就可以看到 `ar` 正在做什么。`ar` 工具会响应被提取的文件（`x - object`），你可以在对子目录执行 `ls` 后看到它。这里注意，在提取后你也列出了静态库的内容，你的 `initapi.o` 对象仍然存在。提取选项并不会真正移除对象，它只是将其拷贝到归档外部。必须使用删除 (`-d`) 选项才能从静态库中彻底移除。

`ar` 工具的选项列表见表 7.1。

### 表 7.1 ar 工具的重要选项

| 选项 | 名称 way | 示例 |
| --- | --- | --- |
| -d | 删除 | ar -d <archive> <objects> |
| -r | 替换 | ar -r <archive> <objects> |
| -t | 列表显示 | ar -t <archive> |
| -x | 提取 | ar -x <archive> <objects> |
| -v | 详细模式 | ar -v |
| -c | 创建 | ar -c <archive> |
| -ru | 更新对象 | ar -ru <archive> <objects> |

## 构建共享库

现在是再次尝试测试应用程序了，这次使用共享库而不是静态库。这个过程本质上一样简单。首先，使用 `initapi.o` 和 `randapi.o` 对象构建共享库。在构建共享库的源码时，需要进行一项更改。因为库和应用程序没有像在静态库中那样绑定在一起，因此生成的库不能假设绑定应用程序的任何情况。例如，在地址址中，引用必须是相对的（通过使用 GOT，即全局偏移表）。加载器在加载共享库时会解析所有的 GOT 地址。为了编译位置无关的源文件，我们使用 `gcc` 的 `-fPIC` 选项：

```
$ gcc -fPIC initapi.c
$ gcc -fPIC -o randapi.c
```

这产生了两个包含位置无关代码的新对象文件。你可以使用这些 `gcc` 和 `-shared` 标志创建共享库。该标志指示要创建一个共享库：

```
$ gcc -shared initapi.o randapi.o -o librand.so
```

你指定两个模块并通过输出文件 (`-o`) 作为你的共享库。注意，你使用 `.so` 后缀来标识该文件为共享对象（shared object）。

使用新的共享对象构建应用程序，你可以像之前处理静态库一样将元素重新链接在一起：

```
$ gcc test.c -L. -lmrand -o test
```

你可以通过 `ldd` 命令判断新映像是否依赖于共享库。`ldd` 命令打印指定应用程序的共享库依赖。例如：

```
$ ldd test
librand.so => not found
libc.so.6 => /lib/tls/libc.so.6 (0x042000000)
/lib/ld-linux-x86-64.so.2 (0x00007ffff000)
```

`ldd` 命令打印指定应用程序的共享库依赖。例如：

```
$ ldd test
librand.so => not found
libc.so.6 => /lib/tls/libc.so.6 (0x042000000)
/lib/ld-linux-x86-64.so.2 (0x00007ffff000)
```

`ldd` 命令打印指定应用程序的共享库依赖。例如：
