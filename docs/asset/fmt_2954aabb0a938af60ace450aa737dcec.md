
```c
/*
* setup_machine_fdt - 当 dtb 传递给内核时进行的机器设置
* @dt: 指向 dt blob 的虚拟地址指针
* 如果向内核传递了 dtb，则使用它来选择正确的
* machine_desc 并设置系统。
*/
```

```c
const struct machine_desc *setup_machine_fdt(void *dt)
{
    struct machine_desc *mdesc;
    unsigned long dt_root;

    if (!early_init_dt_scan(dt))
        return NULL;

    mdesc = of_flat_dt_match_machine(NULL, arch_get_next_machine);
    if (!mdesc)
        machine_halt();

    dt_root = of_get_flat_dt_root();
    arc_set_early_base_baud(dt_root);

    return mdesc;
}
```

```c
bool __init_early_init_dt_scan(void *params)
{
    bool status;

    status = early_init_dt_verify(params);
    if (!status)
        return false;

    early_init_dt_scan_nodes();
    return true;
}
```

```c
void __init_init_dt_scan_nodes(void)
{
    int rc = 0;

    /* 从 /chosen 节点中检索各种信息 */
    rc = of_scan_flat_dt(early_init_dt_scan_chosen, boot_command_line);
    if (!rc)
        pr_warn("No chosen node found, continuing without\n");

    /* 初始化 {size,address}-cells 信息 */
    of_scan_flat_dt(early_init_dt_scan_root, NULL);
}
```

```c
/* 设置内存，调用 early_init_dt_add_memory_arch */
of_scan_flat_dt(early_init_dt_scan_memory, NULL);
}
```

3. **设备发布**：在板卡被识别且解析完早期配置数据后，内核初始化就可以按照正常方式进行。在此过程的某个点，会调用 `flatten_device_tree()` 将数据转换为更高效的运行时表示。这里也是特定特定的设置钩子被调用的地方，例如 ARM 设备上的 `init_early`、`init_irq()` 和 `init_machine()` 钩子。从名称可以推测出，`init_early()` 用于任何需要在启动过程早期执行的特定机器的设置，而 `init_irq()` 用于设置中断处理。

DT 上下文中最有趣的钩子是 `init_machine`，它主要负责为 Linux 设备模型填充有关平台的数据。可以通过解析 DT 并动态分配设备结构来获取设备列表。通过遍历位于 `drivers/of/platform.c` 中的 `of_platform_populate()` 函数的第二个参数，可以遍历设备树中的节点并根据这些节点创建平台设备。由于 `of_platform_populate()` 是一个 `device_id` 表，任何在该表中具有条目的节点也将将获得注册。

设备树被视为一种具有其自身语法和语义的语言。设备树数据结构是一个简单的节点树。树有一个没有名称并用斜杠（`/`）字符标记的根节点。每个节点可以包含任意数量的属性。

# 第 3 章

## 最简单的驱动程序

有一组宏用于用于标识模块的各种属性。这些字符串会被打包到模块中，并可以被各种工具访问。最重要的模块描述宏是 `MODULE_LICENSE`。如果此宏没有被设置为某种 GPL 许可，那么当你加载模块时，内核将变为“受污染的（tainted）”状态。当内核被污染时，意味着它处于一个社区不受支持的状态。大多数内核开发人员会忽略涉及受污染内核的错误报告，社区成员也可能要求你在继续诊断与内核相关的问题之前纠正污染状态。此外，当内核被污染时，某些调试功能和 API 调用可能会禁用。

## 许可协议

Linux 内核根据 GNU 公共通用许可证第 2 版（GPL v2）授权。该许可允许你自由地使用、研究、修改和共享软件。然而，当对软件进行分发时（无论是否经过了修改），GPL 要求你以相同的许可协议附带源代码重新分发该软件。如果对 Linux 内核进行了修改（例如为了适配你的硬件），它就是内核的派生版本，因此必须在 GPLv2 下发布。你只需要在设备开始分发给客户时执行此操作，而不需要面向全球发布。

本书提供的内核模块根据 GPL 许可协议发布。有关开源软件许可的更多信息，请参阅 `http://opensource.org/licenses`。

## 实验 3.1: "helloworld"

在你的第一个内核模块中，每当你加载和卸载模块时，简单地向树莓派控制台发送一些信息。`hello_init()` 和 `hello_exit()` 函数包含一个 `pr_info()` 函数。这与用户应用程序中使用的 `printf` 语法非常相似，但 `pr_info()` 用于在内核空间打印消息。如果你查看内核源码，你会看到类似如下的内容：

```
printk(KERN_ERR, "something wrong, return code: %d\n", ret);
```

其中 `KERN_ERR` 是内核源码树中 `include/linux/kern.h` 定义的八日志级别之一，用于指定错误消息的严重程度。`pr_*` 宏是各自 `printk` 调用的简写定义，在较新的驱动程序中使用它们。

在你的主机 PC 的家目录下，你创建一个 `linux_5.4_rpi3_drivers` 文件夹，你将在其中存储通过本书开发的所有驱动程序和应用程序。

```bash
~ mkdir linux_5.4_rpi3_drivers
```

使用你喜欢的文本编辑器创建 `helloworld_rpi3.c` 和 `Makefile` 文件，并将它们保存到 `linux_5.4_rpi3_drivers` 目录中。向这些文件中写入列表 3-1 代码和列表 3-2 代码。`Makefile` 中添加安全拷贝 (`SCP`)，以便通过以太网将模块从主机 PC 传输到树莓派文件系统：

```bash
scp *.ko root@10.0.0.10:
```

通过简单将新的 `<module>.o` 添加到 `Makefile` 变量 `obj-m` 中，可以在许多库复用同一个 Makefile。

编译 `helloworld_rpi3.c` 驱动程序并部署到树莓派：

```bash
~linux_5.4_rpi3_drivers$ make
~linux_5.4_rpi3_drivers$ make deploy
```

### 列表 3-1: helloworld_rpi3.c

```c
#include <linux/module.h>
static int __init hello_init(void)
{
    pr_info("Hello init\n");
    return 0;
}
static void __exit hello_exit(void)
{
    pr_info("Hello exit\n");
}
module_init(hello_init);
module_exit(hello_exit);

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Alberto Liberal <alberto@arroweurope.com>");

MODULE_DESCRIPTION("This is a print out Hello World module");
```

### 列表 3-2: Makefile

```makefile
obj-m := helloworld.o

KERNEL_DIR ? $(HOME)/linux_rpi3/linux

all:
  make -C $(KERNEL_DIR) \
    ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- \
    M=$(PWD) modules

clean:
  make -C $(KERNEL_DIR) \
    ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- \
    M=$(PWD) clean

deploy:
  scp *.ko root@10.0.0.10:/home/pi
```

## helloworld_rpi3.co 演示

加载模块：
