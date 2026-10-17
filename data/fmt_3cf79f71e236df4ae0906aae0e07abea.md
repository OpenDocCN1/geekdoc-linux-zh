
- **`动态 LPAR (Dynamic LPAR, DLPAR)`**: 该术语表示分区接受特定的资源重新排列。运行`AIX`和`AIX-5`应用的分区可以在之间进行处理器和内存的动态移动。

- **`虚拟机管理程序 (Hypervisor)`**: 这是位于物理硬件和操作系统之间的底层控制机制。虚拟机管理程序通过分配和共享这些资源来拥有并创建分区。

划分机器不需要`AIX`，安装和运行`Linux`也不需要`AIX`。`AIX`为硬件分析、智能故障检测和错误日志提供了更丰富的功能。

欲了解更多信息，请访问`pSeries`网站：

```
http://www-l.ibm.com/servers/eserver/pseries/linux/
```

`AIX`和`Linux`可以同时在支持`LPAR`的`pSeries`服务器上的独立分区上任意组合运行（即在零或多个`AIX`分区上运行零或多个`Linux`分区）。这允许您将多个独立服务器的工作负载整合到单个系统上。

由于支持`LPAR`的`pSeries`划分由基于固件的虚拟机管理程序和硬件控制台(`HMC`)控制，因此运行`Linux`不需要`AIX`。

图`6-4`显示了一个典型的逻辑分区`pSeries`服务器。它展示了`HMC`连接到各个分区和虚拟机管理程序的主要组件。这包括`HMC`可以控制的内部组件：处理器、内存和`I/O`适配器。

![](img/6b2be6cf94c5583e73925c180246991a_186_0.png)

图`6-4``LPAR`上`pSeries`服务器的`Linux`

逻辑分区功能允许在分区与外部之间进行资源的重新排列，以及在两个分区之间移动资源，而无需重启操作系统。`pSeries`中新的动态`LPAR`功能可以动态移动`AIX`分区的资源。目前`Linux`不支持此。然而，`Linux`分区和动态`LPAR`可以在同一台服务器上运行。

欲了解有关支持`LPAR`的`pSeries`服务器的更多信息，请参阅：

```
http://www.ibm.com/servers/eserver/pseries/lpar/resources.html
```

在图`6-4`的示例中，任何`Linux`分区都可以是`AIX`分区。

## `6.15``Linux`及其`AIX`的关系

`Linux`有两种方式与`AIX`关联。可能同时存在这两种关系的系统环境。

- 在`AIX 5L`内部作为运行`Linux`应用的能力

- 基于`Linux`的`pSeries`前端系统与处理关键任务的基于`AIX`的`pSeries`服务器交互的能力

`Linux`已经为`AIX`提供了帮助，由于`AIX Toolbox for Linux Applications`的出现，`AIX 5L`获得了更多动力。通过允许`AIX Toolbox for Linux Applications`软件包让`Linux`应用能够轻松地为`AIX`编译，`IBM`正在扩大可用的产品组合。此外，`AIX`现在可以利用日益增长的`Linux`技能储备。

此外，`Linux`和`AIX`是互补的操作系统。`AIX`是`pSeries`战略性的、经过验证的、关键任务操作系统。`Linux`是一种高度可移植的操作系统，支持所有`IBM`平台。`IBM`期望看到许多运行`Linux`（在`xSeries`或`pSeries`硬件上）的实例作为运行`DB2`和其他企业应用的关键任务`AIX`系统的前端。

如你所见，`AIX`是`pSeries`服务器的战略性操作系统。它包含了诸如扩展性和远程访问安全(`RAS`)等企业功能，这些功能在`Linux`上需要多年时间才能实现。许多来自其他`IBM`操作系统的`AIX`能力和功能正在被添加到`Linux`中。`Linux`将成熟为完整的企业运行环境。

## `6.2` 用于 `pSeries` 硬件启用的 `Linux`

为`pSeries`提供了`32`位和`64`位版本的`Linux`，以优化客户选择并利用`pSeries`硬件能力。`RS/6000 B50`和`150`是`32`位`PowerPC`系统，受`Linux for pSeries 32`位内核和应用环境的支持。

`64`位的`POWER3`和`POWER4`系统具有`32`位或`64`位内核，并支持`32`位或`64`位应用环境（取决于型号和`Linux`发行版）。

### 用于 `pSeries` 硬件启用的 `Linux`

为`pSeries`提供了`32`位和`64`位版本的`Linux`，以优化客户选择并利用`pSeries`硬件能力。`RS/6000 B50`和`150`是`32`位`PowerPC`系统，受`Linux for pSeries 32`位内核和应用环境的支持。

`64`位的`POWER3`和`POWER4`系统具有`32`位或`64`位内核，并支持`32`位或`64`位应用环境（取决于型号和`Linux`发行版）。

为`pSeries`提供了`32`位和`64`位版本的`Linux`，以优化客户选择并利用`pSeries`硬件能力。`RS/6000 B50`和`150`是`32`位`PowerPC`系统，受`Linux for pSeries 32`位内核和应用环境的支持。

`64`位的`POWER3`和`POWER4`系统具有`32`位或`64`位内核，并支持`32`位或`64`位应用环境（取决于型号和`Linux`发行版）。

## `I/O` 设备和适配器

许多适配器和设备可以连接到`pSeries`。由于`Linux`的某些适配器和设备可以使用`AIX`的驱动，因此`Linux`无法直接使用。然而，`Linux`适配器和设备可以使用`pSeries`驱动。

欲获取`Linux pSeries`的更多信息，请查看：

```
http://www.ibm.com/servers/eserver/pseries/linux/
```

对于`Linux for pSeries`的扩展性的更多详细信息，请查看`Linux for pSeries`的扩展性和启用。

在`IBM`网站上查看`Linux for pSeries`的白皮书：

```
http://www.ibm.com/servers/eserver/pseries/linux/facts.pdf
```

> **重要**：任何`LDP`上的某些硬件设备可能未完全启用或认证。我们建议定期查看`Linux`硬件数据库：

```
http://support.suse.de/sdb/en/
```

`Linux for pSeries`启用以使用串口控制台：

```
http://www.ibm.com/servers/eserver/pseries
```

### `6.2.1``Linux for pSeries` 的扩展性

`Linux`内核`2.4`在对称多处理(`SMP`)系统上的扩展良好。这使得它能够很好地扩展到`RS/6000 170, 270, 610, 620, 630, 640, 650, 655, 660, 670`和`690`以及`1`到`8`路`LPAR``Linux for pSeries`还可以扩展到`64 GB`内存和`2 TB`文件系统。

欲了解`Linux for pSeries`的扩展性和启用详细信息，请参阅：

```
http://www.ibm.com/services/learning/conf/us/pseries
```

此外参阅关于`Linux for pSeries`的演示文稿：

```
://www.ibm.com/partnerworld/phome.nsf/vAssetsLookup/LunchLearnLinux2002_08_27.pdf
```

`Linux2002_08_27.pdf`

### `6.2.2``Linux pSeries` 的可靠性、可用性和维护性

`pSeries`的一个关键属性是其关键的可靠性、可用性和维护性(`RAS`)功能。`RAS`是一个不仅由`IBM`使用的概念。然而，其实现方式取决于您正在工作的平台和环境。欲了解有关`pSeries`的`RAS`的更多信息，请访问：

```
http://www.ibm.com/servers/eserver/pseries/hardware/whitepapers/p690_ras.html
```

`Linux for pSeries`正在快速开发`RAS`能力。然而，运行`AIX`时许多`RAS`功能得到了充分实现。

在运行`Linux`时支持以下`pSeries``RAS`功能：

- `Chipkill`和`ECC`内存

- 日志文件系统（`Linux`下可用多种）。不支持`AIX``JSF`。

- `PCI`扩展错误检测

- 冗余、热插拔电源和冷却

- 错误日志

- 服务处理器（部分）

- 启动时处理器和内存卸分配

目前`Linux`不支持的某些`pSeries``RAS`功能包括：

- 硬盘的热插拔（可以通过命令行程序完成）

- `PCI`和内存的热插拔

- 磁盘镜像

- 首次故障数据捕获

- 动态逻辑分区（支持静态`LPAR`）

- `PCI`扩展错误恢复

- 向服务焦点报告错误

- 错误日志分析

- 远程支持

- 高可用集群多处理(`HACMP`)：可能有替代的第三方和开源解决方案

### `6.2.3` 其他信息来源
