
表 10.2 解释了上述转储中显示的一些值。前两个字节包含供应商 ID，它标识了制造该卡的公司。PCI 供应商 ID 在全球范围内维护和分配。（请将你的浏览器指向 www.pcidatabase.com 以获取数据库。）你可以从上述输出中破译出，Intel、Texas Instruments 和 Xircom（现已被 Intel 收购）分别拥有 `0x8086`、`0x104C` 和 `0x115D` 的供应商 ID。接下来的两个字节特定于卡的功能，并构成其设备 ID。从上述输出来看，Xircom 卡的以太网功能拥有 `0x0003` 的设备 ID，而调制解调器对应 `0x0103` 的设备 ID。PCI 卡还额外拥有子供应商和子设备 ID（参见上述转储中偏移量 44 和 46 处的单词），以便进一步精确定位其身份。

### 表 10.2. PCI 配置空间语义

| 配置空间偏移量 | 语义 | Xircom 卡转储输出中的值 |
| :--- | :--- | :--- |
| 0 | 供应商 ID | 0x115D |
| 2 | 设备 ID | 0x0003 |
| 10 | 类代码 | 0x0200 |
| 16 到 39 | 基地址寄存器 0 (BAR 0) 到 BAR5 | 0x3001...0000 |
| 44 | 子供应商 ID | 0x115D |
| 46 | 子设备 ID | 0x1181 |

配置空间内第 10 个字节处是描述设备类的代码。PCI 桥的类代码以 `0x06` 开头，网络设备拥有以 `0x02` 开头的类代码，通信设备拥有以 `0x07` 开头的类代码。因此，在上面的例子中，CardBus 桥、以太网卡和串行调制解调器分别拥有 `0x0607`、`0x0200` 和 `0x0700` 的类代码。你可以在 `include/linux/pci_ids.h` 中找到类代码定义。

PCI 驱动程序将其支持的供应商 ID、设备 ID 和类代码注册到 PCI 子系统中。利用此数据库，PCI 子系统在从其配置空间获取其身份后，将插入的卡绑定到适当的设备驱动程序。我们将在后面实现一个示例驱动程序时看到这是如何完成的。

## 访问 PCI 区域

PCI 设备包含三个可寻址区域：配置空间、I/O 端口和设备内存。让我们学习如何从设备驱动程序中访问这些内存区域。

### 配置空间

内核提供了一组六个函数，供您的驱动程序用于操作 PCI 配置空间：

```c
pci_read_config_(byte|word|dword)(struct pci_dev *pdev,
    int offset, int *value);
and
pci_write_config_(byte|word|dword)(struct pci_dev *pdev,
    int offset, int value);
```

在参数列表中，`struct pci_dev` 是 PCI 设备结构体，`offset` 是您想要访问的配置空间中的字节位置。对于读取函数，`value` 是指向提供的数据缓冲区的指针；对于写入例程，它包含要写入的数据。

让我们来看一些示例：

- 若要解析分配给卡片功能的 IRQ 号，请使用以下代码：

```c
unsigned char irq;
pci_read_config_byte(pdev, PCI_INTERRUPT_LINE, &irq);
```

根据 PCI 规范，PCI 配置空间中的偏移量 `60` 存储分配给该卡片的 IRQ 号。所有配置寄存器偏移量都在 `include/linux/pci_regs.h` 中通过描述性名称定义，因此使用 `PCI_INTERRUPT_LINE` 而不是 `60` 来指定此偏移量。类似地，要读取 PCI 状态寄存器（配置空间中偏移量 6 处的两个字节），请执行此操作：

```c
unsigned short status;
pci_read_config_word(pdev, PCI_STATUS, &status);
```

- 只有配置空间的前 64 个字节是标准化的。设备制造商为其余部分定义所需的语义。前面提到的 Xircom 卡片在偏移量 `64` 处分配了四个字节用于电源管理目的。为了禁用电源管理，Xircom CardBus 驱动程序 `drivers/net/tulip/xircmod_cb.c` 执行此操作：

```c
#define PCI_POWERMGT 0x40
pci_write_config_dword(pdev, PCI_POWERMGT, 0x0000);
```

## I/O 和内存

PCI 卡最多有六个 I/O 或内存区域。I/O 区域包含寄存器，而内存区域保存数据。例如，视频卡具有容纳控制寄存器的 I/O 空间和映射到帧缓冲区的内存区域。然而，并非所有卡都有可寻址的内存区域。I/O 和内存空间的语义取决于硬件，可以从设备数据手册中获取。

与配置内存一样，内核提供了一组辅助函数来操作 PCI 设备的 I/O 和内存区域：

```c
unsigned long pci_resource_{start|len|end|flags} (struct pci_dev *pdev, int bar);
```

要操作 I/O 区域，例如 PCI 视频卡上的设备控制寄存器，驱动程序需要执行以下操作：

1. 从配置空间中适当的基地址寄存器（bar）获取 I/O 基地址：
   ```c
   unsigned long io_base = pci_resource_start(pdev, bar);
   ```
   这假设该卡片的设备控制寄存器映射到与 `bar` 相关的内存区域，其值范围为 0 到 5，如表 10.2 所示。

2. 使用第 5 章“字符驱动程序”中讨论的内核 `request_region()` 监管机制标记此区域已被占用：
   ```c
   request_region(io_base, length, "my_driver");
   ```
   这里，`length` 是控制寄存器空间的大小，`my_driver` 标识该区域的所有者。在 `/proc/ioports` 中查找包含 `my_driver` 的条目即可定位此内存区域。

   您也可以使用在 `drivers/pci/pci.c` 中定义的包装函数 `pci_request_region()`。

3. 将数据手册中获取的寄存器偏移量加到第 1 步中获取的基地址上。使用第 5 章中讨论的 `inb()` 和 `outb()` 函数族操作此地址：
   ```c
   /* 读取 */
   register_data = inl(io_base + REGISTER_OFFSET);
   /* 使用 */
   /* ... */
   /* 写入 */
   outl(register_data, io_base + REGISTER_OFFSET);
   ```

要操作内存区域，例如上述 PCI 视频卡上的帧缓冲区，请遵循以下步骤：

1. 获取与内存区域相关的基地址、长度和标志：

   ```c
   unsigned long mmiobase = pci_resource_start(pdev, bar);
   unsigned long mmio_length = pci_resource_length(pdev, bar);
   unsigned long mmio_flags = pci_resource_flags(pdev, bar);
   ```

   这假设此内存映射到基地址寄存器 bar。

2. 使用内核的 `request_mem_region()` 监管机制标记此区域的所有权：

   ```c
   request_mem_region(mmiobase, mmio_length, "my_driver");
   ```

   您也可以使用之前提到的包装函数 `pci_request_region()`。

3. 获取对第 1 步中获得的设备内存的 CPU 访问权限。某些内存区域，例如保存寄存器的区域，需要防范副作用，因此被标记为 CPU 不可预取（或不可缓存）。其他区域，例如此示例中使用的区域，可以被缓存。根据访问标志，使用适当的函数获取映射区域对应的内核虚拟地址：

   ```c
   void __iomem *buffer;
   if (flags & IORESOURCE_CACHEABLE) {
       buffer = ioremap(mmiobase, mmio_length);
   } else {
       buffer = ioremap_nocache(mmiobase, mmio_length);
   }
   ```

   为了安全起见，并避免执行上述检查，请改用 `lib/iomap.c` 中定义的 `pci_iomap()` 服务：

   ```c
   buffer = pci_iomap(pdev, bar, mmio_length);
   ```
