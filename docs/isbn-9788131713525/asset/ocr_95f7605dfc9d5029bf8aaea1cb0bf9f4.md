to load register $r25$. (Remember, `klimit` is a pointer, and we are interested in the value that `klimit` points to). Register $r25$ now holds the pointer that was stored in the variable `klimit`. In the final line of Listing 16-9, you subtract the kernel's linked base address (`KERNELBASE`) from $r25$ to adjust the pointer to our actual physical address. In C, it would look like this:

```
```
unsigned int *tmp;            /* represents r25 */
tmp = *klimit;
tmp -= KERNELBASE;
```
```

In summary, we referenced a pointer stored in `klimit` and adjusted its value to our real (physical) address so we can use its contents. When the kernel enables the MMU and virtual addressing, we no longer have to worry about this—the kernel will be running at the address where it was linked, regardless of where in physical memory it is actually located.

# ### 16.3.2 Board Information Structure

Many bootloaders are used for PowerPC platforms, but there is still no unified way to pass in board-specific data such as serial port baud rate, memory size, and other low-level hardware parameters that the bootloader has configured. The platform-initialization file from Listing 16-8 supports two different methods; data stored as `struct bi_record` and data stored as `struct bd_info`.⁸ Both methods provide similar results: hardware-specific data is passed from the bootloader to the kernel in these structures.

From Listing 16-8, here is the code snippet that saves the bootloader-supplied hardware configuration:

```
```
struct bi_record *bootinfo = find_bootinfo();

if (bootinfo)
    parse_bootinfo(bootinfo);
else {
    /* Load the bd_t board info structure */
    if (r3)
        memcpy((void*)&_res, (void*)(r3+KERNELBASE),
               sizeof(bd_t));
```
```

⁸ Each method has its own roots. The struct `bd_info` originated in U-Boot, and struct `bi_record` was an attempt to unify across all platforms. Both are supported by many platforms.