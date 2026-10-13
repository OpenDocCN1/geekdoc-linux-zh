
and bindings, and load the object into memory.

- a) Allocate `module` structure().
- b) Allocate space for the module’s symbols in the kernel’s `kobj_map` resource map.
- c) Loop through the segments of the module being loaded, and allocate and map space for text and data.
- d) Load kernel object into memory, linking the object’s segments into the appropriate kernel address space segments.

3. Set the `mod_loaded` bit in the module’s `modctl` structure, and increment the `mod_loadcnt`.

4. Create a link to module’s `mod_linkage` structure.

5. Execute the module’s `mod_install` function indirectly by looking up the `module_init()` routine and calling it.

As the preceding steps indicate, the major kernel subsystems involved in module loading are the module facility and the kernel’s runtime linker, `krtld`, which is loaded very early in the bootstrap procedure. The module subsystem does not free a `modctl` structure when a module is unloaded. The structure remains on the linked list, and the `mod_loaded` bit is cleared. This is why step 1 searched the list first; in case the module was loaded and subsequently unloaded, the `modctl` structure would already exist. This is also why a `mod_loaded` status bit is maintained—the existence of a `modctl` structure does not necessarily mean that the module is loaded.

The facts that the Solaris kernel is dynamic in nature and that kernel objects can be loaded and unloaded during the life of a running system require that the kernel’s symbol table (step 2) exist as a dynamic entity. All executable object files have a symbol table that holds information required to resolve an object’s symbolic references. A symbolic reference is the correlation of the virtual address of a function or variable, and its name. The Solaris kernel’s symbol table is maintained through a pseudodevice, `/dev/ksyms`, and corresponding device driver, `/usr/kernel/drv/ksyms`. In Solaris 7, the kernel symbol table is updated by a kernel thread created specifically for that purpose. The kernel runtime linker issues a wakeup to the `ksyms_update_thread()` when a module is loaded (or unloaded), and the kernel symbol table is updated to reflect the current state of loaded kernel objects.

In Solaris 2.5.1 and 2.6, a different update mechanism is used. A kernel variable is updated when a module is loaded or unloaded. Inside the ksyms driver `ksyms_open()` code, the variable is tested to determine whether a new symbol table image needs to be created. The implication here is that if an open has been issued in the ksyms driver, meaning that a user (or program) is examining the kernel symbol table, and a kernel module is loaded or unloaded, then the currently opened version will not reflect the change. A close and subsequent open must be issued for an updated view. You can use the `nm(1)` command to examine an object’s symbol table; use `/dev/ksyms` to examine the kernel’s table.

```text
# nm -x /dev/ksyms | grep modload
[1953]  0xf01108c  0x00000060 FUNC LOCAL  0  ABS  modctl_modload
[1072]  0xf01113c  0x000000a0 FUNC GLOB   0  ABS  modload
[1973]  0xf011398  0x000000b8 FUNC LOCAL  0  ABS  modload_now
[1972]  0xf0111d8  0x00000008 FUNC LOCAL  0  ABS  modload_thread
[9926]  0xf011450  0x000000a4 FUNC GLOB   0  ABS  modloadonly
```

The preceding example searches the symbol table of the running kernel for modload, a kernel function we discussed earlier. The command returned several matches that contain the modload string, including the desired modload function symbol. (For more information on symbol tables and specific information on the columns listed, see the `nm(1)`, `a.out(4)`, and `elf(3E)` manual pages. Also, refer to any number of texts that describe the Executable and Linking Format (ELF) file, which is discussed in more detail in Chapter 4.)

In step 5, we indicate that the module install code is invoked indirectly through the module’s `_init()` function. Several functions must be included in any loadable kernel module to facilitate dynamic loading. Device drivers and STREAMS modules must be coded for dynamic loading. As such, a loadable driver interface is defined. In general, the required routines and data structures that are documented apply to all loadable kernel modules—not just to drivers and STREAMS modules (although there are components that are specific to drivers)—and do not apply to objects such as loadable system calls, file systems, or scheduling classes.

Within a loadable kernel object, an initialization, information, and finish routine must be coded, as per the definitions in the `_init(9E)`, `_info(9E)`, and `_fini(9E)` manual pages. A module’s `_init()` routine is called to complete the process of making the module usable after it has been loaded. The module’s `_info()` and `_fini()` routines also invoke corresponding kernel module management interfaces, as shown in Table 4-2.

### Table 4-2 Module Management Interfaces

| Kernel Module Routine | Module Facility Interface | Description |
|---|---|---|
| `_init()` | `mod_install()` | Loads a kernel module. |
| `_info()` | `mod_info()` | Retrieves module information. |
| `_fini()` | `mod_remove()` | Unloads a kernel module. |

Module installation is abstracted to define a generic set of structures and interfaces within the kernel. Module operations function pointers for installing, removing, and information gathering (the generic interfaces shown in Table 4-2) are maintained in a mod_ops structure, which is extended to provide a definition for each type of loadable module. For example, there is a `mod_installsys()` function specific to loading system calls, a `mod_install_drv()` function specific to loading device drivers, and so forth.

For each of these module types, a module linkage structure is defined; it contains a pointer to the operations structure, a pointer to a character string describing the module, and a pointer to a module-type-specific structure. For example, the linkage structure for loadable system calls, `modlsys`, contains a pointer to the system entry table, which is the entry point for all system calls. Each loadable kernel module is required to declare and initialize the appropriate type-specific linkage structure, as well as a generic `modlinkage` structure that provides the generic abstraction for all modules.

Within the module facility is a module type-specific routine for installing modules, entered through the `MODL_INSTALL` macro called from the generic `mod_install()` code. More precisely, a loadable module’s `_init()` routine calls `mod_install()`, which vectors to the appropriate module-specific routine through the `MODL_INSTALL` macro. This procedure is shown in Figure 4.6.

![](img/220ae4af07df2fe8e5be69d27f885d1b_162_0.png)

### Figure 4.6 Module Operations Function Vectoring

Figure 4.6 shows the data structures defined in a loadable kernel module: the generic `modlinkage`, through which is referenced a type-specific linkage structure (`modlxxx`), which in turn links to a type-specific operations structure that contains pointers to the type-specific functions for installing, removing, and gathering information about a kernel module. The `MODL_INSTALL` macro is passed the address of the module’s generic linkage structure and from there vectors in to the appropriate function. The module-specific installation steps are summarized in Table 4-3.

### Table 4-3 Module Install Routines

| Module Type | Install Function | Summary |
|---|---|---|
| Device driver | `mod_install_drv` | Wrapper for `ddi_installdrv()`. Install the driver entry in the kernel devops table. |
| System call | `mod_installsys` | Install the system call’s sysent table entry in the kernel sysent table. |
| File system | `mod_installfs` | Installs the file system Virtual File System (VFS) switch table entry. |
| STREAMS modules | `mod_installstrmod` | Install the STREAMS entry in the kernel fmodsw switch table. |
| Scheduling class | `mod_installsched` | Install the scheduling class in the kernel `sclass` array. |
| Exec module | `mod_installexec` | Install the exec entry in the kernel execsw switch table. |

The summary column in Table 4-3 shows a definite pattern to the module installation functions. In many subsystems, the kernel implements a switch table mechanism to vector to the correct kernel functions for a specific file system, scheduling class, exec function, etc. The details of each implementation are covered in subsequent areas of the book, as applicable to a particular chapter or heading.

As we’ve seen, the dynamic loading of a kernel module is facilitated through two major kernel subsystems: the module management code and the kernel runtime linker. These kernel components make use of other kernel services, such as the kernel memory allocator, kernel locking primitives, and the kernel ksym driver, taking advantage of the modular design of the system and providing a good example of the layered model discussed earlier.
