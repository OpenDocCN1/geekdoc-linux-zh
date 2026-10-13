and bindings, and load the object into memory.

+   a) Allocate `module` structure().
+   
+   b) Allocate space for the module’s symbols in the kernel’s `kobj_map` resource map.
+   
+   c) Loop through the segments of the module being loaded, and allocate and map space for text and data.
+   
+   d) Load kernel object into memory, linking the object’s segments into the appropriate kernel address space segments.

+   3. Set the `mod_loaded` bit in the module’s `modctl` structure, and increment the `mod_loadcnt`.
+   
+   4. Create a link to module’s `mod_linkage` structure.
+   
+   5. Execute the module’s `mod_install` function indirectly by looking up the `module_init()` routine and calling it.

As the preceding steps indicate, the major kernel subsystems involved in module loading are the module facility and the kernel’s runtime linker, `krtld`, which is loaded very early in the bootstrap procedure. The module subsystem does not free a `modctl` structure when a module is unloaded. The structure remains on the linked list, and the `mod_loaded` bit is cleared. This is why step 1 searched the list first; in case the module was loaded and subsequently unloaded, the `modctl` structure would already exist. This is also why a `mod_loaded` status bit is maintained—the existence of a `modctl` structure does not necessarily mean that the module is loaded.

The facts that the Solaris kernel is dynamic in nature and that kernel objects can be loaded and unloaded during the life of a running system require that the kernel’s symbol table (step 2) exist as a dynamic entity. All executable object files have a symbol table that holds information required to resolve an object’s symbolic references. A symbolic reference is the correlation of the virtual address of a function or variable, and its name. The Solaris kernel’s symbol table is maintained through a pseudodevice, `/dev/ksyms`, and corresponding device driver, `/usr/kernel/drv/ksyms`. In Solaris 7, the kernel symbol table is updated by a kernel thread created specifically for that purpose. The kernel runtime linker issues a wakeup to the `ksyms_update_thread()` when a module is loaded (or unloaded), and the kernel symbol table is updated to reflect the current state of loaded kernel objects.

In Solaris 2.5.1 and 2.6, a different update mechanism is used. A kernel variable is updated when a module is loaded or unloaded. Inside the ksyms driver `ksyms_open()` code, the variable is tested to determine whether a new symbol table image needs to be created. The implication here is that if an open has been issued in the ksyms driver, meaning that a user (or program) is examining the kernel symbol table, and a kernel module is loaded or unloaded, then the currently opened version will not reflect the change. A close and subsequent open must be