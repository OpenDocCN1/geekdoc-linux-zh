The kernel maintains a linked list of `modctl` structures for all modules in the kernel, as shown in Figure 4.5.

![](bbox=[0.159, 0.169, 0.898, 0.351])

**Figure 4.5 _Module Control Structures_**

The kernel modules pointer marks the beginning of the doubly linked list of module control structures. Not every structure member is shown in the figure. In addition to the structure links (next and previous pointers), the module identification (`mod_id`) is maintained, along with links to a `mod_modinfo` structure and `mod_linkage` structure. `mod_mp` links to a module structure, defined in the kernel object linker code (`/usr/include/sys/kobj.h`), and used by the kernel run-time linker and the module load facility. Other interesting bits include character string pointers to the directory name, `mod_filename`, that holds the module and the module file name, `mod_modname`.

A given kernel module may depend on the existence of other kernel modules in order to function or may have other kernel modules depend on it. For example, the System V Interprocess Communication (IPC) modules for shared memory, semaphores, and message queues all depend on the kernel `ipc` module to function. Such dependencies are defined in the module code and maintained in the `modctl` structure by pointers in `mod_requisites` (other modules this module depends on) and `mod_dependents` (modules that depend on this one).

The kernel module loading facility is threaded. That is, when the kernel `modload()` function is called (during bootstrap or by the `modload(1M)` command), it creates a kernel thread to perform the module load function. The benefit here is that concurrent module loads are possible on multiprocessor systems and so provide faster system boot and initialization. Once the kernel thread is created, the following series of events is executed to complete the loading and linking of the module.

+   1. Create and allocate a `modctl` structure. First, search the linked list of `modctl` structures, looking for a match to the module name (`mod_modname`). If a match is found, return address of existing structure; otherwise, create a new one. Add a new `modctl` structure to the linked list.
+   2. Enter the kernel runtime linker, `krtld`, to create address space segments