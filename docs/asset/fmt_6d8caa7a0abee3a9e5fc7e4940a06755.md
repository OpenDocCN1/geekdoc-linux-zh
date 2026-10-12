
- 标签（`label`）被添加到中断控制器节点，用于在根节点中分配一个句柄；然而，所有节点都可以显式配置。
- 每个设备都有一个中断。
- 此示例显示了常用模式：使用第一个单元编码中断控制器，使用第二个单元编码高电平。具体信息请参考绑定（`binding`）。

在设备树源（`DTS`）语法中，使用多个属性描述中断：

- `interrupts` 属性用于指定设备的中断（号）和类型。

```
node {
    compatible = "vendor,device";
    interrupts = <4 2>;
}
```

![](img/bc86631e65e541c1c58ec0ab72a978e0_328_2.png)

## 第 12 章 嵌入式 Linux 简介

在此示例中，`interrupts` 指定设备使用中断号 `4`，类型为 `2`（可能对应上升沿、下降沿等）。

- `interrupt-parent`：`interrupt-parent` 属性用于指定作为设备父控制器的节点。

```
node {
  compatible = "vendor,device";
  interrupts = <4 2>;
  interrupt-parent = <&intc>;
}
```

```
intc {
  compatible = "vendor,intc";
}
```

在此示例中，`interrupt-parent` 属性指定 `intc` 节点作为中断控制器。

- `interrupt-cells`：`#interrupt-cells` 属性用于指定 `interrupts` 属性中每个中断指定符的单元数量。每个单元编码中断信息（例如中断号、极性等）。

```
node {
  compatible = "vendor,device";
  interrupts = <4 2>;
  #interrupt-cells = <2>;
}
```

在此示例中，`#interrupt-cells` 指定 `interrupts` 中的每个中断指定符包含两个单元（对应中断号和类型）。

- `interrupt-controller`：`interrupt-controller` 属性用于指定一个节点作为其子节点的中断控制器。

```
intc {
  compatible = "vendor,intc";
  interrupt-controller;
  #interrupt-cells = <2>;
}
```

在此示例中，`interrupt-controller` 属性指定 `intc` 节点作为其子节点的中断控制器。

![](img/bc86631e65e541c1c58ec0ab72a978e0_329_0.png)

## 第 13 章 嵌入式 Linux 简介

总体而言，`DTS` 语法中的这些中断相关属性提供了一种灵活且丰富的方式来描述系统的中断配置，包括中断号、类型、控制器和编码。

## 设备树包含

在设备树源（`DTS`）语法中，在一个 `DTS` 文件中包含另一个 `DTS` 文件是常见的，通常用于描述在多个系统中板卡或模块。这是通过 `include` 语句实现的，该语句将包含的 `DTS` 文件路径作为参数。

- 可以拆分为多个文件，并相互包含
- `dtsi` 文件是包含文件，`.dts` 文件是最终的设备树
- 通常它们将包含 `SoC` 层信息的定义
- 使用 `DTS` 操作 `/include/` 或者在某些内核版本中，`DTS` 会通过 C 预处理器，因此建议使用 `#include-sabresd.dts`。

![](img/bc86631e65e541c1c58ec0ab72a978e0_330_0.png)

## ev93-sabresd.dts 示例

例如，假设有一个用于特定 `CPU` 和一组设备的板卡的 `DTS` 文件：

```
/dts-v1;

/ {
  model = "MyBoard";
  compatible = "vendor,board";

  cpu {
    compatible = "arm,cortex-a9"
  }

  ethernet {
    compatible = "vendor,ethernet"
    ...
  }

};
```

我们将此 `DTS` 文件包含另一个描述使用该板系统的 `DTS` 文件中：

```
/dts-v1;

/ {
  model = "MySystem";
  compatible = "vendor,system"
}
```

```
chosen {
  bootargs = "console=ttyS0,115200 root=/dev/mmcblk1p2 rw";
}
```

```
memory {
  device_type = "memory";
  reg = <0x0 0x40000000>;
}
```

```
myboard {
  compatible = "vendor,board";
  model = "MyBoard"
  status = "okay"
};
```

在此示例中，`myboard` 节点通过 `include` 语句包含了该板卡的 `DTS` 文件：

```
myboard {
  compatible = "vendor,board"
  model = "MyBoard"
  status = "okay"
  include "myboard.dtsi"
};
```

`include` 语句导致 `myboard.dtsi` 文件的内容包含在 `myboard` 节点中。

通过使用 `DTS` 包含，我们可以创建一个模块化且可重用的系统描述，以适应不同的硬件配置和用例。

# 13. 嵌入式 Linux 简介

![](img/bc86631e65e541c1c58ec0ab72a978e0_332_0.png)

# Linux 启动序列

- 引导加载（`Boot loader`）：
  - 通常此阶段执行硬件初始化和测试，加载内核镜像，并将控制权交给 `Linux` 内核。
- 内核初始化阶段：
  - 此阶段执行特定平台的初始化，启动内核子系统，开启多任务处理，挂载根文件系统，并跳转到用户空间。
- 用户空间初始化阶段：
  - 通常此阶段启动服务，进行网络初始化，然后输出日志提示符（`log-prompt`）。

## 引导加载阶段

- 硬件初始化：这通常包括：
  - 配置 `CPU` 速度
  - 内存初始化，例如设置寄存器、清理内存以及确定板内存的大小
  - 开启缓存（`caches`）
  - 设置用于启动控制台的串口

# 第 15 章 嵌入式 Linux 简介

- 一旦成功完成上述步骤，下一步是加载 `Linux` 内核。
- 下载内核镜像和内存磁盘
  - 引导加载程序需要找到内核镜像，该镜像可能位于系统闪存或网络上。
  - 如果镜像是压缩的（通常如此），则需要对镜像进行解压。
  - 此外，如果存在初始内存磁盘（`initial ram disk`），引导加载程序需要将其镜像加载到内存中
- 设置参数
  - 参数传递是 `Linux` 内核支持的一个非常强大的选项。`Linux` 提供了一种跨平台向内核传递参数的通用方法。
  - 使用以下字符串设置内核参数：
    - `setenv bootargs 'console=ttyS0,115200n8 root=/dev/mmblk0p2 roottype=ext2 rw'` 你可以看到：
      - `console` 内核设置 `115200n8` 和 `ttyS0`（如果是屏幕显示，则可能是 `ttyS2`）
      - 根文件系统路径为 `SD` `/dev/mmblk0p2`，文件类型 `ext2`（可以是 `ext3`），权限为读和写
- 跳转到内核入口点
  - 内核入口点在构建内核时由链接器脚本决定

## 内核启动

`Linux` 内核的启动过程大致可以分为以下几个阶段：

1. `CPU`/平台特定初始化：此阶段包括特定架构的初始化代码，用于设置 `CPU`、内存管理、中断处理以及其他低层硬件细节。
2. 子系统初始化：在此阶段，内核初始化各种子系统，如调度器、虚拟内存管理器、文件系统、网络和输入/输出（`I/O`）子系统。这涉及分配内存、初始化数据结构以及设置相关硬件。
3. 驱动程序初始化：子系统初始化完成后，内核会探测并初始化硬件组件的驱动程序。这涉及识别硬件、分配资源以及在相关子系统中注册驱动程序。
4. 挂载根文件系统：驱动程序初始化后，内核挂载根文件系统，该系统包含系统运行所需的文件和目录。
5. 移动到用户空间：最后，内核将控制权交给用户空间，通常会启动 `init` 进程，该进程负责启动用户空间守护进程和服务。

总的来说，`Linux` 内核的启动过程是一个复杂的多阶段过程，涉及硬件初始化、设置子系统以及加载驱动程序和文件系统，最后将控制权交给用户空间。

![](img/bc86631e65e541c1c58ec0ab72a978e0_333_0.png)

内核启动可以分为以下阶段：

- `CPU`/平台特定初始化
- 子系统初始化
- 驱动程序初始化
- 挂载根文件系统
- 移动到用户空间

![](img/bc86631e65e541c1c58ec0ab72a978e0_334_0.png)

## CPU/平台特定初始化
