
## 16.2.2 Customizing Kernel Initialization

Now that we have a baseline kernel source tree from which to start, let’s determine where to begin customizing for our particular board. We discovered that for the PowerPC architecture, the board-specific files reside in a directory called .../arch/ppc/platforms. Of course, this is not strictly necessary, but if you ever intend to submit your patches to the Linux kernel development community for consideration, proper form and consistency matter!

We find in the platforms directory a file called lite5200.c. It’s a fairly simple file, containing two data structures and five functions. Listing 16-3 presents the functions from this file.

### **Listing 16-3**
**Functions from 5200 Platform File**

```
lite5200_show_cpuinfo() /* Prints user specified text string */
lite5200_map_irq() /* Sets h/w specific INT logic routing */
lite5200_setup_cpu() /* CPU specific initialization */
lite5200_setup_arch() /* Arch. specific initialization */
platform_init() /* Machine or board specific init */
```

Let’s look at how these functions are used. We briefly examined the low-level kernel initialization in Chapter 5. Here we look at the details for a particular architecture. Details differ between architectures, but when you can navigate one, the others will be easier to learn.

From Chapter 5, we saw the early flow of control on power-up. The bootloader passed control to the kernel’s bootstrap loader, which then passed control to the Linux kernel via the kernel’s head.o module. Here the platform-specific initialization begins. Listing 16-4 reproduces the pertinent lines from .../arch/ppc/kernel/head.S.

### **Listing 16-4**
**Calling Early Machine Initialization**

```
...
/*
 * Do early bootinfo parsing, platform-specific initialization,
 * and set up the MMU.
 */
    mr r3,r31
    mr r4,r30
    mr r5,r29
    mr r6,r28
    mr r7,r27
    bl    machine_init
    bl    MMU_init
...
```

Here you can see the assembly language call to machine_init. Of particular significance is the setup of the registers r3 through r7. These registers are expected to contain well-known values, which you will see momentarily. They were stored away very early in the boot sequence to the PowerPC general-purpose registers r27 through r31. Here they are reloaded from these stored values.

The machine_init() function is defined in a C file called setup.c, in the same architecture-specific kernel directory: .../arch/ppc/kernel/setup.c. The start of this routine is reproduced here in Listing 16-5.

### **Listing 16-5**
**Function machine_init() in setup.c**

```c
void __init
machine_init(unsigned long r3, unsigned long r4, unsigned long r5,
             unsigned long r6, unsigned long r7)
{
#define CONFIG_CMDLINE
    strcpy(cmd_line, CONFIG_CMDLINE, sizeof(cmd_line));
#undef /* CONFIG_CMDLINE */

#ifdef CONFIG_6xx
    ppc_md.power_save = ppc6x_idle;
#endif
#ifdef CONFIG_POWER4
    ppc_md.power_save = power4_idle;
#endif

    platform_init(r3, r4, r5, r6, r7);

    if (ppc_md.progress)
        ppc_md.progress("id mach(): done", 0x200);
}
```

There is some very useful knowledge in this simple function. First, notice that the parameters to machine_init() represent the PowerPC general-purpose registers r3 through r7.² You saw that they were initialized just before the machine language call to machine_init(). As you can see from Listing 16-5, these register values are passed unmodified to platform_init(). We need to modify this function for our platform. (We have more to say about that in a moment.)

² By convention, parameters in C are passed in these PowerPC registers.

Listing 16-5 also contains some machine-specific calls for power-management functions. If your kernel is configured for PowerPC 6xx support (CONFIG_6xx defined in your .config file), a pointer to a machine-specific power-management function (ppc6xx_idle) is stored in a structure. Similarly, if your kernel is configured for a PowerPC G5 core (CONFIG_POWER4), a pointer to its machine-specific power-management routine is stored in the same structure member. This structure is described in Section 16.3.3, "Machine-Dependent Calls."

## 16.2.3 Static Kernel Command Line

One of the more interesting operations in the machine_init() function reproduced in Listing 16-5 is to store the default kernel command line. This operation is enabled if CONFIG_CMDLINE is enabled in your kernel configuration. On some platforms, the bootloader does not supply the kernel command line. In these cases, the kernel command line can be statically compiled into the kernel. Figure 16-2 illustrates the configuration options for this.

![](img/7a1144833e62564667e7dd9eb4c9f03d_460_0.png)

### FIGURE 16-2
Default kernel command line

Enable “Default bootloader kernel arguments” in the configuration in Figure 16-2 and edit the “Initial kernel command string” as shown. This results in a set of entries in the `.config` file, as shown in Listing 16-6.

### **Listing 16-6**
**Configuration for Default Kernel Command Line**

```
...
CONFIG_CMDLINE_BOOL=y
CONFIG_CMDLINE="console=ttyS0 root=/dev/ram0 rw"
...
```

The ellipses in Listing 16-6 indicate that we have taken only a small snippet of the `.config` file. When these configuration symbols are processed by the kernel build system, they become entries in the `.../include/linux/autoconf.h` file, as detailed in Listing 16-7.

### **Listing 16-7**
**File autoconf.h Entries for Default Kernel Command Line**

```
...
#define CONFIG_CMDLINE_BOOL 1
#define CONFIG_CMDLINE "console=ttyS0 root=/dev/ram0 rw"
...
```

Now referring back to Listing 16-5, we have the following line:

```c
strcpy(cmd_line, CONFIG_CMDLINE, sizeof(cmd_line));
```

You can see that this kernel-based string-copy function copies the string defined by CONFIG_CMDLINE into a global kernel variable called cmd_line. This is important because many functions and device drivers might need to examine the kernel command line early in the boot sequence. The global variable cmd_line is hidden away at the start of the .data section, defined in the assembler file `.../arch/ppc/kernel/head.S`.

A subtle detail is worth mentioning here. Looking back at Listing 16-4, we see that the machine_init assembly language call is made *before* the call to MMU_init. That means that any code we are able to run from machine_init is executed in a context with limited support for accessing memory. Many of today’s processors that contain an MMU cannot access any memory without some initial mapping via hardware registers in the processor.³ Typically, a small amount of memory is made available at boot time to accommodate loading and decompressing the kernel and a ramdisk image. Trying to access code or data beyond these early limits will fail. Each architecture and platform might have different early limits for accessing memory. Values on the order of 8 to 16MB are not untypical. We must remember that any code we execute from machine_init, including our platform initialization, takes place in this context. If you encounter data access errors (PowerPC DSI exception⁴) while debugging your new kernel port, you should immediately suspect that you have not properly mapped the memory region your code is trying to access.

³ The AMCC PPC405 is a perfect example of this. The interested reader is encouraged to examine the BAT registers in this processor.

⁴ Refer to the Programming Environments Manual referenced at the end of this chapter for details of the PowerPC DSI exception.

## 16.3 Platform Initialization

Following is a quick review of the code flow during early initialization. Figure 16-3 shows the flow of execution from the bootloader or bootstrap loader to your platform-initialization code.

From bootloader

![](img/7a1144833e62564667e7dd9eb4c9f03d_462_0.png)

### FIGURE 16-3
Platform initialization flow of control

The files head.S and setup.c are both found in the .../arch/ppc/kernel directory for the PowerPC architecture. Our custom platform-initialization file will be placed in the .../arch/ppc/platforms directory. In Figure 16-3, it is represented by the file myplat.c. We are now in a position to examine the platform-specific initialization file in detail.
