# # Chapter 1

# # Hello, world

When the first caveman programmer chiseled the first program on the walls of the first computer, it was a program began to paint the string 'Hello, world' in Antelope pictures. Roman programming textbooks began with the 'Salut, Mundi' program. I don't know what happens to people who break with this tradition, and I think it's safer not to find out.

A kernel module has to have at least two functions: init_module which is called when the module is inserted into the kernel, and cleanup_module which is called just before it is removed. Typically, init_module either registers a handler for something with the kernel, or replaces one of the kernel function with its own code (usually code to do something). The cleanup_module function is supposed to undo whatever init_module did, so the module can be unloaded safely.

```
helloc
/* hello.c
 * Copyright (C) 1998 by Ori Pomerantz
 *
 * "Hello, world" - the kernel module version.
 */

/* The necessary header files */
/* Standard in kernel modules */
#include <linux/kernel.h>    /* We're doing kernel work */
```