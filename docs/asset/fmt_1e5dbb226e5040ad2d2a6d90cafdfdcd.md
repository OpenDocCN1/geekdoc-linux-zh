
# 代码示例

```
9: #include "randapi.h"
10:
11: #define ITERATIONS 1000000L
12:
13: int main()
14: {
15:     void *handle;
16:     char *err;
17:     void (*initRand_d)();
18:     double (*getSRand_d)();
19:     int (*getRand_d)(int);
20:
21:     long i;
22:     long isum;
23:     double fsum;
24:
25:     /* 打开动态库句柄 */
26:     handle = dlopen("/usr/local/lib/myrand.so", RTLD_LAZY);
27:     if (handle == (void *)0) {
28:         fputs(dlerror(), stderr);
29:         exit(-1);
30:     }
31:
32:     /* 访问 initRand() 函数 */
33:     initRand_d = (void (*())())dlsym(handle, "initRand");
34:     err = dlerror();
35:     if (initRand_d == NULL) {
36:         fputs(err, stderr);
37:         exit(-1);
38:     }
39:
40:     /* 访问 getSRand() 函数 */
41:     getSRand_d = (double (*())())dlsym(handle, "getSRand");
42:     err = dlerror();
43:     if (getSRand_d == NULL) {
44:         fputs(err, stderr);
45:         exit(-1);
46:     }
47:
48:
49:     /* 访问 getRand(int) 函数 */
50:     getRand_d = (int (*)(int))dlsym(handle, "getRand");
51:     err = dlerror();
52:     if (getRand_d == NULL) {
53:         fputs(err, stderr);
54:         exit(-1);
55:     }
56:
57:     /* 初始化随机数 API */
58:     (*initRand_d)();
59:
60:     /* 查找 getRand(10) 的平均值 0..9 */
61:     isum = 0;
62:     for (i = 0; i < ITERATIONS ; i++) {
63:
64:         isum += (*getRand_d)(10);
65:     }
66:
67:     printf(" getRand() Average %d\n", (int)(isum / ITERATIONS));
68:
69:
70:     /* 查找 getSRand() 的平均值 */
71:     fsum = 0.0;
72:     for (i = 0; i < ITERATIONS ; i++) {
73:
74:         fsum += (*getSRand_d)();
75:     }
76:
77:     printf(" getSRand() Average %f\n", (fsum / (float)ITERATIONS));
78:
79:
80:     /* 关闭对动态库的句柄 */
81:     dlclose(handle);
82:
83:     return;
84: }
```

这段代码可能比之前的实现看起来复杂一些，但一旦你理解了 DL API 的工作原理，它其实非常简单。我们所做的使用 `dlopen` 打开共享对象文件，然后将对象中的函数赋值给本地函数指针（使用 `dlsym`）。这允许我们随后调用它。当我们完成后，使用 `dlclose` 关闭共享库，引用就会被移除（释放接口使用的任何内存）。

我们通过包含 `dlfcn.h` 头文件使 DL API 对我们可见。使用动态库的第一步是使用 `dlopen` 打开它（行 27）。我们指定了需要使用的库（`/usr/local/lib/libmyrand.so`）以及一个标志位。在两个可能的标志位（`RTLD_LAZY` 和 `RTLD_NOW`）中，我们指定了 `RTLD_LAZY`，以便在执行过程中解析引用，而不是在加载库时立即解析（那是 `RTLD_NOW` 的作用）。`dlopen` 函数返回一个表示已打开库的不透明句柄（`handle`）。请注意，如果发生错误，我们可以使用 `dlsym` 函数提供一个错误字符串并输出到 stdout 或 stderr。

虽然在这个示例中没有必要，但如果我们希望在通过 `dlopen` 打开共享库时调用一个初始化函数，我们可以在共享库中创建一个名为 `*_init*` 的函数。`dlopen` 函数将确保在 `dlopen` 返回给调用者之前调用该 `*_init*` 函数。

下一步是获取我们需要处理的函数的引用。让我们来看下方的代码示例（取自列表 6.5 的第 34–39 行）。

```
34: initRand_d = dlsym(handle, "initRand");
35: err = dlsym();
36: if (err != NULL) {
37:     fputs(err, stderr);
38:     exit(-1);
39: }
```

从这段代码段可以看出，该过程非常简单。API 函数 `dlsym` 在我们的共享库中搜索定义的函数（在本例中，为我们的初始化函数 `"initRand"`）。一旦找到它，它会返回一个 `(void *)` 指针并将其存储在本地函数指针中。然后可以调用它（如第 59 行所示）来执行实际初始化。我们会自动检查错误状态（第 35 行），如果返回了错误字符串，我们将输出它并退出应用程序。

这实际上是用于识别我们想要在共享库中调用的函数。在获取 `initRand` 指针后，我们又获取了 `getRand`（第 42–47 行）以及 `getRand`（第 49–55 行）。

我们的测试应用程序现在本质上是相同的，不同在于我们不再直接调用函数，而是使用函数指针接口来调用它们。为了动态加载接口提供的灵活性，付出这个代价是完全的。

我们测试应用程序的最后一步是关闭库。这是通过 `dlclose` API 函数完成的（第 83 行）。如果 API 发现该共享库没有其他用户，则它会被卸载。可以构建测试镜像，并指定 `-dll`（用于与 libdl 链接）：

```
gcc -ldl test.c -o test
```

# 构建和使用库

与 `dlopen` 提供的类似，`dlclose` 提供了一种机制，允许共享对象导出一个完成例程，该例程在调用 `dlclose` 函数时被调用。开发者只需在共享库中添加一个名为 `*_fini*` 的函数，`dlclose` 将确保在 `dlclose` 返回之前调用 `*_fini*`。

![](img/e2d3d6ad54c540455223ec59a4bf39e6_96_0.png)

就是这样！创建一个利用动态加载共享库的应用程序虽然有一点点痛苦，但它最终可以节省内存。另注意，当应用程序启动时并不总是需要让所有动态函数可见。你可以只让正常运行必需的函数可见，并在需要时再加载其他动态库。

动态加载库的 API 非常简单，为了完整性在此列出：

```
void *dclopen(const char *filename, int flag);
const char *dlerror(void );
void *dlsym(void *handle, char *symbol);
int dlclose(void *handle );
```

![](img/e2d3d6ad54c540455223ec59a4bf39e6_96_1.png)

库的组成取决于它所代表的内容。库应该包含解决特定领域问题所需的所有函数。与领域无特定相关的函数应该被排除，并可能包含另一个库中。

## 工具

现在，让我们来看一些在创建静态、共享或动态库时有用的其他工具。

### file

`file` 工具通过测试文件参数来识别其类型。该工具在许多不同场景中都非常有用，但在这种情况下，它将为我们提供关于共享对象的少量信息。让我们来看一个交互示例：

```
$ file /usr/local/lib/libmyrand.so
/usr/local/lib/libmyrand.so: ELF 32-bit LSB shared object,
Intel 80386, version 1 (SYSV), not stripped
$
```

### GNU/Linux 应用程序编程

因此，通过 `file`，我们看到共享库是一个适用于 Intel 80386 处理器族的 32 位 ELF 对象。它被定义为“not stripped”（未剥离），这简单意味着存在调试信息。

### size

`size` 命令为我们提供了一种非常简单的方法来理解对象的 text、data 和 bss 段。如下我们的共享库使用 `size` 命令的示例所示：

```
$ size /usr/local/lib/libmyrand.so
text data bss dec
2013 264 4 2281 8e9 /usr/local/lib/libmyrand.so
$
```

### nm

要深入对象，我们使用 `nm` 命令。它允许我们查看文件内可用的符号。这是一个使用 `grep` 过滤结果的简单示例：

```
$ nm -n /usr/local/lib/libmyrand.so | grep T
00000608 T _init
000074c T initRand
0000784 T getRand
0000fbe T Rand
```

在这个示例中，我们使用 `nm` 打印共享库内的符号，但只输出带有 T 标签的符号（即 .text 段符号）。我们还使用 `-n` 选项按数字排序输出，而不是按字母顺序。如果我们想知道这些 .text 段的具体大小，可以使用 `-S` 选项：

```
$ nm -S /usr/local/lib/libmyrand.so | grep *
00000608 T _init
000074c T initRand
0000784 T getRand
0000fbe T Rand
0000844 T _fini
```

从这个示例中，可以看到 `initRand` 位于库的相对偏移 `0x74c` 处，大小为 `0x36`（54字节）。还有许多其他选项；`-S` 提供了更多细节。

### objdump

`objdump` 工具与 `nm` 类似，都提供了深入并检查对象内容的能力。`objdump` 最有趣的特性之一是将对象反汇编为原生指令集。这里是 `objdump` 执行此功能的片段：

```
$ objdump -disassemble -S /usr/local/lib/libmyrand.so
...
0000074c <initRand>:
74c:    55              push %ebp
74d:    89 e5            mov %esp,%ebp
74f:    53              push %ebx
753:    83 ec 04        sub $0x4,%esp
797:    e8 00 00 00      call 79c <initRand+0xc>
79c:    5b              pop %ebx
801:    81 c3 fc 11 00 00  add $0x11fc,%ebx
time_t seed;
    seed = time(NULL);
7a3:    83 ec 0c        sub $0xc,%esp
7a6:    6a 09            push $0x0
7a8:    e8 77 fe ff ff  call 674 <init_0+0x28>
7bd:    83 c4 10        add $0x10,%esp
7b0:    89 45 f8          mov %eax,0xffffff8(%ebp)
7b3:    83 ec 0c        sub $0xc,%esp
7b6:    f7 75 78          pushl 0xffffffff(%ebp)
77a:    83 c4 10          add $0x10,%esp
77d:    8b 5d fc          mov 0xfffffffc(%ebp),ebx
780:    c9              leave
781:    c3              ret
782:    90              nop
783:    90              nop
...
```

除了 `-s`（反汇编为原生指令），我们还指定了源代码。问题是我们在编译对象时排除了这些信息。我们可以通过在编译过程中添加 `-g` 来轻松修复此：

```
$ gcc -c -g -fPIC initapi.c
$ gcc -c -g -fPIC randapi.c
$ gcc -shared initapi.o randapi.o -o libmyrand.so
$ objdump -disassemble -S libmyrand.so
```

```
00000790 <initRand>:
/*
void initRand()
{
790:    55              push %ebp
791:    89 e5            mov %esp,%ebp
793:    53              push %ebx
794:    83 ec 04        sub $0x4,%esp
797:    e8 00 00 00      call 79c <initRand+0xc>
79c:    5b              pop %ebx
801:    81 c3 fc 11 00 00  add $0x11fc,%ebx
time_t seed;
    seed = time(NULL);
7a3:    83 ec 0c        sub $0xc,%esp
7a6:    6a 09            push $0x0
7a8:    e8 77 fe ff ff  call 674 <init_0+0x28>
7bd:    83 c4 10        add $0x10,%esp
7b0:    89 45 f8          mov %eax,0xffffff8(%ebp)
7b3:    83 ec 0c        sub $0xc,%esp
7b6:    f7 75 78          pushl 0xffffffff(%ebp)
77a:    83 c4 10          add $0x10,%esp
77d:    8b 5d fc          mov 0xfffffffc(%ebp),ebx
780:    c9              leave
781:    c3              ret
782:    90              nop
783:    90              nop
...
```

# 构建和使用库

## ranlib

`ranlib` 工具是创建静态库时最重要的工具之一。该工具会创建库内容的索引，并将其存储在库文件本身。当库中存在此索引时，构建镜像的链接阶段可以显著加快速度。因此，每当创建一个新的静态库时，都应该执行 `ranlib` 工具。这里展示了一个 `ranlib` 的示例：

```
$ ranlib libmyrand.a
$
```

注意，使用 `ar` 命令配合 `-s` 选项也可以执行相同的操作，如下：

```
$ ar -s libmyrand.a
$
```

## 总结

在本章中，我们探索了程序库的创建和使用。首先讨论了传统的静态库，接着是共享库，最后是动态加载库。我们还研究了源代码，以演示使用 `ar` 命令创建库以及使用 `gcc` 使用库的方法。最后，还讨论了若干基于库的工具，包括 `ldd`、`objdump`、`nm`、`size` 和 `ranlib`。

# 动态库 API

```c
#include <dlfcn.h>
void *dlopen(const char *filename, int flag);
const char *dlerror(void);
void *dlsym(void *handle, char *symbol);
int dlclose(void *handle);
```

# 7 使用 GNU gcov 进行覆盖率测试

在本章中：

- 理解 GNU 的 `gcov` 工具
- 探索 `gcov` 的不同用途
- 为 `gcov` 编译软件
- 理解 `gcov` 的各种数据产品
- 使用 `gcov` 演示问题并进行优化

## 引言

在本章中，我们将探索 `gcov` 工具，并查看它如何用于帮助测试以及支持软件剖析和优化。我们将学习如何构建用于 `gcov` 的软件，然后理解所提供的各种类型的数据。最后，我们将研究在执行覆盖率测试时需要避免的事项。

## 什么是 gcov？
