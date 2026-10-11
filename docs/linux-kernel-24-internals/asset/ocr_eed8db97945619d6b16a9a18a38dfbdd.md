```
```c
#define __initdata     __attribute__ (``section__ (".data.init"))
#else
#define __init
#define __initdata
#endif
```
```

What this means is that if the code is compiled statically into the kernel (i.e. MODULE is not defined) then it is placed in the special ELF section .text.init, which is declared in the linker map in arch/i386/vmlinux.lds. Otherwise (i.e. if it is a module) the macros evaluate to nothing.

What happens during boot is that the "init" kernel thread (function init/main.c:init()) calls the arch-specific function free_initmem() which frees all the pages between addresses __init_begin and __init_end.

On a typical system (my workstation), this results in freeing about 260K of memory.

The functions registered via module_init() are placed in .initcall.init which is also freed in the static case. The current trend in Linux, when designing a subsystem (not necessarily a module), is to provide init/exit entry points from the early stages of design so that in the future, the subsystem in question can be modularised if needed. Example of this is pipel, see fs/pipe.c. Even if a given subsystem will never become a module, e.g. bdflush (see fs/buffer.c), it is still nice and tidy to use the module_init() macro against its initialisation function, provided it does not matter when exactly is the function called.

There are two more macros which work in a similar manner, called __exit and __exitdata, but they are more directly connected to the module support and therefore will be explained in a later section.

# # 1.9 Processing kernel command line

Let us recall what happens to the commandline passed to kernel during boot:

+   1. LILO (or BCP) accepts the commandline using BIOS keyboard services and stores it at a well-known location in physical memory, as well as a signature saying that there is a valid commandline there.

+   2. arch/i386/kernel/head.S copies the first 2k of it out to the zeropage. Note that the current version (21) of LILO chops the commandline to 79 bytes. This is a nontrivial bug in LILO (when large EBDA support is enabled) and Werner promised to fix it sometime soon. If you really need to pass commandlines longer than 79 bytes then you can either use BCP or hardcode your commandline in arch/i386/kernel/setup.c:parse_mem_cmdline() function.

+   3. arch/i386/kernel/setup.c:parse_mem_cmdline() (called by setup_arch(), itself called by start_kernel()) copies 256 bytes from zeropage into saved_command_line which is displayed by /proc/cmdline. This same routine processes the "mem=" option if present and makes appropriate adjustments to VM parameters.

+   4. We return to commandline in parse_options() (called by start_kernel()) which processes some "in-kernel" parameters (currently "init=" and environment/arguments for init) and passes each word to checksetup().

+   5. checksetup() goes through the code in ELF section .setup.init and invokes each function, passing it the word if it matches. Note that using the return value of 0 from the function registered via __setup(), it is possible to pass the same "variable=value" to more than one function with "value" invalid to one and valid to another. Jeff Garzik commented: "hackers who do that get spanked :)"