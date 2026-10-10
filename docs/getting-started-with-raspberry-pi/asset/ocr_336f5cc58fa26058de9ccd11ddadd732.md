# Kernel Hacking Config Options

Several options exist under Kernel hacking in the kernel configuration menu that can emit valuable debug information. If you enable an option, corresponding debug code gets compiled when you build the kernel.[9] Here are a few examples:

+   1. Show Timing information on prints (CONFIG_PRINTK_TIME) adds timing instrumentation to printk() output, so you can use prints as checkpoints for measuring execution times and identifying slow code regions.
+   
+   2. Using freed memory results in memory poisoning. Debug slab memory allocations (CONFIG_DEBUG_SLAB) helps you detect such problems.
+   
+   3. Spinlock and rw-lock debugging: basic checks (CONFIG_DEBUG_SPINLOCK) finds lock-related problems such as uninitialized spinlock usage and helps catch code that is not SMP-safe.
+   
+   4. You have already worked with Magic SysRq key (CONFIG_MAGIC_SYSRQ) when you learned to use kdump. If you turn this on, you will have some avenues left even if the kernel crashes during debugging. For example, pressing Alt-Sysrq-t produces a dump of current tasks, whereas Alt-Sysrq-p prints the contents of processor registers.
+   
+   5. Detect Soft Lockups (CONFIG_DETECT_SOFTLOCKUP) utilizes the services of a watchdog to detect tight loops in kernel code that last for more than 10 seconds. We looked at this when we analyzed a kernel hang using kdump. Note that hardware lockups cannot be found this way. For that, use the services of a Non-Maskable Interrupt (NMI)-watchdog if your platform supports it.
+   
+   6. If you enable CONFIG_DEBUG_SLAB, CONFIG_DEBUG_HMEM, or CONFIG_DEBUG_PAGE_ALLOC while configuring your kernel, additional error-checking code gets compiled that help debug problems related to memory management.
+   
+   7. Check for stack overflows (CONFIG_DEBUG_STACKOVERFLOW) adds code to emit warnings if the available stack space falls below a threshold. Stack utilization instrumentation (CONFIG_DEBUG_STACK_USAGE) adds stack space instrumentation to the magic Sysrq key output. Another related option, CONFIG_4KSTACKS, lets you set the kernel stack size to 4KB rather than 8KB.
+   
+   8. Verbose BUG() reporting (CONFIG_DEBUG_BUGVERBOSE) produces extra debug information when any kernel code invokes BUG(), assuming that you have CONFIG_BUG turned on during kernel configuration.

Some debug options live outside the Kernel hacking submenu, too. For example, we enabled CONFIG_KALLSYMS in this chapter to debug an "oops" message using gdb and to kprobe a kernel module. This option lives under General setup —> Configure Standard Kernel Features (for small systems) in the configuration menu.

Kernel hacking options result in overhead and increased footprint, so don't leave them on in production-level kernels.