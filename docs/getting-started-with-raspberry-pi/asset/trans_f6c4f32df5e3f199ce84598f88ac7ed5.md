
对于断电可能突然发生、且存储器件只能承受有限次数擦写的嵌入式系统而言，这种限制尤为关键。在闪存的擦除操作期间，当前扇区的内容会被保存至 RAM（随机存取存储器）。如果在缓慢的擦除过程中发生断电，该扇区的全部内容可能会丢失。JFFS2 采用日志结构设计来规避这一问题。新数据会被追加到位于已擦除区域的日志中。每个 JFFS2 节点都包含元数据，用于追踪离散的文件位置。系统会定期通过垃圾回收机制回收内存。得益于这种设计，闪存写入无需经过“保存-擦除-写入”的循环，从而提高了断电时的可靠性。此外，日志结构还通过分散写入操作延长了闪存的寿命。

若要为位于 `/path/to/filesystem/` 下的目录树创建一个针对擦除大小为 256KB 闪存芯片的 JFFS2 镜像，请使用 `mkfs.jffs2` 执行以下操作：

```bash
bash> mkfs.jffs2 -e 256KiB -r /path/to/filesystem/ -o jffs2.img
```

JFFS2 包含一个*垃圾回收器*（GC），用于回收不再使用的闪存区域。垃圾回收算法依赖于擦除大小，因此提供准确的值可以使其效率更高。要获取闪存分区的擦除大小，可以查看 `/proc/mtd`。图 17.2 中所示的 Linux 手持设备的输出如下：

```bash
bash> cat /proc/mtd
dev:    size     erasesize  name
mtd0: 00100000  00040000   "pda_btldr"
mtd1: 00200000  00040000   "pda_krn1"
mtd2: 01400000  00040000   "pda_fs"
```

JFFS2 支持压缩功能。启用 `CONFIG_JFFS2_COMPRESSION_OPTIONS` 下的相应选项以选择可用的压缩算法，并查看 `fs/jffs2/compr*.c` 以了解其实现。

请注意，JFFS2 文件系统镜像通常是在进行交叉开发的主机上创建的，然后通过合适的下载机制（如串行端口、USB 或 NFS）传输到目标设备的指定闪存分区。关于此内容的更多细节，请参阅第 18 章“嵌入式 Linux”。

## YAFFS2

2.6 内核中的 JFFS2 实现包含针对 NAND 闪存限制的功能，但*又一个闪存文件系统*（YAFFS）是专为在 NAND 内存特定约束下运行而设计的文件系统。YAFFS 并非主线内核的一部分，但一些嵌入式发行版预先为其内核打上了支持 YAFFS2（YAFFS 的当前版本）的补丁。

你可以从 www.yaffs.net 下载 YAFFS2 的源代码和文档。

## MTD 工具

可以从 ftp://ftp.infradead.org/pub/mtd-utils/ 下载的 MTD-utils 软件包包含若干实用工具，它们运行在支持 MTD 的闪存之上。包含的工具示例有 *flash-eraseall*、*nanddump*、*nandwrite* 和 *sumtool*。

要擦除第二个闪存分区（在 NOR 或 NAND 设备上），请如下使用 `flash-eraseall`：

```bash
bash> flash-eraseall -j /dev/mtd/2
```

由于 NAND 芯片可能包含坏块，建议使用支持 ECC 的程序（如 `nandwrite` 和 `nanddump`）来复制原始数据，而不是使用 `dd` 等通用工具。要将之前创建的 JFFS2 镜像存储到第二个 NAND 分区，请执行以下操作：

```bash
bash> nandwrite /dev/mtd/2 jffs2.img
```

你可以使用 `sumtool` 将摘要信息插入到 JFFS2 镜像中，并在配置内核时启用 `CONFIG_JFFS2_SUMMARY`，从而减少 JFFS2 的挂载时间。要将带有摘要的 JFFS2 镜像写入之前的 NAND 闪存，请执行以下操作：

```bash
bash> sumtool -e 256KiB -i jffs2.img -o jffs2.summary.img
bash> nandwrite /dev/mtd/2 jffs2.summary.img
bash> mount -t jffs2 /dev/mtdblock/2 /mnt
```

## 配置 MTD

要启用内核的 MTD 支持，你必须选择合适的配置选项。对于**图 17.2**中所示的闪存芯片，所需的选项如下：

```text
CONFIG_MTD=y             # 启用 MTD 子系统
CONFIG_MTD_PARTITIONS=y  # 支持多个分区
CONFIG_MTD_GEN_PROBE=y   # 芯片探测的通用例程
CONFIG_MTD_CFI=y         # 启用 CFI 芯片驱动程序
CONFIG_MTD_PDA_MAP=y     # 启用映射驱动程序的选项
CONFIG_JFFS2_FS=y        # 启用 JFFS2
```

假设 **CONFIG_MTD_PDA_MAP** 是新增的选项，用于启用我们之前编写的映射驱动程序。除非你有基于 MTD 的根文件系统，否则这些功能也可以作为内核模块构建。要在启动期间将**图 17.2**中的文件系统分区作为根设备挂载，请要求引导加载程序在其传递给内核的命令字符串中添加 `root=/dev/mtdblock/2`。

你可以通过消除冗余探测来减少内核的占用空间。由于我们的示例手持设备具有两个位于 32 位物理总线上的并行 16 位存储体（从而导致双向交叉和 2 字节的存储体宽度），你可以使用以下额外选项进行优化：

```text
CONFIG_MTD_CFI_ADV_OPTIONS=y
CONFIG_MTD_CFI_GEOMETRY=y
CONFIG_MTD_MAP_BANK_WIDTH_2=y
CONFIG_MTD_CFI_I2=y
```

**CONFIG_MTD_MAP_BANK_WIDTH_2** 启用 CFI 总线宽度为 2，**CONFIG_MTD_CFI_I2** 设置交叉值为 2。

## 执行内存直接运行

通过**执行内存直接运行**（XIP，eXecute In Place），你可以直接从闪存中运行内核。由于去除了将内核复制到 RAM 的额外步骤，内核启动速度会更快。缺点是闪存内存的需求量会增加，因为内核必须以未压缩的形式存储。在决定采用 XIP 方案之前，也请意识到，从闪存中获取指令的较慢速度可能会影响运行时性能。

## 固件集线器

PC 兼容系统使用一个名为固件集线器（FWH，Firmware Hub）的 NOR 闪存芯片来保存 BIOS。FWH 并未直接连接到处理器的地址和数据总线。相反，它通过低引脚计数（LPC）总线进行接口连接，该总线是南桥芯片组的一部分。连接示意图如图 17.5 所示。

![](img/07cc6f9c8c74622020874f66bfb53dc4_482_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_482_1.png)

MTD 子系统包含用于将处理器与 FWH 进行接口连接的驱动程序。FWH 通常不符合 CFI 规范。相反，它们符合 JEDEC（联合电子设备委员会）标准。为了让 MTD 识别尚未支持的 JEDEC 芯片，请在 `drivers/mtd/chips/jedec_probe.c` 中的 `jedec_table` 数组中添加一个条目，其中包含芯片制造商 ID 和命令集 ID 等信息。以下是一个示例：

```c
static const struct amd_flash_info jedec_table[] = {
	/* ... */
	{
		.mfr_id = MANUFACTURER_ID,	/* 例如：MANUFACTURER_ST */
		.dev_id = DEVICE_ID,		/* 例如：M50FW080 */
		.name = "MYNAME",		/* 例如："M50FW080" */
		.uaddr = {
			[0] = MTD_UADDR_UNNECESSARY,
		},
		.dev_size = SIZE_1MiB,		/* 例如：1MB */
		.cmd_set = CMDSET,		/* 用于与闪存芯片通信的命令集，
					 * 例如 P_ID_INTEL_EXT */
		.num_erase_regions = 1,	/* 一个区域 */
		.regions = {
			ERASEINFO (0x10000, 16),/* 十六个 64K 扇区 */
		}
	},
	/* ... */
};
```

当你按照此处所示将芯片详细信息录入 `jedec_table` 后，只要你启用了正确的内核配置选项，MTD 就应该能识别你的闪存。以下配置使内核能够识别通过 Intel ICH2 或 ICH4 南桥芯片组与处理器接口连接的 FWH：

```text
CONFIG_MTD=y             # 启用 MTD 子系统
CONFIG_MTD_GEN_PROBE=y   # 芯片探测的通用例程
CONFIG_MTD_JEDECPROBE=y  # JEDEC 芯片驱动程序
CONFIG_MTD_CFI_INTELEXT=y # 与芯片通信的命令集
CONFIG_MTD_ICHXROM=y     # 映射驱动程序
```

`CONFIG_MTD_JEDECPROBE` 启用 JEDEC MTD 芯片驱动程序，`CONFIG_MTD_ICHXROM` 添加将 FWH 映射到处理器地址空间的 MTD 映射驱动程序。此外，你还必须包含适当的命令集实现（例如，对于 Intel 扩展命令使用 `CONFIG_MTD_CFI_INTELEXT`）。

加载这些模块后，你可以通过 MTD 导出的设备节点从用户空间应用程序与 FWH 通信。例如，你可以使用一个简单的应用程序从用户空间重新编程 BIOS，如清单 17.5 所示。警告：错误地操作该程序可能会损坏 BIOS 并导致系统无法启动！

清单 17.5 操作的是与 FWH 关联的 MTD 字符设备，假设该设备为 `/dev/mtd/0`。该程序发出三个 MTD 专用的 `ioctl` 命令：

- `MEMUNLOCK` 在编程之前解锁闪存扇区
- `MEMERASE` 在重写之前擦除闪存扇区
- `MEMLOCK` 在编程后重新锁定扇区

### 清单 17.5. 更新 BIOS

```c
#include <linux/mtd/mtd.h>
#include <stdio.h>
#include <fcntl.h>
#include <asm/ioctl.h>
#include <signal.h>
#include <sys/stat.h>

#define BLOCK_SIZE      4096
#define NUM_SECTORS     16
#define SECTOR_SIZE     64*1024

int
main(int argc, char *argv[])
{
    int fwh_fd, image_fd;
    int usect=0, lsect=0, ret;
    struct erase_info_user fwh_erase_info;
    char buffer[BLOCK_SIZE];
}
```
