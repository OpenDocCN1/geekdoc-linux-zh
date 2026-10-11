
是什么决定了函数指针进入 `__initcall*_start` 数组？是由链接器完成的，它使用了来自 `module_init` 和 `*__initcall` 宏的提示。对于内置模块，这些宏将函数指针分配给特定的 ELF 段。

考虑一个内置模块（在 `.config` 中配置为 `"y"`），`module_init` 仅简单地展开如下（位于 `Linux/include/linux/init.h`）：

```c
#define module_init(x)    __initcall(x);
```

然后你遵循以下内容（位于 `Linux/include/linux/init.h`）：

```c
#define __initcall(fn)          device_initcall
#define device_initcall(fn)    device_initcall(fn, 6)
```

所以，现在 `module_init(my_func)` 意味着 `__define_initcall(my_func, 6)`。这是 `__define_initcall`：

```c
#define __initcall(fn, id) \
    static inline call_t __initcall##fn \
    attribute((__section(".initcall"##id))) = fn
```

这意味着到目前为止：

```c
static __initcall_my_func attribute((__section(".initcall6.init"))) = fn;
```

这意味着创建了一个符号 `__initcall_my_func`，它被放在名为 `.initcall6.init` 的 ELF 段中，通过将所有函数添加到此段创建了完整的函数指针数组 `.initcall6.init`。

查看 `do_initcall_level()` 中的后续代码：

级别 6 代表所有带有 `module_init(x)` 的内置模块。它从 `__initcall6_start` 开始，其值是 `.initcall6.init` 段中第一个函数的地址，并在 `__initcall7_start` 结束。

`do_one_initcall()` 将简单调用当前条目指向的函数。

`of_platform_populate()` 从 `customize_machine()`（位于 `Linux/arch/arm/kernel/setup.c`）被调用，而 `customize_machine()` 通过 `__initcall3_start` 条目被调用。

这是调用序列：

```
do_initcalls() -> do_one_initcall() -> customize_machine() -> imx6q_init_machine(void) -> of_platform_populate(customize_machine())
```

在 `Linux/arch/arm/kernel/setup.c` 中查找 `customize_machine()`：

```c
static int __init customize_machine(void)
{
    * 自定义平台设备或添加新的设备
     * 对于基于设备树的机器，从设备树填充机器，
     * 如果没有回调，否则我们需要一个 init_machine 回调。
     */
    if (machine_desc->init_machine)
        machine_desc->init_machine(); /* 调用 imx6q_init_machine(void) */
#ifdef CONFIG_OF
    of_platform_populate(NULL, default_bus_table, NULL);
#endif
    return 0;
}
```

在 `customize_machine()` 函数下方可以找到下一行代码：

```c
arch_initcall(customize_machine); /* #define_initcall(fn) __define_initcall(fn, 3) */
```

它向 `__initcall3_start` 添加了指向 `customize_machine()` 函数的函数指针。

通过 `of_platform_populate()` 创建平台设备后，驱动程序与设备之间的匹配（调用 `probe()` 函数）将从 `__initcall6_start` 条目完成，通过作为 `module_init(fn)` 参数的 `platform_driver_register()` 函数。

## 内存管理驱动

![](img/739a3b59067f8a55eff80a587614f_293_0.png)

查看 `machine_desc` 钩子的伪代码：

```
start_kernel()
    mdesc = setup_machine_fdt(atags_pointer)
    mdesc = of_flat_dt_match_machine()
    early_paging_init()
        mdesc->_init_meminfo()
    arm_memblock_init()
        mdesc->reserve()
    paging_init()
        devicemaps_init()
        mdesc->map_io()
    ...
    flatten_device_tree()
    if (mdesc->_init(smp_init))
        ...
        handle_arch_irq = mdesc->handle_irq
```

# 第 7 章

```
mdesc->init_early()
init_IRQ()
	machine_desc->init_irq()
outer_cache.write_sec = machine_desc->l2c_write_sec
time_init()
	machine_desc->init_time()
rest_init()
	kernel_thread(kernel_init, ...)
	kernel_init()
do_initcalls()
customize_machine()/* *initcall3_start */
machine_desc->init_machine()
__initcall6_start() / 平台驱动与平台绑定 /
init_machine_late()
machine_desc->init_late()
```

`rest_init()` 函数产生第一个内核，调用 `kernel_thread()` 函数并将 `kernel_init()` 函数作为第一个参数。此时，有两个线程在运行；`start_kernel()` 和 `kernel_init()`。最后，`kernel_init` 将挂载根文件系统并运行所有用户进程的父进程 init进程。

在调用 `start_kernel()` 之前，在内核初始化阶段，通过 `create_page_tables()`（位于 `Linux/arch/arm/kernel/head.S`）创建的初始页映射将允许内核启动的位置相关代码运行。这些映射稍后会被函数 `paging_init()`（位于 `Linux/arch/arm/mm/mmu.c`）覆盖（条目相同），该函数由 `setup_arch()`（位于 `Linux/arch/arm/kernel/setup.c`）调用，用于创建 L1 页表。

## 内存管理驱动

`imx6_pm_map_io_void` 调用 `iotable_init(imx6_pm_io_desc, ARRAY_SIZE(imx6-pm_io_desc))`，该函数通过 `create_mapping(struct map_desc *md)` 函数（位于 `Linux/arch/arm/mmu/mmu.c`）进行映射。`create_mapping()` 函数为 `"md"`指定的映射创建页目录项和任何必要的页表。

`iotable_init()` 在已知物理地址和虚拟地址之间创建静态映射。

`ioremap()` 在已知物理地址和分配的虚拟地址之间创建动态映射。

`iotable_init()` 的局限性是大小必须是页的倍数，而 `iotable()` 会映射任何大小的区域。以下是传递给 `create_mapping()` 函数的 `map_desc` 结构体数组（位于 `Linux/arch/arm/mach-imx/imx6`）：
