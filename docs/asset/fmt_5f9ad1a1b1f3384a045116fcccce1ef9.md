
```c
#include <linux/io.h>

unsigned int iread8 (void *addr);
unsigned int iread16 (void *addr);
unsigned int iread32 (void *addr);

void iowrite8 (u8 val, void *addr);
void iowrite16 (u16 val, void *addr);
void iowrite32 (u32 val, void *addr);
```

`addr` 参数应该指向通过 `ioremap()` 获取的地址（带有物理地址偏移量），读取函数返回读取到的值。

多次读写可以使用以下函数完成：

```c
void iread8_rep (void *addr, void *buf, unsigned long count);
void iread16_rep (void *addr, void *buf, unsigned long count);
void iread32_rep (void *addr, void *buf, unsigned long count);

void iowrite8_rep (void *addr, void *buf, unsigned long count);
void iowrite16_rep (void *addr, void *buf, unsigned long count);
void iowrite32_rep (void *addr, void *buf, unsigned long count);
```

这些函数是对特定地址进行 I/O 操作，而不是针对地址范围，即从指向的内核地址读取或向其写入。

64 位架构也有 64 位的读写操作，函数如下：

```c
u64 readq (unsigned long address);
void writeq (unsigned long val, unsigned long address);
```

其用法非常显而易见，其中 `q` 代表 quad（四字节）。目前还没有 `iread64()` 和 `iowrite64()` 函数。

直接操作内存块可以使用以下函数：

```c
void memset_io (void *addr, u8 val, unsigned int count);
void memcpy_io (void *dest, void *source, unsigned int count);
void memcpy_to_io (void *dest, void *source, unsigned int count);
```

上述函数以小端序进行 I/O 操作，并进行任何必要的字节交换，`memmove` 除外，它仅处理字节流且不进行任何交换。

旧的 I/O 函数：

```c
unsigned char readb (unsigned long address);
unsigned short readw (unsigned long address);
unsigned long readl (unsigned long address);
```

```c
void writeb (unsigned char val, unsigned long address);
void writew (unsigned short val, unsigned long address);
void writel (unsigned long val, unsigned long address);
```

这些函数已经过弃，尽管它们仍然可以使用。它们不如新函数那样安全，因为它们没有进行足够彻底的类型检查。

## 19.9 用户态访问 - `ioperm()`, `iopl()`, `/dev/port`

- I/O 端口也可以从用户空间访问。这是一种常用于用户态驱动程序（如 X Server）的技术。执行此类操作的应用必须以 root 权限运行。因此，从稳定性和安全角度来看是危险的。

- 一方法是使用函数：

```c
#include <sys/io.h>

int ioperm(unsigned long from, unsigned long num, int turn_on);
int iopl(int level);
```

- `ioperm()` 获取单个端口的权限，范围从端口地址 `from` 开始的 `num` 个字节，如果 `turn_on = 1` 则启用。

- 前 `0x3ff` 个端口可以通过这种方式访问；对于较大的值，你必须使用 `iopl()`，它赋予对整个 I/O 空间的权限。

参数范围从 0 到 3。小于或等于该值的 Ring 级别将获得 I/O 端口的访问权限；因此，`level=3` 的值允许普通用户应用（在 Ring 3 中）访问 I/O 端口。

- 使用这些设施时，可以在用户空间使用 `inb()`、`outb()` 函数。这需要在开启优化的情况下进行编译，以确保内联函数的展开。

- 另一种方法是使用 `/dev/port` 设备节点。只需跳转到正确的偏移量并使用普通的读写函数即可。这个后门被认为相当危险，但经常在遗留应用程序中使用。

## 19.10 实验

### 实验 1：从用户空间访问 I/O 端口

- 查看 `/proc/ioports` 以找到一个空闲的 I/O 端口区域。一种可能性是使用第一个并行端口（通常在 `0x378`），你应该能够向基地址处的寄存器写入 0，并读取寄存器获取状态信息。

- 使用两种方法尝试对这些端口进行读写：

  - `ioperm()`

  - `/dev/port`

### 实验 2：访问 I/O 端口

- 查看 `/proc/ioports` 以找到一个空闲的 I/O 端口区域。

- 编写一个简单的模块来检查该区域是否可用并请求它。

- 检查并确认该区域已在 `/proc/ioports` 中正确注册。

- 完成后确保释放该区域。

- 模块应该向该区域发送一些数据，并从中读取一些数据。值是否一致？如果不一致，原因是什么？

- 注意：给出了两种解决方案，一种针对旧的区域 API，另一种针对较新的资源 API。

### 实验 3：重映射 I/O 端口

- 修改你的解决方案，使用 `ioremap()` 和正确的读写函数。

### 实验 4：串口鼠标驱动程序

- 将使用 Microsoft 协议的通用串口鼠标连接到空闲的串口。

- 根据你选择的串口，你需要知道相关的 IRQ 和基寄存器地址；即：

表 19.2：串口鼠标节点和寄存器

| 端口 | 节点 | IRQ | IOPORT |
|---|---|---|---|
| com1 | `/dev/ttyS0` | 4 | `0x03f8-0x03ff` |
| com2 | `/dev/ttyS1` | 3 | `0x02f8-0x02ff` |
| com3 | `/dev/ttyS2` | 4 | `0x03e8-0x03ef` |
| com4 | `/dev/ttyS3` | 3 | `0x02e8-0x02ef` |

- 你需要查看鼠标的手页，其中部分提到：

  Microsoft protocol

Microsoft 协议使用 1 位起始位和 7 位数据位。

# 第 20 章. PCI

子系统：ASUSTEK Computer Inc. 未知设备 `82d3`

标志：总线主，快速 devsel，延迟 0

能力：`[e0]` 厂商特定信息

`00ia:1.7` USB 控制器：Intel Corporation 82801JI (ICH10) 家族 Usb22 EHCI 控制器 #2 (prog-if 20 [EHCI])

子系统：ASUSTEK Computer Inc. 未知设备 `82d4`

标志：总线主，中等 devsel，延迟 0，IRQ 18

内存位于 `9ffffc00` (32位，非预取) [size=1K]

能力：`[50]` 电源管理版本 2

能力：`[58]` 调试端口

能力：`[98]` 厂商特定信息

`02:00.0` 以太网控制器：Marvell Technology Group Ltd. 82E8056 PCI-E 千兆网网控制器 (rev 12)

子系统：ASUSTEK Computer Inc. 未知设备 `81f8`

标志：总线主，快速 devsel，延迟 0，IRQ 29

内存位于 `fe9f6c00` (64位，非预取) [size=16K]

I/O 端口位于 `c800` [size=256]

扩展 RUM位于 `fe9c0000` [已禁用] [size=128K]

能力：`[48]` 电源管理版本 3

能力：`[50]` 关键产品数据

能力：`[55]` 消息信号中断：64bit+ Queue=0/0 已启用

能力：`[e0]` Express  legacy端点 IRQ 0

能力：`[100]` 高级错误报告

`01:00.0` VGA 兼容控制器：nvidia Corporation GeForce 8400 GS (rev a) (prog-if 00 [VGA 控制器])

子系统：ASUSTEK Computer Inc. 未知设备 `8278`
