
## 5.4 子系统初始化

许多内核子系统是通过 `main.c` 中的代码初始化的。某些子系统被显式初始化，通过调用 `init_timers()` 和 `console_init()`，这些调用需要在非常早的时候进行。其他子系统使用与之前描述的 `_setup` 宏非常相似的技术进行初始化。简而言之，链接器构建了指向初始化例程的函数指针列表，并使用简单的循环顺序执行每一个。列表 5-7 显示了如何工作。

### 列表 5-7 示例初始化例程

```c
static int __init customize_machine(void)
{
    /* 定制设备，或添加新设备 */
    if (init_machine)
        init_machine();
    return 0;
}

arch_initcall(customize_machine);
```

这段代码片段来自 `.../kernel/params.c`。注意 5.4 关于 `initcall` 的两个重要点：关于以 `obsolete_` 开头的符号名称的使用。这是因为内核开发者正在用一种更通用的机制来替换内核行处理机制，以同时注册时间和可加载模块参数。目前，参数的处理程序是用 `__setup` 声明的。预计新开发将使用内核头文件 `.../include/linux/moduleparam.h` 定义的函数族，特别是 `module_param*` 族。这些将在第 8 章“设备驱动基础”在我们介绍设备时进行更详细的解释。

新机制通过在解析例程中包含一个未知指针参数来保持兼容性。因此，对于 `module_param` 基础设施未知的参数被视为未知的，并在开发者的控制下回退到旧机制。通过检查 `.../kernel/params.c` 中众名的代码以及 `.../init/main.c` 中的 `parse_args()` 调用可以很容易理解这一点。

最后一个值得提到的是 `__setup` 宏创建的 `obs_kernel_param` 结构体中 `flag` 成员的用途。检查列表 5-6 中的代码应该就会一目了然。结构体中名为 `early` 的标志用于指示此特定的命令行参数是否在启动过程早期已经被过过。某些命令行参数旨在在启动过程极早期被消费，此标志为早期解析算法提供了一种机制。你将在 `main.c` 中找到一个名为 `do_early_param()` 的函数，它遍历由链接器生成的 `_setup` 结构体数组，并处理每个被标记为早期消费的项目。这让开发者对该启动过程正在执行的操作有一定的控制。

### 5-8 initcall 族

```c
#define initcall(fn) \
    static initcall_t initcall_##fn __attribute__ ((section(".initcall"))) = fn;

#define core_initcall(fn) \
    static initcall_t core_initcall_##fn __attribute__ ((section(".initcall0"))) = fn;

#define postcore_initcall(fn) \
    static initcall_t postcore_initcall_##fn __attribute__ ((section(".initcall1"))) = fn;

#define arch_initcall(fn) \
    static initcall_t arch_initcall_##fn __attribute__ ((section(".initcall2"))) = fn;

#define device_initcall(fn) \
    static initcall_t device_initcall_##fn __attribute__ ((section(".initcall3"))) = fn;

#define subs_initcall(fn) \
    static initcall_t subs_initcall_##fn __attribute__ ((section(".initcall4"))) = fn;

#define russian_initcall(fn) \
    static initcall_t russian_initcall_##fn __attribute__ ((section(".initcall5"))) = fn;

#define late_initcall(fn) \
    static initcall_t late_initcall_##fn __attribute__ ((section(".initcall6"))) = fn;

#define early_initcall(fn) \
    static initcall_t early_initcall_##fn __attribute__ ((section(".initcall7"))) = fn;
```

## 5.5 init 线程

在 `.../init/main.c` 中找到的代码负责让内核运行。在 `start_kernel()` 执行了一些基础内核初始化并按名称调用了早期初始化函数后，第一个内核线程被创建了。该线程最终会变成名为 `init()` 的内核线程，其进程 ID（PID）为 1。正如我们将学到的，`init()` 成为用户空间所有 Linux 进程的父进程。在启动序列的此时，有两个不同的线程正在运行：一个是 `start_kernel()`，另一个是 `init()`。前者在完成工作后将变为空闲进程（idle process）。后者变为 init 进程。这如列表 5-9 所示。

### 列表 5-9 内核 init 线程的创建

```c
static inline void __init_refok rest_init(void)
  __releases(kernel_lock)
{
  int pid;
  rcu_scheduler_starting();
  kernel_thread(kernel_init, NULL, CLONE_FS | CLONE_SIGHAND);
  numa_default_policy();
  pid = kernel_thread(kthread, NULL, CLONE_FS | CLONE_FILES);
  kthread_add_task = find_task_by_pid_ns(pid, &init_pid_ns);
  unlock_kernel();
  /*
   * 空闲线程必须执行 schedule();
   * 至少执行一次以让流程运行：
   */
  init_idle_bootstrap_task(current);
  preempt_enable_no_resched();
  schedule();
  preempt_disable();
  /* 在禁用抢占的情况下进入 cpu_idle */
  cpu_idle();
}
```
