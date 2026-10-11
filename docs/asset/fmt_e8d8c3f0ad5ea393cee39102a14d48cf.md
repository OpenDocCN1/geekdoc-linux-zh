
### 10.3.2 内核命令行分区

如 10.3 节“MTD 分区”中所述，原始 Flash 分区信息可以通过其他方法传递给内核。事实上，最直接的方法（尽管可能不是最简单的方法）是手动直接在内核命令线上传递分区信息。当然，正如我们之前所学，一些引导加载器使这变得很容易（例如 `U-Boot`），而其他引导加载器则在启动时没有向内核传递内核命令行的机制。在这些情况下，内核命令行必须在编译时配置，因此更改起来更加困难，每次修改分区时都需要重新编译内核本身。

要在 MTD 子系统中启用命令行分区，您的内核必须配置为此支持。您可以在图 10-2 的 MTD 分区支持部分看到此配置选项。选择用于解析命令行分区表的选项，该选项定义了 `CONFIG_MTD_CMDLINE_PARTS` 选项。

清单 10-10 显示了在内核命令线上定义分区的格式（摘自 `.../drivers/mtd/cmdlinepart.c`）。

**清单 10-10**
**内核命令行 MTD 分区格式**

```
mtdparts=<mtddev>[;<mtddef>]

* <mtddef>     := <mtd-id>[:<partdef>][;<partdef>]

* <partdef>    := <size>[<offset>][<name>][ro]

* <mtd-id>     : 用于映射驱动/设备 (mtd-name) 的唯一名称

* <size>       : 标准 Linux 内存大小，或者 "-" 表示所有剩余空间

* <name>       : ' NAME '
```

通过内核命令行传递的每个 `mtddef` 参数定义一个单独的分区。如清单 10-10 所示，每个 `mtddef` 定义包含多个部分。您可以指定唯一的 ID、分区大小以及从 Flash 开始处的偏移量。您还可以传递分区名称，并可选地传递只读属性。参考我们在清单 10-5 中的 Redboot 分区定义，我们可以如下在内核命令线上静态定义这些分区：

```
mtdparts=MainFlash:384K(Redboot),4K(config),128K(FIS),-(unused)
```

使用此定义，内核将实例化四个 MTD 分区，其 MTD ID 为 `MainFlash`，包含的大小和布局与在清单 10-5 中发现的大小和布局相匹配。

### 10.3.3 映射驱动

定义您的板级特定 Flash 布局的最终方法是使用专用的板级特定映射驱动。Linux 内核源代码树中包含许多映射驱动示例，位于 `.../drivers/mtd/maps`。其中任何一个都是创建您自己的驱动的良好示例。实现细节因架构而异。

映射驱动是一个合适的内核模块，包含 `module_init()` 和 `module_exit()` 调用，如第 8 章“设备驱动程序基础”中所述。典型的映射驱动很小且易于浏览，通常包含不到几十行 C 代码。

清单 10-11 复制了 `.../drivers/mtd/maps/pq2fads` 的一部分。此映射驱动定义了 Freescale PQ2FADS 评估板上的 Flash 设备，该板支持 MPC8272 和其他处理器。

**清单 10-11**
**PQ2FADs Flash 映射驱动**

```c
static struct mtd_partition pq2fads_partitions[] = {

	{
#define CONFIG_ADS8272

		.name		= "HRCW",

		.size		= 0x040000,

		.offset	= 0,

		.mask_flags = MTD_WRITEABLE,	/* force read-only */
	}, {
		.name		= "User FS",

		.size		= 0x5c0000,

		.offset	= 0x40000,

	}
#else
		.name		= "User FS",

		.size		= 0x060000,

		.offset	= 0,
#endif
	}, {
		.name		= "uImage",

		.size		= 0x010000,

		.offset	= 0x600000,

		.mask_flags = MTD_WRITEABLE,	/* force read-only */
	}, {
		.name		= "bootLoader",

		.size		= 0x040000,

		.offset	= 0x700000,

		.mask_flags = MTD_WRITEABLE,	/* force read-only */
	}, {
		.name		= "bootLoader env",

		.size		= 0x40000,

		.offset	= 0x740000,

		.mask_flags = MTD_WRITEABLE,	/* force read-only */
	}
};

/* pointer to MPC855ADS board info data */
extern unsigned char __res[];

static int __init init_pq2fads_mtd(void)
{
	bd_t *bd = (bd_t *)__res;
	physmap_configure(bd->bi_flashstart, bd->bi_flashsize,
					PQ2FADS_BANK_WIDTH, NULL);
	physmap_set_partitions(pq2fads_partitions,
					sizeof (pq2fads_partitions)/
					sizeof (pq2fads_partitions[0]));
```

（续）

### 10.3.4 Flash 芯片驱动程序

MTD 支持各种各样的 Flash 芯片和设备。你选定的芯片很可能也已被支持。最常见的 Flash 芯片支持前文提到的通用闪存接口（`CFI`）。较旧的 Flash 芯片可能支持 JEDEC，这是一种较旧的闪存兼容性标准。图 10-4 展示了来自最新 Linux 内核快照的内核配置。该版本支持许多类型的闪存。

![](img/7a1144833e62564667e7dd9eb4c9f03d_294_0.png)

#### 图 10-4
Flash 设备支持

如果你的 Flash 芯片不受支持，你必须自己提供一个设备文件。以 `../drivers/mtd/chips` 中的众多示例之一作为起点，自定义或创建你自己的 Flash 设备驱动程序。更甚的是，除非该芯片刚刚引入且具有某种混乱的接口，否则很有可能已经有人编写了驱动程序。

### 10.3.5 特定于板卡的初始化

除了映射驱动程序外，你的特定于板卡（平台）的设置必须提供基础定义，以实现 MTD Flash 系统的正确操作。清单 10-12 复现了 `../arch/arm/mach-1px4xxx/coyote-setup.c` 的相关部分。

#### 清单 10-12
**Coyote 特定板卡设置**

```
static struct flash_platform_data coyote_flash_data = {
  .map_name = "cfi_probe",
  .width = 2,
};

static struct resource coyote_flash_resource = {
  .start = COYOTE_FLASH_BASE,
  .end = COYOTE_FLASH_BASE + COYOTE_FLASH_SIZE - 1,
  .flags = IORESOURCE_MEM,
};

static struct platform_device coyote_flash = {
  .name = "IXP42X-Flash",
  .id = 0,
  .dev = {
    .platform_data = &coyote_flash_data,
  },
  .num_resources = 1,
  .resource = &coyote_flash_resource,
};

...

static struct platform_device *coyote_devices[] __initdata = {
  &coyote_flash,
  &coyote_uart
};

static void __init coyote_init(void)
{
  ...
  platform_add_devices(coyote_devices,
                       ARRAY_SIZE(coyote_devices));
}
...
```
