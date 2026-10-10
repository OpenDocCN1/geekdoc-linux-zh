
In Listing 16-3, we listed the functions in the `lite5200.c` platform-initialization file. Every function except `platform_init()` is declared as static. Therefore, as shown in Figure 16-3, this is the entry point for the platform-initialization file. The rest of the functions in the file are referenced only from within the file itself.

Let's examine the entry function `platform_init()`. Listing 16-8 reproduces the `platform_init()` function from the `lite5200.c` file.

# Listing 16-8

## Lite5200 platform_init Function

```c
void __init
platform_init(unsigned long r3, unsigned long r4,
           unsigned long r5, unsigned long r6,
           unsigned long r7)
{
  /* Generic MPC52xx platform initialization */
  /* TODO Create one and move a max of stuff in it.
     Put this init in the syslib */

  struct bi_record *bootinfo = find_bootinfo();

  if (bootinfo)
    parse_bootinfo(bootinfo);
  else {
    /* Load the bd_t board info structure */
    if (r3)
      memcpy((void*)&__res, (void*)(r3+KERNELBASE),
             sizeof(bd_t));

    #ifdef CONFIG_BLK_DEV_INITRD
    /* Load the initrd */
    if (r4) {
      initrd_start = r4 + KERNELBASE;
      initrd_end = r5 + KERNELBASE;
    }
    #endif

    /* Load the command line */
    if (r6) {
      *(char *)(r7+KERNELBASE) = 0;
      strcpy(cmd_line, (char *)(r6+KERNELBASE));
    }
  }

  /* PPC Sys identification */
  identify_ppc_sys_by_id(mfspr(SPRN_SVR));

  /* BAT setup */
  mpc52xx_set_bat();

  /* No ISA bus by default */
  isa_io_base         = 0;
  isa_mem_base        = 0;

  /* Powersave */
  /* This is provided as an example on how to do it.  But you
   * need to be aware that NAP disable bus snoop and that may
   * be required for some devices to work properly, like USB
   *... */
  /* powersave_nap = 1; */

  /* Setup the ppc_md struct */
  ppc_md.setup_arch = lite5200_setup_arch;
  ppc_md.show_cpuinfo = lite5200_show_cpuinfo;
  ppc_md.show_percpuinfo = NULL;
  ppc_md.init_IRQ       = mpc52xx_init_irq;
  ppc_md.get_irq       = mpc52xx_get_irq;

  #ifdef CONFIG_PCI
  ppc_md.pci_map_irq = lite5200_map_irq;
  #endif

  ppc_md.find_end_of_memory = mpc52xx_find_end_of_memory;
  ppc_md.setup_io_mappings = mpc52xx_map_io;

  ppc_md.restart   = mpc52xx_restart;
  ppc_md.power_off = mpc52xx_power_off;
  ppc_md.halt      = mpc52xx_halt;

  /* No time keeper on the LITE5200 */
  ppc_md.time_init    = NULL;
  ppc_md.get_rtc_time = NULL;
  ppc_md.set_rtc_time = NULL;

  ppc_md.calibrate_decr   = mpc52xx_calibrate_decr;
  #ifdef CONFIG_SERIAL_TEXT_DEBUG
  ppc_md.progress          = mpc52xx_progress;
  #endif
}
```

This function contains much of the customizing that is required for this particular platform. It starts by searching for board-specific data supplied by the boot-loader. We defer discussion of the details of this until Section 16.3.2, "Board Information Structure."

Following this, if your kernel is configured for an initial ramdisk (initrd), the start and end addresses of the ramdisk image are saved. Notice that they are passed in the PowerPC general-purpose registers r4 and r5 by convention. It is the bootloader’s responsibility to pass the initrd addresses in these registers. Later, the kernel will use these addresses to load the initrd image from raw memory (where the bootloader placed it, or a nonvolatile Flash image) into an internal kernel ramdisk structure.

Next we see code to store the kernel command line, whose address is passed into `platform_init()` via registers r6 and r7, marking the start and end addresses, respectively. This differs from the method described earlier for storing a static kernel command line in one specific detail: this kernel command line was passed to `platform_init()` from the bootloader, as opposed to being compiled into the kernel.

Copying the initrd and kernel command line is very straightforward. Basically, the registers passed in from the bootloader contain the memory addresses where these data structures reside. There is one minor subtlety, however. You may have already wondered about the purpose of the constant `KERNELBASE`. Understanding this is key to grasping one of the more complex parts of the boot sequence.

The addresses the bootloader provides are physical addresses. This means they are the real hardware addresses where the data resides in the memory chips. The bootloader typically operates without support for virtual memory. However, the kernel itself is statically linked to a well-known, user-configured base address. This address is `KERNELBASE`. (The value itself is not relevant to the discussion—it is user-configurable but virtually never changed from its default value of 0xC0000000.)

This sets up an interesting situation in `head.S`. When the kernel is decompressed and relocated to RAM (usually to location 0), all of its code and data symbols are linked at the kernel’s virtual address, `KERNELBASE`. This can be seen by examining the kernel symbol map file, produced during the kernel build process, `System.map`. However, the execution context prior to enabling the MMU is such that physical addresses are real hardware addresses. This means that all the code prior to enabling the MMU and virtual memory mapping must be relocatable, and access to symbols must be fixed up. This involves adding an offset to the symbol’s address to access it. An example will make this clear.

- The initial ramdisk, or initrd, was introduced in Chapter 6.
- We introduced the `System.map` file in Chapter 4.

### 16.3.1 Early Variable Access

Let’s assume that a code segment very early in the boot process needs to access the variable `cmd_line`—so early that we’re executing in 1:1 real to physical mapping. As pointed out earlier, this variable is defined in `head.S` and will end up in the .data section when the kernel is linked. From the Linux kernel’s `System.map` file, you can find the linked addresses for `cmd_line`:

```bash
$ cat System.map | grep cmd_line
c0150000 D cmd_line
```

If we were running in real = physical mode (MMU disabled) and accessed this variable using its symbol, we would be trying to read or write to an address greater than 3GB. Most smaller embedded systems don’t have any RAM in this region, and the results would be undefined or would result in a crash. Even if we had physical RAM at that address, it is unlikely that it would be mapped and accessible this early in the boot process. So we have to adjust our reference to this variable to access it.

Listing 16-9 reproduces a code snippet from `head.S` that does just that.

# Listing 16-9

## Variable Reference Fixup

```assembly
relocate_kernel:
addis r9,r26,klimit@ha /* fetch klimit */
lwz r25,klimit@l(r9)
addis r25,r25,-KERNELBASE8h
```

This code snippet from the PowerPC `head.S` is a good example of the issue we are describing. The variable `klimit` represents the end of the kernel image. It is defined elsewhere as `char *klimit`. Therefore, it is a pointer—it is an address that contains an address. In Listing 16-9, we fetch the address of `klimit`, sum it with a previously calculated offset that is passed in r26, and deposit the resulting value in register r9. Register r9 now contains the high-order 16 bits of the adjusted address of `klimit`, with the low-order bits zeroed. It was adjusted by the offset value previously calculated and passed in register r26.

In the next line, the `lwz` instruction uses register r9 together with the offset of `klimit` (the lower 16 bits of the `klimit` address) as an effective address from which to load register r25. (Remember, `klimit` is a pointer, and we are interested in the value that `klimit` points to). Register r25 now holds the pointer that was stored in the variable `klimit`. In the final line of Listing 16-9, you subtract the kernel's linked base address (`KERNELBASE`) from r25 to adjust the pointer to our actual physical address. In C, it would look like this:

```c
unsigned int *tmp;            /* represents r25 */
tmp = *klimit;
tmp -= KERNELBASE;
```

In summary, we referenced a pointer stored in `klimit` and adjusted its value to our real (physical) address so we can use its contents. When the kernel enables the MMU and virtual addressing, we no longer have to worry about this—the kernel will be running at the address where it was linked, regardless of where in physical memory it is actually located.

### 16.3.2 Board Information Structure

Many bootloaders are used for PowerPC platforms, but there is still no unified way to pass in board-specific data such as serial port baud rate, memory size, and other low-level hardware parameters that the bootloader has configured. The platform-initialization file from Listing 16-8 supports two different methods; data stored as `struct bi_record` and data stored as `struct bd_info`. Both methods provide similar results: hardware-specific data is passed from the bootloader to the kernel in these structures.

From Listing 16-8, here is the code snippet that saves the bootloader-supplied hardware configuration:

```c
struct bi_record *bootinfo = find_bootinfo();

if (bootinfo)
    parse_bootinfo(bootinfo);
else {
    /* Load the bd_t board info structure */
    if (r3)
        memcpy((void*)&__res, (void*)(r3+KERNELBASE),
               sizeof(bd_t));
```

- Each method has its own roots. The struct `bd_info` originated in U-Boot, and struct `bi_record` was an attempt to unify across all platforms. Both are supported by many platforms.
