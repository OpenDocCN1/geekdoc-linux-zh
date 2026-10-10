```
```
struct map_info {
char * name; /* Name */
unsigned long size; /* Flash size */
int bankwidth; /* In bytes */
/* ... */
/* You need to implement custom routines for the following methods
only if you have special needs. Else populate them with built-in methods using simple_map_init() as done in Listing 17.3 */
map_word (*read)(struct map_info *, unsigned long);
void (*write)(struct map_info *, const map_word,
unsigned long);
/* ... */
};
```
```

While we are in the topic of accessing flash chips, let’s briefly revisit memory barriers that we discussed in Chapter 4, “Laying the Groundwork.” An instruction reordering that appears semantically unchanged to the compiler (or the processor) may not be so in reality, so the ordering of data operations on flash memory is best left alone. You don’t want to, for example, end up erasing a flash sector after writing to it, instead of doing the reverse. Also, the same flash chips, and hence their device drivers, are used on diverse embedded processors having different instruction reordering algorithms. For these reasons, MTD drivers are notable users of hardware memory barriers. simple_map_write(), a generic routine available to map drivers for use as the write() method in the map_info structure previously listed, inserts a call to mb() before returning. This ensures that the processor does not reorder flash reads or writes across the barrier.

# Listing 17.3. Map Driver Probe Method

```
``` 
Code View:
#include <linux/mtd/mtd.h>
#include <linux/mtd/map.h>
#include <linux/ioport.h>

static int
pda_mtd_probe(struct platform_device *pdev)
{
struct map_info *pda_map;
struct mtd_info *pda_mtd;
struct resource *res = pdev->resource;

/* Populate pda_map with information obtained
from the associated platform device */
pda_map->virt = ioremap_nocache(res->start, (res->end - res->start + 1));
pda_map->name = pdev->dev.bus_id;
pda_map->phys = res->start;
pda_map->size = res->end - res->start + 1;
pda_map->bankwidth = 2; /* Two 16-bit banks sitting
on a 32-bit bus */
simple_map_init(&pda_map); /* Fill in default access methods */

/* Probe via the CFI chip driver */
pda_mtd = do_map_probe("cfi_probe", &pda_map);
/* Register the mtd_partition structure */
add_mtd_partitions(pda_mtd, pda_partitions, 3); /* Three Partitions */
/* ... */
}
```
```