# Managing Kernel Modules

A kernel module consists of object code, which is loaded into the kernel address space at runtime, where it can be executed. When the system starts, it is not known which modules with what functionalities should be loaded, so the module has make itself known to the respective components of the kernel. A module should also remove all references to itself when it is removed from the kernel address space. There are two methods available for these tasks, each kernel module should implement—namely, init_module() and cleanup_module(). We will have a closer look at these methods in Section 2.4.2; first, however we need some general information about the management of kernel modules outside the kernel.

The following tools are used to manually load a module into the kernel, or-remove it from the system:

```
insmod Modename.o [arguments]—This command tries to load a module into the kernel address space. In a successful case, the object code of the module is linked to the kernel; the module can now access the symbols (functions and data structures) of the kernel. Calling insmod causes the following system calls to run implicitly:
sys_create_module() allocates memory space to accommodate the module in the kernel address space.
sys_get_kernel_symbols() returns the kernel's symbol table to resolve the missing references within the module to kernel symbols (See Section 2.4.4).
sys_init_module() copies the module's object code into the kernel address space and calls the module's initialization function (init_module()).
```

When loading a module, we can also pass parameters (e.g., values for device name, interrupt lines, irq, and I/O ports. to_addr). The module itself, these parameters should be designated by the macro PARM(arg, type). When the module is loaded, then these parameters are simply passed by (module name—for example:

```
root@tux # insmod wvlan_cs=1 kernel-name="MyWavelan
```

rmmod Modename removes the specified module from the kernel address space. For this purpose, we use the system call sys_delete_module(), which in turn, calls the module's method cleanup_module().

The module can now be removed, if the module's reference counter is zero, which means that the module is currently not used in any point within the kernel. (See details in [RuCo01]).

modinfo shows information about a module (e.g., its functionality, parameters, and author). This information cannot be generated automatically: it has to be set by the macros MODULE_DESCRIPTION, MODULE_AUTHOR, and so on in the module's source text.