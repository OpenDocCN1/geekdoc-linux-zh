

## PCMCIA 核心

Card Services（卡服务）是 PCMCIA 核心的主要组成部分。它向客户端驱动程序和主机控制器驱动程序提供一组服务。它包含一个名为 `pccardd` 的内核线程，用于轮询套接字相关的事件。当主机控制器报告诸如卡片插入和卡片移除等事件时，Pccardd 会通知 Driver Services（驱动服务）事件处理程序（将在下一节中讨论）。

PCMCIA 核心的另一个组件是一个库，用于操纵 *卡片信息结构*（CIS），这是 PCMCIA 卡的一部分。PCMCIA/CF 卡有两个内存空间：*属性内存*（Attribute memory）和 *公共内存*（Common memory）。属性内存包含 CIS 和卡片配置寄存器。例如，PCMCIA IDE 磁盘的属性内存包含其 CIS 和指定扇区数与柱面号的寄存器。在此情况下，公共内存包含存储磁盘数据的内存阵列。PCMCIA 核心向客户端驱动程序提供 CIS 操纵例程，如 `pccard_get_first_tuple()`、`pccard_get_next_tuple()` 和 `pccard_parse_tuple()`。清单 9.2 使用了其中一些函数的辅助。

PCMCIA 核心通过 sysfs 和 udev 将 CIS 信息传递给用户空间。诸如 `pccardctl` 之类的实用程序（属于 pcmciautils 包的一部分）依赖 sysfs 和 udev 来运行。当内核中缺少这些设施时，这简化了早期依赖自定义基础设施的设计方法。

### 驱动服务

Driver Services（驱动服务）提供了一种基础设施，提供以下内容：

- 一个捕获由 pccard 内核线程分发的事件警报的处理程序。该处理程序扫描并验证卡片的 CIS 空间，并触发加载适当的客户端驱动程序。
- 一个负责与内核总线核心通信的层。为此，Driver Services 实现了 `pcmcia_bus_type` 和相关总线操作。
- 客户端驱动程序使用来与 PCMCIA 核心注册自己的服务例程，如 `pcmcia_register_driver()`。清单 9.1 中的示例驱动程序使用了其中一些例程。

### 客户端驱动程序

客户端设备驱动程序（**图 9.3** 中的 XX_cs）查看卡片的 CIS 空间，并根据其收集的信息配置卡片。

### 数据结构

在继续开发一个示例 PCMCIA 客户端驱动程序之前，让我们先了解一些相关的数据结构：

1. PCMCIA 设备由在 `include/linux/mod_device.table.h` 中定义的 `pcmcia_device_id` 结构标识：

```c
struct pcmcia_device_id {
    /* ... */
    __u16     manf_id;    /* Manufacturer ID */
    __u16     card_id;    /* Card ID */
    __u8      func_id;    /* Function ID */
    /* ... */
};
```

`manf_id`、`card_id` 和 `func_id` 分别保存卡片的制造商 ID、卡片 ID 和功能 ID。PCMCIA 核心提供了一个名为 `PCMCIA_DEVICE_MANF_CARD()` 的宏，它使用提供的制造商和卡片 ID 创建一个 `pcmcia_device_id` 结构。另一个内核宏 `MODULE_DEVICE_TABLE()` 标记模块镜像中支持的 `pcmcia_device_ids`，以便在插入卡片时，PCMCIA 子系统从卡片的 CIS 空间提取匹配的制造商/卡片/功能 ID，从而可以按需加载模块。我们在第 4 章“奠定地基”中的“模块自动加载”部分探讨了这种机制。此过程类似于用于支持热插拔的两个其他流行 I/O 总线的设备驱动程序所使用的方法：PCI 和 USB。**表 9.1** 简要介绍了这三种总线技术驱动程序之间的相似之处。如果难以消化这一点请不要担心；我们将在后续章节中详细讨论 PCI 和 USB。

| | **PCMCIA** | **PCI** | **USB** |
|---|---|---|---|
| **表 9.1 PCMCIA、PCI 和 USB 的设备 ID 和热插拔方法** | | | |
| 设备 ID 表结构 | `pcmcia_device_id` | `pci_device_id` | `usb_device_id` |
| 创建设备 ID 的宏 | `PCMCIA_DEVICE_MANF_CARD()` | `PCI_DEVICE()` | `USB_DEVICE()` |
| 设备表示 | `struct pcmcia_device` | `struct pci_dev` | `struct usb_device` |
| 驱动程序表示 | `struct pcmcia_driver` | `struct pci_driver` | `struct usb_driver` |
| 热插拔方法 | `probe()` 和 `remove()` | `probe()` 和 `remove()` | `probe()` 和 `disconnect()` |
| 热插拔事件检测 | `pcicard kthread` | `PCI-family-dependent` | `khubd kthread` |

2. PCMCIA 客户端驱动程序需要将其 `pcmcia_device_id` 表与其 `probe()` 和 `remove()` 方法关联起来。这种关联通过 `pcmcia_driver` 结构实现：

```c
struct pcmcia_driver {
int (*probe)(struct pcmcia_device *dev); /* Probe method */
void (*remove)(struct pcmcia_device *dev); /* Remove method */
/* ... */
struct pcmcia_device_id *id_table; /* Device ID table */
/* ... */
};
```

3. `struct pcmcia_device` 内部表示一个 PCMCIA 设备，并在 `drivers/pcmcia/ds.h` 中定义如下：

```c
struct pcmcia_device {
/* ... */
io_req_t io; /* I/O attributes */
irq_req_t irq; /* IRQ settings */
config_req_t conf; /* Configuration */
/* ... */
struct device dev; /* Connection to device model */
/* ... */
};
```

4. CIS 操纵例程使用在 `include/pcmcia/cis.h` 中定义的 `tuple_t` 结构来保存 CIS 信息单元。例如，`CISPL_LINK_MFC` tuple 类型包含与多功能卡相关的信息。有关 tuple 的完整列表及其描述，请查看 `include/pcmcia/cis.h` 和 http://pcmcia-cs.sourceforge.net/ftp/doc/PCMCIA-PROG.html。

```c
typedef struct tuple_t {
/* ... */
cisdata_t TupleCode; /* See include/pcmcia/cis.h */
/* ... */
cisdata_t DesiredTuple; /* Identity of the desired tuple */
/* ... */
cisdata_t *TupleData; /* Buffer space */
};
```

5. CIS 包含卡片支持的每种配置的配置文件项。`cispl_cftable_entry_t` 定义在 `include/pcmcia/cis.h` 中，保存这样一个条目：

```c
typedef struct cispl_cftable_entry_t {
/* ... */
cispl_power_t vcc, vppi, vpp2; /* Voltage level */
cispl_io_t io; /* I/O attributes */
cispl_irq_t irq; /* IRQ settings */
cispl_mem_t mem; /* Memory window */
/* ... */
};
```

6. `cisparsed_t`，同样定义在 `include/pcmcia/cistpl.h` 中，保存由 PCMCIA 核心解析的 tuple：

```c
typedef union cisparsed_t {
    /* ... */
    cistpl_mandid_t manfid;        /* Manf ID */
    /* ... */
    cistpl_cftable_entry_t cftable_entry;  /* Configuration table entry */
    /* ... */
} cisparsed_t;
```

## 设备示例：PCMCIA 卡

让我们开发一个骨架客户端设备驱动程序（因为过多的细节会使讨论变得冗长），以了解 PCMCIA 子系统的工作原理。实现是通用的，因此无论你的卡片实现的是网络、存储还是其他技术，你都可以将其用作模板。只实现了 `XX_cs` 驱动程序；假设通用的 `XX` 驱动程序是现成的。

如前所述，PCMCIA 驱动程序包含 `probe()` 和 `remove()` 方法以支持热插拔。清单 9.1 将驱动程序的 `probe()` 方法、`remove()` 方法和 `pcmcia_device` 表注册到 PCMCIA 核心。当关联的 PCMCIA 卡插入时，调用 `XX_probe()`；当卡片弹出时，调用 `XX_remove()`。

### 清单 9.1 注册客户端驱动程序

```c
#include <pcmcia/ds.h> /* Definition of struct pcmcia_device */

static struct pcmcia_driver XX_cs_driver = {
    .owner          = THIS_MODULE,
    .drv            = {
        .name       = "XX_cs",    /* Name */
    },
    .probe          = XX_probe,   /* Probe */
    .remove         = XX_remove,  /* Release */
    .id_table       = XX_ids,     /* ID table */
    .suspend        = XX_suspend, /* Power management */
    .resume         = XX_resume,  /* Power management */
};

#define XX_MANUFACTURER_ID  0xABCD   /* Device's manf_id */
#define XX_CARD_ID          0xCDEF   /* Device's card_id */

/* Identity of supported cards */
static struct pcmcia_device_id XX_ids[] = {
    PCMCIA_DEVICE_MANF_CARD(XX_MANUFACTURER_ID, XX_CARD_ID),
    PCMCIA_DEVICE_NULL,
};

MODULE_DEVICE_TABLE(pcmcia, XX_ids); /* For module autoload */

/* Initialization */
static int __init
init_XX_cs(void)
{
    return pcmcia_register_driver(&XX_cs_driver);
}
```

