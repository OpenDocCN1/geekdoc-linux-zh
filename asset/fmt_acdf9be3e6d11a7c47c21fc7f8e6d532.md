
当 `device_id` 条目中的 `compatible` 字段与 DT 设备节点的 `compatible` 属性匹配时，驱动的 `probe()` 函数被调用。`probe()` 函数负责初始化设备、从匹配的节点获取配置并将设备注册到适当的内核框架。

在你的 i2c 设备驱动中，你也定义了一个 `i2c_device_id` 结构体数组：

```c
static const struct i2c_device_id mma8451_id[] = {
    {"mma8450", 0 },
    {"mma8451", 1 },
};
MODULE_DEVICE_TABLE(i2c, mma8451_id);
```

`probe()` 函数的第二个参数是该数组中与连接设备元素：

```c
static int accel_probe(struct i2c_client *client, const struct i2c_device_id *id)
```

你可以使用 `id->driver_data`（每个设备唯一）设备特定数据。例如，对于“mma8451”设备，`driver_data` 为 1。

绑定基于 `i2c_device_id` 表或设备树兼容字符串发生。I2c内核首先通过兼容字符串（OF 样式，即设备树）匹配设备，如果失败，则尝试通过 id 匹配。

# Linux 设备与驱动模型

```c
&i2c1 {
    clock-frequency = <100000>;
    pinctrl-names = "default";
    pinctrl-0 = <&pinctrl_i2c1>;
    status = "okay";
    mma8451ic {
        compatible = "fsl,mma8451";
        reg = <0xc>
        position = <0>;
        vdd-supply = <&reg_sensor>;
        vddio-supply = <&reg_sensor>;
        interrupt-parent = <&gpio1>;
        interrupts = <18 8>;
        interrupt-route = <1>;
    };
}
```

i2c1 节点中的 `pinctrl-0` 属性指向 `pinctrl_i2c1` 节点，i.MX6 的 pads 在此处进行复用用：

```c
pinctrl_i2c1: i2c1grp {
    fsl,pins = <n        MX6QDL_PAD_CSI0_DAT8 I2C1_SDA 0x4001b8b1
        MX6QDL_PAD_CSI0_DAT9 I2C1_SCL 0x4001b8b1
    >;
};
```

# 第 3 章

## 最简单的驱动

Linux 嵌入式系统设计的一个核心概念是将用户应用程序与底层硬件分离。用户空间应用程序不允许直接访问外设寄存器、存储媒体甚至 RAM 内存。相反，硬件是通过内核驱动程序访问的，RAM 内存由内存管理单元（MMU）管理，应用程序在虚拟地址上进行操作。

这种分离提供了健壮性。如果假设 Linux 内核运行正常，那么只允许内核与底层硬件交互，可以防止应用程序无意或恶意地错误配置硬件外设，并将其置于未知状态。

这种分离提供了可移植性。如果只有内核驱动程序管理硬件特定代码，那么在将系统从一个硬件平台迁移到另一个平台时，只需要修改这些驱动程序。应用程序访问的是一组跨硬件平台一致的驱动 API，允许应用程序在很少或不修改源代码的情况下从一个平台移动到另一个平台。

设备驱动可以是内核模块，也可以静态编译到内核镜像中。默认内核构建会将大多数驱动程序静态编译到内核中，以便它们自动启动。内核模块并不一定是设备驱动程序；它是内核的扩展。内核模块被加载到内核的虚拟内存中。将设备驱动编译为模块可以使开发更容易，因为可以在不重启内核的情况下加载、测试和卸载。内核模块通常位于根文件系统的 `/lib/modules/<kernel_version>` 上。

每个 Linux 内核模块都有一个 `init()` 和 `exit()` 函数。在驱动程序加载时调用一次 `init` 函数，在驱动程序移除时调用 `exit` 函数。`init()` 函数让操作系统知道驱动程序的能力，以及在发生特定事件时应该调用它的函数（例如：将驱动程序注册到总线、注册字符设备等）。`exit()` 函数释放 `init` 函数请求的所有资源。

宏 `module_init()` 和 `module_exit()` 导出 `init` 和 `exit` 函数的符号，使得加载你的模块的内核代码可以识别这些入口点。

有一组宏用于识别模块的各种属性。这些字符串被封装到模块中，并可以被各种工具访问。最重要的模块描述宏是 `MODULE_LICENSE` 宏。如果此宏没有被设置为某种 GPL 许可标签，当你加载模块时，内核将变得“被污染”（tainted）。当内核被污染时，意味着它处于一个社区不支持的状态。大多数内核开发者会忽略涉及被污染内核的错误报告，社区成员可能会要求你在继续诊断与内核相关的问题之前纠正污染状态。此外，当内核被污染时，某些调试功能和 API 调用可能会禁用。

## 许可

Linux 内核根据 GNU 通用许可证第 2 版（GPL2）授权。该许可允许你自由使用、学习、修改和共享软件。但是，当你重新分发软件（无论是否修改）时，GPL 要求你以相同的许可和源代码重新分发。如果你对 Linux 内核进行了修改（例如为了适配你的硬件），则它是内核的衍生作品，因此必须根据 GPL2 发布。但是，你只需要在设备开始分发给客户时这样做，而不是面向整个世界。

书中提供的内核模块根据 GPL 许可发布。有关开源软件许可的更多信息，请访问 http://opensource.org/licenses。

# 实验 3.1："helloworld" 模块

## 用户空间

![](img/739a35b59067f8a55eff80a58765146f_114_0.png)

helloworld

## IO 空间

![](img/739a35b59067f8a55eff80a58765146f_114_1.png)

## 内核空间

在你的第一个内核模块中，每次加载和卸载模块时，只需向控制台发送一些信息。`hello_init()` 和 `hello_exit()` 包含了 `pr_info()` 函数。这与你在用户应用程序中使用 `printf` 的语法相似。

# 实验 3.2: "带参数的helloworld" 模块

![](img/739a35b59067f8a55eff80a58765146f_117_0.png)

许多 Linux 可载内核模块 (LKM) 都有可以在加载时、启动时以及有时在运行时设置的参数。在这个内核模块中，你将向命令行传递一个参数，该参数将在模块加载期间设置。你还可以通过 sysfs 文件系统读取这些参数。

sysfs 是 Linux 内核提供的一种种虚拟文件系统，它通过虚拟文件从内核设备模型向用户空间导出各种内核子系统、硬件设备和相关设备驱动程序的信息。除了提供各种设备和内核子系统的信息外，导出的虚拟文件还用于它们的配置。

模块参数的定义通过 `module_param()` 宏完成。

```c
module_param(name, type, perm); /* perm 参数指定 sysfs 中对应文件的权限。 */
```

现在将描述驱动程序的主要代码部分：

1. 在 `#include` 语句之后，如下所示声明一个新的整数变量 "`num`"：

```c
static int num = 5;
module_param(num, int, S_IRUGO); /* S_IRUGO 表示所有人都可以读取 sysfs 条目 */
```

2. 如下更改 `hello_init()` 函数中的 `pr_info` 语句：

```c
pr_info("parameter num = %d.\n", num);
```

3. 在 my_modules 项目中创建一个新的 "`helloworld_with_parameters.c`" 文件，并将 `helloworld_with_parameters.o` 添加到你的 `Makefile` 的 `obj-m` 变量中，然后使用 Eclipse 编译并部署模块。

```makefile
obj-m += helloworld_with_parameters.o
```

## 列表 3-3: helloworld_with_parameters
