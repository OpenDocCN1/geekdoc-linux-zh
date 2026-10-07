Unfortunately, we don't have an easy way to unregister a task from a task list.

Since cleanup.module can't return with an error code (it's a void function), the solution is not to let it return at all. Instead, it calls sleep_on or module_sleep_on¹ to put the rmod process to sleep. Before that, it informs the function called on the timer interrupt by setting a global variable. Then, on the next timer interrupt, the rmod process will be woken up, when our function is no longer in the queue and it's safe to remove the module.

# sched.c

```
/* sched.c - schedule a function to be called on
* every timer interrupt. */
```

```
/* Copyright (C) 1998 by Ori Pomerantz * */
```

```
/* The necessary header files */
* Standard in kernel modules */
#include <linux/kernel.h> */* We're doing kernel work */
#include <linux/module.h> */* Specifically, a module */
```

```
/* Deal with CONFIG_MODVERSIONS */
#if CONFIG_MODVERSIONS=1
#define MODVERSIONS
#include <linux/modversions.h>
#endif
```

```
/* Necessary because we use the proc fs */
#include <schedule/proc_fs.h>
```

```
/* We schedule tasks here */
#include <linux/tqueue.h>
```

> ¹They're really the same.