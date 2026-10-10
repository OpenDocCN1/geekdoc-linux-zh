

代码清单 5-4 是 `.../kernel/printk.c` 中的一段代码片段。由于该函数主体与讨论内容无关，因此已被省略。代码清单 5-4 中最相关的部分是最后一行，即对 `__setup` 宏的调用。该宏期望两个参数；在这种情况下，它接收一个字符串字面量和一个函数指针。传入 `__setup` 宏的字符串字面量恰好是与控制台相关的内核命令行前八个字符（即：`console=`）并非巧合。

### 代码清单 5-4
**控制台设置代码片段**

```c
/*
 *      Setup a list of consoles.  Called from init/main.c
 */
static int __init console_setup(char *str)
{
        char name[sizeof(console_cmdline[0].name)];
        char *s, *options;
        int idx;

/*
 * Decode str into name, index, options.
 */

        return 1;
}
__setup("console", console_setup);
```

你可以将这个宏视为内核命令行 `console` 参数的注册函数。实际上，它意味着：**当在内核命令行中遇到 `console=` 字符串时，调用由第二个 `__setup` 宏参数表示的函数——在本例中，即 `console_setup()` 函数。** 但这条信息是如何传递给早期设置代码的呢？这些外部代码并不知晓控制台函数。该机制既巧妙又有些复杂，并依赖于链接器构建的列表。

细节隐藏在一系列宏中，这些宏旨在隐藏向部分目标代码添加*段属性*（以及其他属性）的语法繁琐性。其目标是构建一个关联了字符串字面量和函数指针的静态列表。编译器会在最终的 vmlinux ELF 镜像中，将一个单独命名的 ELF 段中输出此列表。理解这项技术至关重要；它在内核的多个地方用于特殊目的处理。

让我们现在考察在 `__setup` 宏情况下是如何实现这一点的。代码清单 5-5 是来自头文件 `../include/linux/init.h` 的一部分代码，它定义了 `__setup` 宏系列。

### 代码清单 5-5
**来自 `init.h` 的 `__setup` 宏定义系列**

```c
#define __setup_param(str, unique_id, fn, early) \
        static char __setup_str_##unique_id[] __initdata = str; \
        static struct obs_kernel_param __setup_##unique_id \
                __attribute_used__ \
                __attribute__((__section__(".init.setup"))) \
                __attribute__((aligned(sizeof(long)))) \
                = { __setup_str_##unique_id, fn, early }

#define __setup_null_param(str, unique_id)                \
        __setup_param(str, unique_id, NULL, 0)

#define __setup(str, fn)                                  \
        __setup_param(str, fn, fn, 0)
```

代码清单 5-5 正是作者定义的语法繁琐性！回顾代码清单 5-4，我们对原始 `__setup` 宏的调用如下所示：

```c
__setup("console=",  console_setup);
```

经过一些简化，以下是宏展开后编译器预处理器生成的结果：

```c
static char __setup_str_console_setup[] __initdata = "console=";
static struct obs_kernel_param __setup_console_setup
        __attribute_((__section__(".init.setup")))
        { __setup_str_console_setup, console_setup, 0};
```

为了使其更具可读性，我们按照 UNIX 行延续字符 `\` 所示，将第二行和第三行拆开了。

我们有意省略了两个编译器属性的描述，因为它们对本文讨论没有提供任何额外洞察。简而言之，`__attribute_used__`（其本身是一个隐藏更多语法繁琐性的宏）告诉编译器即使优化器确定该函数或变量未被使用，也要输出该函数或变量。⁸ `__attribute__((aligned))` 告诉编译器将结构体对齐到特定边界，在本例中为 `sizeof(long)`。

> ⁸ 通常，如果变量被定义为 `static` 且从未在编译单元中被引用，编译器会发出警告。由于这些变量未被显式引用，若无此指令，警告将会被触发。

## 5.3 内核命令行处理

简化后剩下的就是该机制的核心。首先，编译器生成一个名为 `__setup_str_console_setup[]` 的字符数组，初始化为包含字符串 `console=`。其次，编译器生成一个包含三个成员的结构体：一个指向内核命令行字符串（即刚声明的数组）的指针，一个指向设置函数本身的指针，以及一个简单的标志。这里的魔术关键在于附加在该结构体上的段属性。该属性指示编译器将此结构体输出到 ELF 对象模块中的一个特殊段，名为 `.init.setup`。在链接阶段，所有使用 `__setup` 宏定义的结构体都被收集并放置到这个 `.init.setup` 段中，实际上创建了一个这些结构体的数组。代码清单 5-6 是 `.../init/main.c` 中的一部分，展示了如何访问和使用这些数据。

### 代码清单 5-6
**内核命令行处理**

```c
1  extern struct obs_kernel_param __setup_start[], __setup_end[];
2
3  static int __init obsolete_checksetup(char *line)
4  {
5      struct obs_kernel_param *p;
6
7      p = __setup_start;
8      do {
9          int n = strlen(p->str);
10         if (!strncmp(line, p->str, n)) {
11             if (p->early) {
12                 /* Already done in parse_early_param
13                  * (Needs exact match on param part) */
14                 if (line[n] == '\0' || line[n] == '=' )
15                     return 1;
16             } else if (!p->setup_func) {
17                 printk(KERN_WARNING "Parameter %s is obsolete, "
18                        "ignored\n", p->str);
19                 return 1;
20             } else if (p->setup_func(line + n))
21                 return 1;
22         }
23         p++;
24     } while (p < __setup_end);
25     return 0;
26 }
```

检查这段代码应该相当直接，只需做一些解释。该函数以一个单一的命令行参数被调用，该参数在 `main.c` 的其他地方解析。在我们讨论的例子中，*arg* 将指向字符串 `console=ttyS0,115200`，这是内核命令行的一个组成部分。两个外部结构体指针 `__setup_start` 和 `__setup_end` 在链接器脚本文件中定义，而不是在 C 源代码或头文件中。这些标签标记了放置在对象文件的 `.init.setup` 段中的 `obs_kernel_param` 结构体数组的起始和结束位置。

代码清单 5-6 中的代码通过指针 *p* 扫描所有这些结构体，以查找匹配当前内核命令行参数的内容。在本例中，代码正在搜索字符串 `console=` 并找到了匹配项。从相关的结构体中，函数指针元素返回指向 `console_setup()` 函数的指针，该函数以参数的剩余部分（字符串 `ttyS0,115200`）作为其唯一参数被调用。此过程对内核命令行中的每个元素重复执行，直到内核命令行完全耗尽。

刚刚描述的技术——将对象收集到唯一命名的 ELF 段中的列表——在内核中有很多地方使用。该技术的另一个例子是使用 `__init` 宏系列将一次性初始化例程放入对象文件中的公共段。其近亲 `__initdata`，用于标记一次性使用的数据项，被 `__setup` 宏使用。使用这些宏标记为初始化的函数和数据被收集到一个特别命名的 ELF 段中。后来，在这些一次性初始化和数据对象使用完毕后，内核会释放这些项占用的内存。你可能在启动过程的最后部分见过一条熟悉的内核消息，说：“Freeing init memory: 296K。” 结果可能因情况而异，但使用 `__init` 宏系列的付出换来三百多千字节是值得的。这就是之前 `__setup_str_console_setup[]` 声明中 `__initdata` 宏的目的。

你可能一直在纳闷为什么符号名称前带有 `obsolete_`。这是因为内核开发者正在用一个更通用的机制替换内核命令行处理机制，该机制用于注册启动时和可加载模块参数。目前，有数百个参数是用 `__setup` 宏声明的。然而，新的开发预计将使用内核头文件 `../include/linux/moduleparam.h` 中定义的函数系列，特别是

