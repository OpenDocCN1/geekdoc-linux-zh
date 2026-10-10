
```
Filename '8548/dtb'.
Load address: 0xc00000
Loading: ##
done
Bytes transferred = 16384 (4000 hex)
=> bootm loaddaddr = $fdtaddr
## Booting kernel from Legacy Image at 00600000 ...
Image Name: Montavista Linux 6/2.66/freesc
Image Type: PowerPC Linux Kernel Image (gzip compressed)
Data Size: 1838489 Bytes = 1.8 MB
Load Address: 0000000
Entry Point: 0000000
Verifying Checksum ... OK
## Flattened Device Tree blob at 0xc00000
Booting using fdt blob at 0xc00000
Uncompressing Kernel Image ... OK
Loading Device Tree to 0xff7f000, OK
<... Linux begins here...>
and away!
```

区别在于我们加载了两个镜像。较大的镜像（1.8MB）是内核。较小的镜像（16KB）是扁平设备树。注意我们将内核和 DTB 分别放在 `0x600000` 和 `0xc0000`。当我们使用 `bootm` 命令启动内核时，添加了第三个参数，它告诉 U-Boot DTB 在哪里。

现在你可能在想它来自哪里。简单的答案是它是作为开发者提供的一部分提供的。如果你查看内核树，将看到它所在的地方。困难的答案是，你必须深入硬件细节并熟练编写设备节点及其相应的属性。希望这部分将带你入门。

### 7.5.1 设备树源

设备树节点由特殊的编译器编译成二进制格式，供 U-Boot 和 Linux 使用。可以在网上找到它。列表 7-14 显示了设备树源码。

```dts
/*
* MPC8548 Device Tree Source
* Copyright 2006, 2008 Freescale Inc.
* This program is free software; you can redistribute it or modify it
* under the terms of the GNU Public License as published by
* Software Foundation; either version 2 of the License, or
* any later version).
*/
```

```dts
/dts-v1;
/{
  model = "MPC8548CDS";
  compatible = "MPC548CDS", "MPC85xx";
  #address-cells = <1>;
  #size-cells = <1>;
  aliases {
    ethernet0 = &ethernet0;
    ethernet1 = &ethernet1;
    ethernet2 = &ethernet2;
    ethernet3 = &ethernet3;
    serial0 = &serial0;
    serial1 = &serial1;
    pci0 = &pci0;
    pci1 = &pci1;
    pci2 = &pci2;
    uart0 = &uart0;
  }
cpus {
  #address-cells = <1>;
  #size-cells = <0>;
  PowerPC,85480 {
    device_type = "cpu";
    reg = <0x0>
    d-cache-size = <32>; // 32 bytes
    i-cache-size = <32>; // 32 bytes
    d-cache-size = <0x8000>; // L1, 32K
    i-cache-size = <0x8000>; // L1, 32K
    timebase-frequency = <0>; // 33 MHz, from uboot
    bus-frequency = <0>; // 166 MHz
    clock-frequency = <0>; // 825 MHz, from uboot
    next-level-cache = <L2>;
  };
}
memory {
  device_type = "memory";
  reg = <0x0 0x80000000>; // 128M at 0x
};
localbus@0e000000 {
  #address-cells = <2>;
  #size-cells = <1>;
  compatible = "simple-bus";
  reg = <0xe000000 0x0500000>;
  interrupt-parent = &ic;
};
ranges = <0x0 0x0 0xff000000 0x01000000>; // *16MB Flash*/
flash@0,0 {
  #address-cells = <1>;
  #size-cells = <1>;
  compatible = "cfi-flash";
  bank-width = <2>;
  device-partition@0x0 {
    label = "free space";
    reg = <0x00000000 0x00f80000>;
  };
};
```

# 列表 7-14 续

```dts
partition@0x10000 {
    label = "bootloader";
    reg = <0x00f80000 0x08000>;
    read-only;
};
<...此处省略...>
```

这是一个很长的列表，但研究它是非常值得的。尽管这看起来显而易见，但值得注意的是，此设备树源码是针对 Freescale MPC8548CDS 的。作为自定义 Linux 开发人员，你的工作部分是将此 DTS 采用到你自己的基于 MPC8548 的系统中。

列表 7-14 显示的部分数据是自言自明的。扁平设备树由设备节点组成。节点是设备树中的条目，通常描述单个设备或总线。每个节点包含一组描述它的属性，实际上这是一个树结构。它可以很容易地用熟悉的树的形式表示，如列表 7-15 所示。

# 列表 7-15 DTS 的树视图

```
|/ Model = "MPC8548CDS", etc.
|--- cpus: #address-cells = <1>, etc.
|   |
|   |--- PowerPC,PC85480, etc.
|--- Memory: device_type = "memory", etc.
|--- localbus@00000000: #address-cells = <2>, etc.
|   |
|   |--- flash@0,0: #address-cells = <1>, etc.
|...>
```

32 字节，且这些缓存的大小均为 32KB (`0x8000` 字节)。我们看到几个显示时钟频率的属性，例如 `timebase-frequency` 和 `clock-frequency`，它们表明这些是由 U-Boot 设置的。这很自然，因为 U-Boot 配置了硬件时钟。

名为 `address-cells` 和 `size-cells` 的属性非常值得解释。在此语文中，“单元”（cell）是一个简单的 32 位数值。`address-cells` 和 `size-cells` 仅表示在子节点中指定地址（或大小）所需的单元（32 位字段）数量。

内存设备节点并没有奥秘。从该节点可以明显看出，平台包含一个从地址 0 开始的单体内存库，大小为 128MB。

关于平坦设备树（flat device tree）语法的完整细节，请参阅本章末尾的结果。最有用的之一是 Power.org 生成的文档，位于 `www.power.org/resources/downloads/Power_ePAPR_APPROVED_v1.0.pdf`。

### 7.5.2 设备树编译器

早期引入的设备树编译器（`dtc`）将人类可读的设备树源码转换为 U-Boot 和 Linux 内核都能理解的机器可读二进制文件。虽然 `kernel.org` 上托管了 `dtc` 的 git tree，但设备树源码已合并到内核源码中，并使用 `.../powerpc` 分支的任何 Power 架构内核进行构建。

使用设备树编译器非常简单。一个转换为二进制文件的典型命令如下：

```
$ dtc -O dt -o myboard.dt -b 0 myboard.dt
```
