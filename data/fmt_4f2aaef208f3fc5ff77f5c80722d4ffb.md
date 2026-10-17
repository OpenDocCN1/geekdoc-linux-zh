
```c
#include <linux/errno.h>
#include <linux/kernel.h>
#include <linux/major.h>
#include <linux/sched.h>
#include <linux/malloc.h>
#include <linux/delay.h>
#include <linux/scalax.h>
#include <asm/io.h>
#include <asm/irq.h>
#include <asm/uaccess.h>
```

```c
struct scalax_struct scalax_area =
    {0, 0, 0, 0, NULL, NULL, NULL, NULL};
static int scalax_reset(void)
{
    int retval = 0;
    scalax.area.flags = SCALEX_EXIST;
    scalax.area.readin = 0;
    scalax.area.readout = 0;
    scalax.area.writein = 0;
    scalax.area.writeout = 0;
    return retval;
}
```
