```
task[nr] = NULL;
REMOVE_LINKS(p);
nr_tasks--;
bad_fork_free_stack:
free_kernel_stack(new_stack);
bad_fork_free_p:
kfree(p);
bad_fork:
return error;
}
```

# resource.c

Another important function of the kernel is how it handles the input/output (I/O) of information to devices. The resource.c handles how the I/O is handled by the kernel. It keeps a table of I/O resources, and places new ones in an empty location on the table. Listing 6-4 opens a device driver for loading. When the driver is loaded, it adds the driver to the iotable, where the device drivers are stored.

# Listing 6-4: Handling I/O

```
/*
* linux/kernel/resource.c
*
* Copyright (C) 1995 Linus Torvalds
*    David Hinds
*
* Kernel io-region resource management
*/

#include <linux/sched.h>
#include <linux/kernel.h>
#include <linux/errno.h>
#include <linux/types.h>
#include <linux/iport.h>

#define IOTABLE_SIZE 128

typedef struct resource_entry_t {
 u_long from, num;
 const char *name;
 struct resource_entry_t *next;
} resource_entry_t;
```