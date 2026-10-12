
# 附录 D：系统启动

## D.1 IA-32 系统上的特定特定设置

一旦内核通过引导程序（`arch/x86/boot/header.S`）（LILO、GRUB 等）加载到物理内存中，就会通过跳转语句将控制流切换到内存中的相应点，从而调用设置汇编`function`。这是可能的，因为 `setup` 函数始终位于目标文件的相同位置。

代码执行以下任务，这些任务需要大量的汇编代码：

- 1. 它检查内核是否被加载到内存中的正确位置。为了做到这一点，它使用集成在内核镜像中的 4 字节签名，该签名必须原封不动地位于 RAM 中的正确位置。
- 2. 它确定系统内存的大小。
- 3. 它初始化显卡。
- 4. 它将内核镜像移动到内存中，避免在随后的解压缩过程中产生自我干扰。
- 5. 它将 CPU 切换到保护模式。

完成这些任务后，代码跳转到 `startup_32` 函数（位于 `arch/x86/boot/compressed/head_32.S`），它执行以下操作：

- 1. 它创建了一个临时栈。
- 2. 它用空字节填充未初始化的内核数据。相关区域位于 `_edata` 和 `_end` 常量之间。当内核被链接时，这些常量会自动为内核二进制文件提供正确的值。
- 3. 它调用了 `arch/x86/boot/compressed/misc_head32.c` 中的 C 程序 `decompress_kernel`。该程序解压缩内核并将解压缩后的机器码写入位置 `(0x100000,1)`，紧跟在第一个 MB 内存之后。解压缩是内核执行的首个操作，正如屏幕消息“Uncompressing Linux...” 和“Ok, booting.” 所示。

处理器特定初始化的最后部分通过将控制权重定向到 `arch/x86/kernel/head_32.S` 中的 `startup_32` 开始。

> 这与之前描述的 `startup_32` 函数不同，并且定义在不同的文件中。内核就不必担心这两个“函数”具有相同的标签，因为它直接跳转到相应的地址，该地址是由汇编器进行补丁处理的，并且与源代码中的符号标签没有关联。

¹如果内核作为可重定位内核启动，地址可能会有所不同，但这种场景在此并不相关。

本节负责以下步骤：

- 1. 激活分页模式并设置最终内核栈。
- 2. 用空字节填充位于 `__bss_start` 和 `__bss_stop` 之间的 `.bss` 段。
- 3. 初始化中断描述符表。然而，中断会进入 `ignore_init` 伪程序 ——实际的处理程序会被安装。
- 4. 检测处理器类型。使用 `.cpuid` 语句来识别现代型号。它返回有关处理器类型和功能的信息，但它不区分 80386 和 80486 处理器 —— 这是通过各种既不重要也不无趣的汇编技巧完成的。

平台特定初始化现在完成，代码跳转到 `start_kernel` 函数。与之前描述的代码不同，此函数被实现为普通的 C 函数，因此更容易处理。

## D.2 高级初始化

`start_kernel` 作为一个分发器来执行与平台无关和依赖平台的任务，所有这些任务都用 C 实现。它负责调用几乎所有子系统的高级初始化程序。用户可以识别内核何时进入初始化阶段，因为该函数显示的第一内容是屏幕上的 Linux 横幅。例如，在用户的某个系统上显示了以下消息：

```
Linux version 2.6.24-default (wolfgang@schroedinger) (gcc version 4.2.1 (SUSE Linux)) #1 SMP PREEMPT Mar 20 00:17:06 CET 2008
```

> 该消息在启动操作早期生成，但在控制台系统初始化之前不会显示在屏幕上。在中间期间，它是被缓冲的。

在随后的步骤中，屏幕输出的数量急剧增加，因为正在初始化的子系统会在控制台上显示广泛的状态信息。这些信息非常有用，特别是对于故障排除。

接下来的章节将详细讨论 `start_kernel`，并阐明在完成体系相关阶段后的内核启动过程。

### D.1 子系统初始化

图 D-1 显示了代码流图，用于说明函数的任务和目标。

第一步是输出版本消息。消息文本存储在 `init/version.c` 中定义的 `linux_banner` 变量中。随后是进一步的体系特定初始化步骤，这些步骤不再处理底层处理器细节，而是用 C 编写，并且在大多数系统上的主要任务是为高级内存管理初始化设置框架。一旦解释了启动时传递给内核的命令行参数，`start_kernel` 就会执行初始化工作 —— 设置各种内核子系统的中心数据结构。这是一个非常全面的任务，因为它涉及到几乎所有的子系统。因此，它被拆分成许多短程序，这些程序在后续章节中描述。最后一步是生成内核在无事可做时调用的进程。init 进程也以 PID 1 启动 —— 它运行各种子系统的初始化程序，然后启动 `/bin/init`。这结束了初始化。

图 D-1：`start_kernel` 代码流图。

## 体系特定设置

顾其名，`setup_arch` 是一个体系特定的函数。它执行用 C 编写的任务，主要关注内存初始化。为了简单起见，本节检查了 IA-32 系统上 `setup_arch` 的实现。图 D-2：`setup_arch` 代码流图。

## 解析命令行参数

`parse_args` 由 `start_kernel` 中的 `parse_early_param` 调用，并负责解释启动时传递给内核的命令行参数。遇到的信息与用户空间中的相同 —— 格式为 `key1=val2` 的字符串键值对必须被分解为各个组成部分。这些选项必须保存在内核中或触发特定的响应。

```c
typedef int (*param_get_fn) (char *buffer, struct kernel_param *kp);

struct kernel_param {
    const char *name;
    param_set_fn set;
    param_get_fn get;
    union {
        void *arg;
        const struct kparam_string *str;
        const struct kparam_array *arr;
    };
```

`name` 是参数的名称，`set` 和 `get` 函数用于设置和读取参数值。`arg` 是一个（可选的）参数，也会被传递给前面的函数。正如预期的那样，它允许同一个函数用于不同的参数。该指针也可以被特定地解释为字符串或数组。

参数通过以下方式在内核中注册：`module_param`、`module_param_named` 等。它们会填充一个 `kernel_param` 实例并填入适当的值，并将它们写入二进制文件的 `__param` 节中。

这极大地简化了启动时的解释工作。需要的是一个循环，执行以下操作，直到所有参数都处理完毕：

- 1. `next_arg` 从内核提供的命令行字符串文本中提取键名/值对。
- 2. `parse_one` 遍历所有已注册的参数列表，将传递的值与 `kernel_param` 实例的 `name` 元素进行比较，并在找到匹配时调用 `set` 函数。

# 初始化数据结构和缓存

快速浏览以下内核源码，`start_kernel` 最实质性的任务是调用所有重要内核子系统的 `initialize` 函数：

```c
init/main.c
asmlinkage void _init start_kernel(void)
{
    trap_init();
    rcu_init();
    init_IRQ();
    pidhash_init();
    sched_init();
    init_timers();
    hrtimers_init();
    softirq_init();
    timekeeping_init();
    time_init();
    profile_init();
}
```

```c
early_boot_irqs_on();
local_irq_enable();
/*
*  {警告！现在还很早。我们在完成 PCI 设置等之前
* 就启用了控制台，console_init() 必须意识到
* 这一点。但我们想尽早输出，以防发生某些错误。
*/
console_init();
```

```c
mem_init();
kmem_cache_init();
calibrate_delay();
pidmap_init();
pgtable_cache_init();
```

```c
vfs_caches_init(num_physpages);
radix_tree_init();
ssignals_init();
/* 根填充需要页面回写 */
```
