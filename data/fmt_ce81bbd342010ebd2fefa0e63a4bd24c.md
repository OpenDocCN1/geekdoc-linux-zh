
```c
struct device_driver {
    const char *name;
    struct bus_type *bus;

    struct module *owner;
    const char *mod_name;

    bool suppress_bind_attrs;

    const struct of device_id *of_match_table;
    struct acpi_device_id *acpi_match_table;

    int (*probe) (struct device *dev);
    int (*remove) (struct device *dev);
    void (*shutdown) (struct device *dev);
    int (*suspend) (struct device *dev, pm_message_t state);
    int (*resume) (struct device *dev);
    const struct attribute_group **groups;
};
```

`bus` 成员指向设备驱动程序所注册的 `bus_type` 的指针。

`probe` 成员是一个回调函数，为每个检测到的且被驱动程序支持的设备调用。驱动程序应该为每个设备实例化自己并初始化设备。

`remove` 成员是一个回调函数，用于从设备上解绑驱动程序。这发生在设备被物理移除、驱动程序被卸载或系统关机时。

## 设备树引言

什么是设备树 (Device Tree, DT)？

- 1. DT 是一种用于描述硬件的数据结构，而不是将设备的每个细节都硬编码到操作系统中。
- 2. 该数据结构本身是一个由命名的节点和属性组成的简单树：
  - 节点包含属性和子节点。
  - 属性是简单的键值对，包含零个或多个提供节点信息的数据值。

它提供了哪些优势？

- 平台设备是由内核通过解析设备树节点在运行时创建的。
- 设备节点可以携带设备的配置数据。
- 允许内核代码与特定开发板的配置数据解耦（这是实现 ARM® 平台单内核二进制镜像的一步）。

![](imgimg/739a35b59067f8a55eff80a58765146f_98_0.png)

# Linux 设备与驱动模型

设备树可以为内核提供以下硬件配置：CPUs、内存、总线、外设连接、中断控制器、GPIO 控制器、时钟控制器等。

有三个主要的设备树组件将进行更详细的解释：

- 1. 设备树源 `DTS`
- 2. 设备树二进制 `DTB`
- 3. 设备树编译器 `DTC`

![](img/739a35b59067f8a55eff80a58765146f_99_0.png)

一个 SoC 可能有多个机器，或者对应于许多产品和开发板。设备树文件不是单一的，它们可以拆分成多个文件，并相互包含：

- `dts` 文件是板级定义。.dts 后缀表示设备树源码。
- `dtsi` 文件被 `.dts` 文件包含，通常包含 SoC 级定义。

按照约定，`.dtsi` 是包含文件，包含了 SoC 级信息的定义，而 `.dts` 文件是包含板级信息的最终设备树。.dtsi 后缀表示设备树源码包含文件。

在接下来的图中，你可以看到对于 iMX6 SABRE 开发板，设备树是如何被拆分成几个文件的：

![](img/739a35b59067f8a55eff80a58765146f_100_0.png)

© 2016 NXP B.V.

## 设备树源 (DTS)

DTS 是设备树的文本表示。它包含了用于硬件描述的数据结构，并由 `dtc` 编译成二进制设备树，然后由内核解释。

设备树在 Power.org 的《嵌入式电源架构平台需求》(ePAPER) 中有详细描述：https://www.power.org/documentation/epapr-version-1-1/

ePAPER 定义了一个名为“设备树”的概念，用于描述系统硬件并将该描述与内核镜像分离。设备树是一种树形结构，其节点描述了系统中系统中无法通过软件动态检测的物理设备。节点按层级的父子关系进行组织。节点以属性和值标记的集合的形式按层次结构进行组织。子节点定义了层次结构内设备之间的关系（例如，i2c 设备是 i2c 控制节点的子节点）。设备树从根节点 `/` 开始，该节点将用于匹配 `machine_desc` 条目。这种匹配将在第 7 章的根节点章节“I.MX6 Kernel Booting and I/O Physical to Virtual Static Memory Mapping”中描述。一个节点：

- 具有属性/值对，描述所代表设备的特征。
- 恰好有一个 (1) 父节点。
- 根节点没有父节点。

### 0 / 根节点

```
|---O child node
| |
|   O--- child node
| |
|O----O child node
```

节点名称是用于标识节点的名称。单元地址是用于标识节点的基地址。

```
node_name@unit_address {
  reg = <0x80000000 0x1000>;
}
``` 描述内存布局。

```
aliases {
  serial0 = &uart1;
  ethernet = &eth0;
}
``` 描述设备配置。

```
uart1 {
  clocks = <&ccm clk_uart1>;
  reg = <0x02158000 0x400>;
}
``` 内存。

```
memory {
  reg = <0x80000000 0x40000000>;
};
``` 传递参数给内核。

```
chosen {
  bootargs = "console=ttyS1,115200 root=/dev/mmc0p2";
};
``` 标识硬件。

```
compatible = "nxp,imx6q";
``` 

## 设备树二进制 (DTB) 与设备树编译器 (DTC)

设备树编译器 `DTC` 是用于将源码编译为二进制的工具。`DTC` 的源码位于 `/Linux/scripts/dtc`。

设备树编译器的输出是设备树二进制 `DTB`，由加载程序加载并内核解析。构建时生成的设备树列在 `/Linux/arch/arm/boot/dts/Makefile` 中，但也可以随时通过 `DTC` 手动编译。

设备树数据循环如下：

- 1. `dtc` 从 `.dt` 创建 `.dtb` `(.dtb` 可以附加到 `zimage)`。
- 2. 加载程序将 `.dtb` 拷贝到内存中。加载程序在传递内核之前可以对 blob 进行一些修改——主要是添加运行时学习的信息。参见相关函数 `ft_board_setup()`。
- 3. Linux 内核读取 FDT，创建扩展 DT，扩展 DT 可以被 Linux 修改。

## 在运行的 U-Boot 中解析设备树

如果 U-Boot 支持设备树，则它需要在 `u-boot/include/configs/mx6sabre_common.h` 中定义 `CONFIG_OF_LIBDT`。

如果 U-Boot 不设备树，你需要在编译内核时启用以下选项：

- `CONFIG_ARM_APPENDENDED_DTB`
- `CONFIG_ARM_ATAG_DTB_COMPAT`

使用 `CONFIG_ARM_APPENDENDED_DTB` 选项，启动代码将查找附加到 `zimage` 上的设备树二进制（例如 `cat zimage imx6q-sabresd.dtb > zimage-dtb`）。使用 `CONFIG_ARM_ATAG_DTB_COMPAT` 选项，`zimage` 可以从 ATAG 提取信息并在运行时存储在附加的 `DTB` 中。

当前 NXP 平台上的 U-Boot 有多个查看和操作 FDT 本身的命令：

- 1. `bootm` 有与 FDT 相关的子命令：
  - `bootm fdt`: 重新定位扁平设备树。
  - `bootm go`: 执行修复操作并启动操作系统。

## 2. fdt 纵 FDT

- `fdt addr <addr> <length>`: 将 FDT 位置设置为 `<addr>`。
- `fdt boardsetup`: 执行特定板卡的设置。
- `fdt move <fd> <newaddr>`: 将 FDT 拷贝到 `<addr>`。
- `fdt resize`: 将 FDT 调整为大小 + 填充对齐到 4K 地址边界。
- `fdt print <path> <prop>`: 从 `<path>` 开始递归打印。
- `fdt set <path> <prop> <val>`: 将 `<property>` 设置为 `<val>`。
- `fdt mknode <path> <node>`: 在 `<path>` 之后创建一个节点。
- `fdt rm <path> <prop>`: 删除节点或 `<property>`。
- `fdt header`: 显示信息。
- `fdt chosen <start> <end>`: 在树中添加/更新 `/chosen` 分支。

## 在运行的 Linux 内核上解析设备树
