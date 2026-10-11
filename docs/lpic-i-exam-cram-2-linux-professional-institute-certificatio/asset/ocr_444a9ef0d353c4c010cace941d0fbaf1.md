A monolithic kernel has the following advantages:

+   - It has all the neccessary drivers compiled in.
+   - No load time is required for modules.
+   - It's good when you can't update or recompile.

A modular kernel has the following advantages:

+   - The necessary modules can be loaded/unloaded.
+   - It's smaller than a monolithic kernel.
+   - It's best for flexbile systems.

Most Linux systems use a modular kernel or a kernel that includes less compiled-in code and relies more on external modules of code that are loaded on demand.

# ## Modules

Essentially, a *module* is a software driver that enables interaction with hardware from the kernel or processes. If you don't want to wait for modules to load, or want the driver instantly available, compile it into the kernel.

Because the kernel is the arbiter of what has access to the hardware, modules must be made available for the kernel to load if that hardware is to be used. A module is referenced by name and assumed to be in the correct hierarchy of directories under the `/lib/modules` tree.

For example, you can see the current hierarchy of module directories with the following command:

```
```
tree -d /lib/modules
```
```

This returns output that's much lengthier than the following, which has been truncated for brevity:

```
```
/lib/modules
|-- 2.4.10-3
    |-- build -> ../../usr/src/linux-2.4.10-3
    |-- kernel
        |-- abi
        |   |-- cxenix
        |   |-- ibcs
        |   |-- isc
        |   |-- scc
        |   |-- svr4
        |   `-- util
        |       `-- uw7
        `-- arch
            `-- i386
```
```