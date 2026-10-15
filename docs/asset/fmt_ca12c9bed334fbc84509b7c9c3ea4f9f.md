
> 如果你在接下来的实验中使用 `cat` 读取你的条目，你可能会发现意料之外的行为，即条目被调用了两次，即使你发送了文件结束的信号。 （你可以使用 `strace` 对所有 `proc` 条目进行验证这一点，这不是你模块中的错误。）这是由于 `cat` 的编写方式导致的，无需担心。

- 当写入第二个条目时，它接收到要交付的信号并发送它。
- 读取任何条目只需显示这些参数的当前值。

## 实验 2: 使用 proc 文件系统

编写一个模块，创建一个 `/proc` 条目并能够对其进行读写。

当从条目读取时，你应该获取某些参数的值。当向条目写入时，你应该修改它，这种修改应该反映在随后的读取中。

确保在卸载模块时删除了该条目。如果不这样做并在模块移除后尝试访问该条目，会发生什么？

解决方案展示了如何在 `/proc` 目录中创建条目。

## 实验 3: 创建你自己的子目录

编写一个模块，创建你自己的 `proc` 子目录以及其下的至少两个条目。作为第一个练习，读取条目应该获取一个值，写入它应该重置它。为多个条目使用相同的回调函数。

## 实验 4: 使用 seq file 用于 proc 文件系统

采用之前讨论的示例 `proc` 条目，并使用 `seqfile` 接口重新实现。作为一个参数，输入要打印的行数。

## 实验 4: 使用 /proc 发送信号

从内核向应用程序发送信号是有必要的。执行此操作的函数是：

```c
int send_sig(int signal, struct task_struct *task, int priv);
```

其中 `signal` 是要发送的信号，`task` 指向要信号的任务结构，`priv` 表示权限（用户应用程序为 0，内核为 1）。

编写一个模块在 `proc` 系统打开两个条目。

- 当写入第一个条目时，它设置了通过此机制注册接收信号的进程 `PID`。

# 第 15 章 统一设备模型与 sysfs

## 15.2 基础结构

设备模型的核心是对象 `objects`，它们包含了系统中任何对象的简单表示，如名称、类型、父节点、引用计数等。一组对象被包含在一个列表中。

包含在设备模型中的数据结构包含了每个设备的信息，用于描述它们的用途、位于何处、处于什么状态，以及如何挂起和恢复。它们还描绘了系统总线的结构、它们如何相互连接，以及可以附加和搜索哪些设备。

## 15.2 基础结构

对于每个设备，在 `/usr/src/linux/include/device.h` 中定义了一个通用结构：

```c
struct device {
      struct device *parent;
      struct device *dev;
      struct kset;
      struct object *kobj;
      const char name;
      struct device_type;
      struct *sem; /* 用于同步对其驱动程序的调用； */

      struct bus_type *bus; /* 设备所处的总线类型 */
      struct device_driver *driver;
      /* 哪个驱动程序已附加到设备 */
      void *data; /* 指向私有 struct platform_data 的指针；/*平台设备数据，没有计数 */
      int power;
      struct dev_pm_info *pm;
      struct kobj_node *node; /* 靠近 Udev节点 */
      int *devt;
      int mask; /* dma 掩码（如果是 dma 设备） */
      struct u64;
      struct core_dev *dma; /*类似 dma，但为所有内存节点提供了分配映射并为每个描述符分配了 64 位地址。 */

      struct device_data_parameters *dma_params;
      struct list_head;
      void *pools; /* * dma 池（如果是 dma 设备） */

      struct core_dev *mem; /* 用于核心设备覆盖内部 * */
```

```c
/* 架构特定的添加 */
struct dev_arch_archdata;
      struct dev *t;
      struct dev *dev; /* devt，创建 sysfs 中的 "dev" */
      spinlock_lock;
      devres_lock;
      struct list_head;
      struct klist_node;
      struct class;
      struct class *class;
      struct attribute_group **optional;
} (void)(struct device *dev);
```

在重要字段初始化后，设备通过以下函数在系统内核中注册和注销：

```c
int device_register(struct device *dev);
void device_unregister(struct device *dev);
```

设备的引用计数通过以下函数进行原子性递减：

```c
struct device *get_dev_type(struct device *dev);
void put_dev_type(struct device *dev);
```

指向 `device_type_driver` 的指针描述了设备的驱动程序：

```c
struct device_driver {
      const char *name;
      struct bus_type *bus;

      struct module *owner;
      struct char *modname; /* 用于内置模块 */
      int (*probe)(struct device *dev);
      int (*release)(struct device *dev);
      int (*remove)(struct device *dev, struct dev_pm_message, struct *test);
      struct device *dev;
      struct attribute_group *groups;
      struct dev_pm_ops *ops;
      struct void *priv;
};
```

驱动程序在相应的总线上进行注册/注销：

```c
int device_register(struct device *dev);
void device_unregister(struct device *dev);
```

并且引用计数通过以下函数增加：

```c
struct device *get_dev_type(struct device *dev);
void put_dev_type(struct device *dev);
```

接下来我们考虑这种通用基础设施如何连接到真实设备。

## 15.3 真实设备

实际设备直接与我们目前拥结构工作；它们被每种总线的内部代码使用。例如，PCI 设备有两个重要的结构：

```c
struct pci_dev {
    struct pci_driver *driver;
    struct device;
};
```

并且驱动程序注册到系统中：

```c
#include <linux/pci.h>
int pci_register(struct pci_dev *dev);
void pci_unregister(struct pci_dev *dev);
```

这是如何与通用基础设施连接的？因为设备结构被嵌入在 `pci_dev` 结构中，而通用设备结构被嵌入在 `pci_driver` 结构中，我们只需要指针算术。这是通过使用宏 `to_pci_dev(dev)` 完成的：

```c
#define to_pci_dev(n) ((struct pci_dev *)container_of(n, struct pci_dev, dev))
```

其中第一个参数是设备指针，第二个参数是包含它的结构，第三个参数是字段名称。同样，也可以从嵌入的设备访问 `pci_driver`：

```c
struct pci_driver *drv;
struct pci_dev *pdev = to_pci_dev(drv);
```

除了少数例外（如 DMA）外，设备不涉及通用结构和函数。例如，PCI 设备填充了 `pci_driver_structure`，并按顺序调用它们的函数以接入系统。然而，这些函数是在统一设备模型范围内使用的；我们对其他类型的设备（如 USB 和网络）也可以这样做。添加新类型的设备只是遵循路径的问题：

## 15.4 sysfs
