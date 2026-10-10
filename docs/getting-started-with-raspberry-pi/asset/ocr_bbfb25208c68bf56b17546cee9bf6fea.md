```
Code View:
struct e820map e820;

static int __init
copy_e820_map(struct e820entry *biosmap, int nr_map)
{
    int x;
    /* ... */

do {
    /* Copy memory map information collected from
       the BIOS into local variables */
    unsigned long long start = biosmap->addr;
    unsigned long long size = biosmap->size;
    unsigned long long end = start + size;
    unsigned long long type = biosmap->type;

    /* Sanitize start and size */
    /* ... */

    /* Populate the kernel data structure, e820 */
    x = e820.nr_map;
    e820.map[x].addr = start;
    e820.map[x].size = size;
    e820.map[x].type = type;
    e820.nr_map++;
} while (biosmap++, --nr_map);  /*Do for all elements in map*/

    /* ... */
}
```

Look at `arch/x86/mm/init_32.c` to see how the `e820` structure populated in Listing B.2 is used later on in the boot process.

![](bbox=[0.33, 0.605, 0.81, 0.62])

Starting with the 2.6.23 kernel, the i386 boot assembly code has been largely rewritten in C. Prior to 2.6.23, the code in Listing B.1 lived in `arch/i386/boot/setup.S` rather than in `arch/x86/boot/memory.c`. Also, the switch to protected mode now occurs in `arch/x86/boot/pm.c` rather than `setup.S`.

To take another example, the kernel makes use of the BIOS `int 0x10` service to obtain video mode parameters while it’s in real mode (`arch/x86/boot/video*.c`). The VESA frame buffer driver (`drivers/video/vesafb.c`) relies on these parameters to turn on graphics mode at boot time.

As an exercise, use a similar approach to obtain BIOS *Power-On Self Test* (POST) error codes from the real mode kernel (via `int 0x15`, function `0x2100`) and display them during normal operation via the `/proc` filesystem.

Bootloaders also make use of BIOS services in real mode. If you browse through the sources of LILO, GRUB, or SYSLINUX, you will see a liberal sprinkling of `int 0x13` calls to read the kernel image from the boot device.