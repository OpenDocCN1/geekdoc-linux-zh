# Kernel Module Loading and Linking

The preceding steps indicate, the major kernel subsystems involved in module loading are the module facility and the kernel's runtime linker, krtl, which is loaded early in the bootstrap procedure. The module subsystem does not free a modctl structure when a module is unloaded. The structure remains on the linked list, and the mod_loaded bit is cleared. This is why step 1 searched the list first; if the module was loaded and successfully unloaded, the modctl structure would already exist. This is why a mod_loaded status is maintained—the existence of a modctl structure does not necessarily mean that the module is loaded.

The facts that the Solaris kernel is dynamic in nature and kernel objects can be loaded and unloaded during the life of a running system require that the kernel's symbol table (step 2) exists as a dynamic entity. Each executable file has a symbol table that holds information to resolve an object's symbolic references. A symbolic reference is the correlation of the virtual address of a variable, or its name. The Solaris kernel's symbol table is maintained through a pseudocode, /dev/ksym, and corresponding device driver, /usr/kernel/drv/ksym. In Solaris 7, the symbol table is updated by a kernel thread created specifically for that purpose. The kernel runtime linker issues a wakeup to the ksym_update_thread() when a module is loaded (or unloaded), and the kernel symbol table is updated to reflect the current state of loaded objects.

In Solaris 2.5.1 and 2.6, a different update mechanism is used. A kernel variable is updated when a module is loaded or unloaded. The ksym driver ksym_open() code, the variable is tested to determine whether a new symbol table image needs to be created. The implementation here is that if an open has been issued in the ksym driver, meaning that a user (or program) is examining the kernel symbol table, and a module is loaded or unloaded, the currently opened version will not reflect the change. A close and subsequent event must be issued for an updated view. You can use the mm(1) command to examine an object's symbol table; use /dev/ksym to examine the kernel's.

```
$ nm - /dev/ksym | grep modload
[1953] 0x001108ec 0x00000000 FUNC LOCL 0 ABS  modctl_modload
[10072] 0x0f1113dc 0x000000a0 FUNC GLOB 0 ABS  sallodload
[1973] 0x0f1113d9 0x000000b8 FUNC LOCL 0 ABS  modload_now
[1972] 0x0f1113d1c 0x000000c8 FUNC LOCL 0 ABS  modload_thread
[9926] 0x0f011450 0x000000a4 FUNC GLOB 0 ABS  modloadonly
```

The preceding example shows the symbol table of the running kernel for modload, a kernel function we discussed earlier. The command returned several matches that contain the modload string, including the desired modload function symbol. For more information on symbol tables and specific information on the columns listed, see the nm(1), a(out), and elf(3E) manual pages. Also, refer to any number of texts that describe the Executable and Linking Format (ELF) file, which is discussed in more detail earlier in this chapter.