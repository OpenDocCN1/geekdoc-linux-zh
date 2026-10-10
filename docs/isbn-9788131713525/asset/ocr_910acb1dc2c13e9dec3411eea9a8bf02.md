# 10.3. MTD Partitions

261

# Listing 10-11

# PQ2FADs Flash Mapping Driver

```
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
```

(continues)