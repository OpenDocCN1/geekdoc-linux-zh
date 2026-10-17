
```c
static map_desc imx6_pm_desc[] __initdata = {
imx6_map_entry(IMX6Q, MMDC_P0, MT DEVICE),
imx6_map_entry(IMX6Q, MMDC_P1, MT DEVICE),
imx6_map_entry(IMX6Q, SRC, MT DEVICE),
imx6_map_entry(IMX6Q, IOMUXC, MT DEVICE),
imx6_map_entry(IMX6Q, CCM, MT_DEVICE),
imx6_map_entry(IMX6Q, ANATOP, MT DEVICE),
imx6_map_entry(IMX6Q, GPC, MT DEVICE),
imx6_map_entry(IMX6Q, L2, MT DEVICE),
imx6_map_entry(IMX6Q, SEMA4, MT DEVICE),
};
```

参阅 `imx6_map_entry` 宏（位于 `Linux/arch/arm/mach-imx/hardware.h`）：

```c
#define imx6_map_entry(soc, name, _type) {
  .virtual = soc ## __IO_P2V(soc ## __name ## __BASE_ADDR),
  .pfn = __phys_to_pfn(soc ## __name ## __BASE_ADDR),
  .length = soc ## __name ## SIZE,
  .type = _type,
}
```

在 `Linux/arch/arm/mach-imx/mx6.h` 中：

```c
#define MX6Q_IO_P2V(x) IMX_IO_P2V(x)
```

`/* IMX_IO_P2V(x) 定义在 hardware.h */`

内存映射由 `map_desc` 结构体数组组成。该结构体位于 `Linux/arch/arm/include/asm/map.h`，包含四个元素。这些元素是虚拟地址、长度和页帧号的 `unsigned long` 类型，而类型是 `unsigned int` 类型：

```c
struct map_desc {
  unsigned long virtual;
  unsigned long pfn;
  unsigned long length;
  unsigned int type;
};
```

从内存映射中获得的信息如下：

- 1. `imx6_pm_io_desc[]` 数组中有9个 `map_desc` 结构体。
- 2. `.virtual` 字段是定义 `map_desc` 的虚拟地址。
- 3. `.pfn` 字段是 `map_desc` 项页帧号的地址。页帧号是去掉了偏移值后的物理地址，并将页值右移的结果。

```c
/* 将物理地址转换为页号并反之 */
#define phys_to_pfn (paddr) ((paddr) >> PAGE_SHIFT)
#define pfn_to_phys (pfn) ((pfn) << PAGE_SHIFT)
```

参阅 `Linux/arch/mach-imx6.h` 中根据 `imx6_pm_io_desc` `map_desc` 数组将进行映射的物理地址：

```c
#define MX6Q_L2_BASE_ADDR 0x00a2000
#define MX6Q_L2_SIZE 0x1000
#define MX6Q_IOMUXC_BASE_ADDR 0x020a0000
#define MX6Q_IOMUXC_SIZE 0x4000
#define MX6Q_SRC_BASE_ADDR 0x020d8000
#define MX6Q_SRC_SIZE 0x4000
#define MX6Q_CCM_BASE_ADDR 0x020c4000
#define MX6Q_CCM_SIZE 0x4000
#define MX6Q_ANATOP_BASE_ADDR 0x020c8000
#define MX6Q_ANATOP_SIZE 0x1000
#define MX6Q_GPC_BASE_ADDR 0x020dc000
#define MX6Q_GPC_SIZE 0x4000
#define MX6Q_SEMA4_BASE_ADDR 0x02229000
#define MX6Q_SEMA4_SIZE 0x4000
#define MX6Q_MMDC_P0_BASE_ADDR 0x021b0000
#define MX6Q_MMDC_P0_SIZE 0x4000
#define MX6Q_MMDC_P1_BASE_ADDR 0x021b4000
#define MX6Q_MMDC_P1_SIZE 0x4000
```

（注：上一个代码块中的十六进制地址和大小存在 OCR 错误，已根据标准的 i.MX6 进行修正）。

# 内核分配器

slab 分配技术的主要目的是有效地管理对象的分配并防止碎片。内核对象是相同类型的对象，通常以 C 结构体的形式表示。这些对象仅供内核、模块和运行在内核空间的驱动程序使用。对象的大小可以小于页大小。slab 分配器根据对象的数量按需要增加或减少缓存的大小，并使用页分配器来分配和释放页。

# 页分配器 API

要分配内存，以下是一些标志：

- `GFP_KERNEL`：标准内核分配。分配可能会阻塞。
- `GFP_ATOMIC`：用于紧急上下文，不允许阻塞。
- `GFP_DMA`：在用于 DMA 传输的区域分配内存。

```c
unsigned long get_page(int flags) /* 返回虚拟地址 */
```

```c
unsigned long get_free_page(int flags) /* 相同，但不进行初始化 */
```

```c
unsigned long get_pages(int flags, unsigned int order) /* 返回多个页区域的起始地址 */
```

# SLAB 分配器

slab 分配器允许创建“缓存”，每个类型一个缓存（例如 `inode_cache`、`dentry_cache`、`buffer_head`、`vm_area_struct`）。每个缓存包含多个“slab”（通常为一页长且连续），每个 slab 包含多个对象。slab 分配器由可变的缓存组成，这些缓存在一个称为“缓存链”的双向循环链表中连接在一起。为了减少碎片，slab 被分为三组：

- 无空闲对象的满 slab。
- 部分 slab。
- 无已分配对象的空 slab。

存在部分 slab，则新的分配将从这些 slab 中进行，否则将从空 slab 中进行。

在下图中，你可以看到 SLAB 分配器的通用内存布局：

![](img/739a35b59067f8a55eff80a58765146f_300_0.png)

为了理解 Linux 内核 SLAB 分配器，定义了以下术语，这些术语频繁出现在 SLAB 分配器的源代码中：

### 术语

- 1. **Cache（缓存）**：`Cache` 是同一类型内核对象的组。`Cache` 由一个名称标识，该名称通常与 C 结构体的名称相同。内核使用双向链表来连接创建的 `Cache`。
- 2. **Slab（内存）**：`Slab` 是存储在主内存一个或多个物理页中的连续内存块。每个 `Cache` 拥有若干个 `Slab`，用于存储相同类型的实际内核对象。
- 3. **Kernel object（内核对象）**：内核对象是 C 结构体的分配并初始化的实例。每个 `Slab` 可能会包含一些对象（取决于 slab 的大小和每个对象的大小）。`Slab` 中的内核对象可以是活跃的（内核正在使用该对象）或空闲的（对象在内存池中并准备好在请求时使用）。

## SLAB 分配器 API

Linux 内核 slab 分配子系统提供了一个通用接口，无论 SLAB 分配器的类型，都可以创建和销毁内存缓存。

- 1. `Kmem_cache_create()` 函数创建一个新的内存缓存：

```c
struct kmem_cache *kmem_cache_create(const char *name, size_t size, size_t align, unsigned long flags, void (*ctor)(void))
```

- `name`：用于在 `/proc/slabinfo` 中标识此缓存的字符串。
- `size`：在此缓存中创建的对象的大小。
- `align`：每个对象对象添加的额外空间（用于存储某些额外数据）。
- `flags`：SLAB 标志位。
- `constructor`：用于初始化对象。

成功时返回缓存的指针，失败时返回 NULL。

- 2. `Kmem_cache_destroy()` 函数通过提供已销毁缓存的 `kmem_cache` 对象来销毁内存缓存：

```c
void kmem_cache_destroy(struct kmem_cache *cp)
```
