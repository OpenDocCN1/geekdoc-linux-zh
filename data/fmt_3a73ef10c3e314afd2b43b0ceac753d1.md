
```c
extern struct obs_kernel_param __setup_start[], __setup_end[];
static int __init obsolete_check_setup(char *line)
{
    struct obs_kernel_param *p;
    int had_early_param = 0;

    p = __setup_start();
    do {
        int n = strlen(p->str);
        if (!strnmp(line, p->str, n)) {
            if (p->early) {
                /* 是否已经在 parse_early_param 中处理过了？
                 * (参数部分需要精确匹配)。
                 * 继续迭代，因为我们可能有同名的早期
                 * 参数和初始化设置 */
                if (line[n] == '\0' || line[n] == '=')
                    had_early_param = 1;
            } else if (p->setup_func) {
                printk(KERN_WARNING "Parameter %s is obsolete\n", p->str);
                return 1;
            } else if (p->setup_func(line + n)) {
                return 1;
            }
        }
        p++;
    } while (p < __setup_end());
    return had_early_param;
}
```

对这段代码的检查应该相当直接，只需几处解释。该函数调用时带有一个参数，即内核命令行，该参数在 `...kernel/parms.c` 中进行解析。在我们讨论的示例中，`line` 将指向字符串 `"console=tty5"`，这是内核命令行的一部分。两个外部结构体指针 `__setup_start` 和 `__setup_end` 定义在链接器脚本文件中，而不是 C 源文件或头文件中。这些标签标记了放置在对象文件 `.init.setup` 段中的 `obs_kernel_param` 结构体数组的起始和结束。

列表 5-6 中的代码通过指针 `p` 扫描所有这些结构体，以寻找特定内核命令行参数的匹配项。在这种情况下，代码正在搜索字符串 `console=` 并找到了匹配项。从相关的结构体中，函数指针元素返回指向 `console_setup()` 函数的指针，该函数将参数的剩余部分（字符串 `tty0,115200`）作为唯一参数调用。此过程对内核命令行中的每个元素重复执行，直到内核命令行耗尽。

上述技术——将对象收集到具有唯一命名的 ELF 段中——被广泛用于内核的许多地方。该技术的另一个例子是使用 `__init_function` 宏将一次性初始化例程放置在公共段中。它的“表兄弟” `__init_const` 用于标记一次性数据项，被 `__setup` 宏使用。使用这些宏标记为初始化的函数和数据会被收集到特殊命名的 ELF 段中。稍后，在这些一次性初始化函数和数据释放后，内核会释放这些项目所占用的内存。你可能在内核的最后部分见过熟悉的内核消息。

## 5.4 子系统初始化

许多内核子系统通过 `main.c` 中的代码进行初始化。某些系统是显式初始化的，例如调用 `init_timers()` 和 `console_init()`，这些调用需要尽早执行。另一些则使用与之前描述的 `__setup` 宏类似的技术进行初始化。然后，链接器构建初始化例程的指针列表，并使用一个简单的循环逐个执行。列表 5-7 展示了其工作原理。

```c
static int __init customize_machine(void)
{
    /* 定制平台设备或添加新设备 */
    if (init_machine)
        init_machine();
    return 0;
}
arch_initall(customize_machine);
```

这段代码片段来自 `.../arch/arm/kernel/setup.c`。它是为特定开发板提供定制钩子的一个简单例程。

### 5.4.1 __initcall 宏

注意列表 5-7 所示初始化例程的两个重要点。首先，它是使用 `__init` 宏定义的。正如我们之前看到的，该宏应用了段属性，以声明该函数被放置在 Linux ELF 文件的 `.init.text` 段中。回想一下，将此函数放置在对象文件特殊段中的目的是为了在不再需要时回收它所占用的内存空间。

需要注意的第二点是紧跟函数定义之后的宏：`arch_initcall(customize_machine)`。该宏是 `../include/linux/init.h` 中定义的一系列宏的一部分。这些宏在列表 5-8 中被在此复制。

## 列表 5-8 initcall 宏族

```
#define __initcall(level,fn,id) \
    static initcall_t __initcall__fn##id__used \
    __attribute__((__section(".initcall") level ".init")) = fn

/*
 * 在初始化 SMP 之前的早期初始化调用。
 * 仅用于内置代码，不用于模块。
 */
#define early_initcall(fn)      __define_initcall("early",fn,early)

/*
 * “纯”初始化调用不依赖于任何其他内容，并且纯
 * 初始化无法静态初始化的变量。
 * 这仅用于内置代码，不用于模块。
 */
#define pure_initcall(fn)      __define_initcall("0",fn,0)

#define core_initcall(fn)      __define_initcall("1",fn,1)
#define core_initcall_sync(fn)  __define_initcall("1s",fn,1s)
#define postcode_initcall(fn)    __define_initcall("2",fn,2)
#define postcode_initcall_sync(fn)  __define_initcall("2s",fn,2s)
#define arch_initcall(fn)       __define_initcall("3",fn,3)
#define arch_initcall_sync(fn)  __define_initcall("3s",fn,3s)
#define subsys_initcall(fn)    __define_initcall("4",fn,4)
#define subsys_initcall_sync(fn)  __define_initcall("4s",fn,4s)
#define fs_initcall(fn)        __define_initcall("5",fn,5)
#define fs_initcall_sync(fn)    __define_initcall("5s",fn,5s)
#define rootfs_initcall(fn)     __define_initcall("rootfs",fn,rootfs)
#define device_initcall(fn)    __define_initcall("6",fn,6)
#define device_initcall_sync(fn)  __define_initcall("6s",fn,6s)
#define late_initcall(fn)       __define_initcall("7",fn,7)
#define late_initcall_sync(fn)  __define_initcall("7s",fn,7s)

#define initcall(fn)      __define_initcall(fn)
```

与之前描述的 `__setup` 宏类似，这些宏根据函数名声明了一个数据项。它们还使用 `section` 属性将此数据放置在 Linux ELF 文件中一个唯一命名的段中。这种方法的用处是 `main.c` 可以调用它不了解的子系统的任意初始化函数。正如前面提到的，唯一的其他选择是让 `main.c` 充斥关于内核中每个子系统的知识。

你可以从列表 5-8 中推导出该名称。该段的名称是 `initcall_N`，其中 N 是级别，定义在 1 到 7 之间。还要注意，七个级别中的每个级别都有一个附加 `s` 的段。这用于同步初始化调用。数据项被分配为宏中命名的函数地址。在列表 5-7 和 5-8 定义的示例中，数据项如下（通过省略 `section` 属性进行简化）：

```
static initcall_t __initcall_customize_machine = customize_machine;
```

该数据项被放置在内核对象文件中名为 `.initcall.init` 的段中。

级别 (N) 用于提供初始化调用的顺序。使用 `core_initcall()` 宏声明的函数会在所有所有之前调用。使用 `postcore_initcall()` 宏声明的函数将是调用，依此类推，用 `late_initcall()` 声明的函数是最后一个调用的初始化函数。

以类似于 `__setup` 宏的方式，你可以将这一系列 `*_initcall` 宏视为内核子系统初始化例程的注册函数，这些例程需要在启动时运行且不再运行。这些宏提供了一种在系统启动期间执行初始化例程的机制，以及一种在例程执行后丢弃代码并回收内存的机制。开发者提供了多达七个级别来执行初始化例程。因此，如果你有一个依赖于另一个子系统可用的系统，你可以使用这些级别来强制执行。如果你在内核中 `grep` 字符串 `[a-z]*_initcall`，你会看到这一系列宏被广泛使用。

关于 `*_initcall` 宏族的最后一个说明：多个层级的使用是在 2.6 内核系列开发期间引入的。早版本的内核使用 `__initcall()` 宏为此目的。该宏仍在广泛使用，特别是在设备驱动程序中。为了向后兼容，该宏被定义为 `device_initcall()`，其定义为级别 6 的初始化调用。

## 5.5 init 线程

位于 `...init/main.c` 中的代码负责让内核活跃起来。在 `start_kernel()` 执行了一些基础内核初始化并显式通过名称调用初始化函数后，第一个内核线程被创建。该线程成为名为 `init()` 的内核线程，其进程 ID (PID) 为 1。

## 5.5.2 initcall_debug

一个非常有趣的内核命令行参数允许你在启动过程中观察这些调用的执行情况。你可以通过设置内核命令行参数 `initcall_debug` 来启用它。只需在启动内核时带有 `initcall_debug` 命令行参数即可启用此诊断输出。¹²

以下是你启用这些调试语句时会看到的内容示例：

```
calling uhci_hcd_init+0x0/0x100 0
uhci_hcd: USB Universal Host Controller Interface driver
initcall uhci_hcd_init+0x0/0x100 returned 0 after 5639 usecs
```

在这里，我们看到正在被调用 USB 通用主机控制器接口驱动程序。第一行宣布了要调用 `uhci_hcd_init` 函数的意图，这是一个来自 USB 驱动程序的驱动初始化调用。在声明之后，就会执行对该函数的调用。第二行由驱动程序本身打印。第三行的追踪信息包含了返回结果和调用的持续时间。

这是查看内核初始化细节的一种有用方法，特别是各种子系统和模块被调用的顺序。更有趣的是调用的持续时间。如果你关心系统启动时间，这是隔离启动过程中时间消耗所在处的极佳方法。

即使在配置简单的嵌入式系统上，也有几十个这样的初始化函数以这种方式被调用。此示例取自 ARM XScale 嵌入目标，使用默认配置编译。默认配置导致了 206 次对各种内核初始化例程的调用。

## 5.5.3 最后启动步骤

在产生 `kernel_init()` 线程之后，在所有初始化调用完成后，内核执行其启动序列中的最后步骤。这些步骤包括释放初始化函数和数据使用的内存、打开系统控制台设备以及启动第一个用户空间进程。列表 5-11 重现了来自 `main.c` 的内核 `init` 过程的最后步骤。

> ¹² 你可能需要降低系统的默认日志级别（loglevel）才能看到这些调试信息。在许多关于 Linux 系统管理的参考书中都有此描述。无论如何，你都可以在内核日志文件中看到它们。

## 列表 5-11 来自 main.c 的内核最后启动步骤

```c
static noinline int init_post(void)
    __releases(kernel_lock)
{
    <... 为了清晰起见省略了行 ...>
if (execute_command) {
    run_init_process(execute_command);
    printk(KERN_WARNING "Failed to execute %s. Attempting \n%defaults...\n", execute_command);
}
}

run_init_process("/bin/init")
run_init_process("/etc/init")
run_init_process("/bin/init")
run_init_process("/bin/sh")

panic("No init found. Try init=option to kernel.");
```

注意，如果代码执行到 `init_post()` 函数的末尾，就会发生内核恐慌。如果你花过时间实验嵌入式系统或自定义根文件系统，你无疑在控制台输出的最后一行遇到过这个非常常见的错误信息。它是各种 Linux 和嵌入式系统相关公共论坛上最常问的问题（FAQs）之一。

无论如何，这些 `run_init_process()` 命令中必须有一个无错误地继续执行。`run_init_process()` 在成功调用后不会返回。它会用新进程覆盖调用进程，实际上是用新进程替换当前进程。它使用熟悉的 `execve()` 系统调用来实现此功能。最常见的配置是将 `/sbin/init` 作为用户态初始化进程。我们将在下一章学习这一功能。

嵌入式系统开发者的一种选项是创建一个自定义的用户初始化程序。这就是前面代码片段中条件语句的目的。如果 `execute_command` 不空，它指向该命令。如果 `execute_command` 为空，则会使用默认的 `/sbin/init`。我们将在下一章研究这一功能。

正如你很快将看到的，根文件系统对 Linux 系统有特殊要求。Linux 期望根文件系统包含启动系统所需的程序和工具、初始化服务（如网络和系统控制台）、加载设备驱动程序以及挂载额外的文件系统。

# 第 6 章 用户空间初始化

## 6.1.1 FHS：文件系统层次级标准

几位内核开发人员编写了一项用于规范 UNIX 文件系统组织和布局的标准。文件系统层次级标准（FHS）为 Linux 发行版与应用程序之间建立了一个微型兼容性基准。你将在本章的最后一部分找到对该标准的引用。我们鼓励你查阅 FHS，以更好地了解 UNIX 文件系统组织布局及其原理的背景知识。

许多 Linux 发行版的目录布局与 FHS 标准中描述的布局密切匹配。该标准的存在是为了在不同的 UNIX 和 Linux 发行版之间提供一个共同基础的元素。FHS 允许你的应用程序软件（以及开发者）预测文件系统中系统中某些系统元素（包括文件和目录）的位置。

## 6.1.2 文件系统布局

在考虑空间的情况下，许多嵌入式系统开发者会在启动设备（如闪存存储器）上创建一个非常小的根文件系统。随后，会从另一个设备挂载较大的文件系统，可能是硬盘或网络文件系统 (NFS) 服务器。事实上，在原始小根文件系统之上挂载一个更大的根文件系统并不罕见。当我们在本章稍后的部分检查初始内存磁盘（initramfs）时，你会看到这样一个示例。

一个简单的 Linux 根文件系统可能包含以下顶级目录项：

```
||
|--bin
|--dev
|--etc
|--home
|--lib
|--sbin
|--usr
|--var
|--tmp
```

### 表 6-1 顶级目录

| 目录 | 内容 |
| --- | --- |
| bin | 二进制可执行文件，系统上的所有用户均可用¹ |
| dev | 设备节点（参见第 8 章“设备驱动程序基础”） |
| etc | 本地系统配置文件 |
| home | 用户账户文件 |
| lib | 系统库，例如标准 C 库及许多其他库 |
| sbin | 通常留给系统上超级用户账户的二进制可执行文件 |
| tmp | 临时文件 |
| usr | 用于应用程序的二级文件系统层次结构，通常为只读 |
| var | 包含可变文件，如系统日志和临时配置文件 |

Linux 文件系统层次结构的顶端由斜杠字符 (`/`) 本身引用。要列出根目录的内容，你需要输入：

```
$ ls /
```

这会产生一个类似于下面的列表：

```
root@coyote:/# ls /
bin dev etc home lib mnt proc root sbin tmp usr var
root@coyote:/#
```
