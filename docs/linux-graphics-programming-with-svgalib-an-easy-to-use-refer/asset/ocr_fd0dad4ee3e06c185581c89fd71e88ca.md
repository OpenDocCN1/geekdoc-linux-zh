able, or being ready for new write data, or being in an exceptional condition (urgent data arriving on a TCP stream), set the corresponding bits in the `fd_set` structures passed (see `select()`). On a W32 `vga_waitevent()` to return after a timeout value, it has a `struct timeval` with the desired value. If you're not interested in the corresponding events, you may pass `NULL` for any of the pointers.

If `NULL` is passed for timeout, `vga_waitevent()` will not time out but block until any of the other events occur. If the integer returned is a < 0, an error has occurred. Check the global variable `errno` for details. If a value >= 0 is returned, it is a bitmask constructed using `VGA_MOUSEEVENT` and `VGA_KEYEVENT` to show which of these events has occurred.

If any of these two occurred, the appropriate update functions are already called by `vga_waitevent()`. `vga_waitevent()` operates in raw as well as non-raw keyboard mode. In the latter case, use `vga_getch()` and not `vga_getkey()` to read the newly arrived keys.

Any of the file related conditions being met will be signalled by setting exactly the bits for files that met the conditions in the corresponding `fd_set` structures. If a non-`NULL` timeout is passed the remaining time is written into it on return. If it is 0 a timeout occurred (again: cf. `select()`). Therefore, depending on context, `vga_waitkey()` may return 0 if only special, non-SVGA/lib, events occurred.

# Direct VGA Memory Access

These functions are in regard to direct VGA memory access:

#### `void vga_setpage(int page)`

Usually, SVGA cards have more than 64K of memory, which suffices for an ordinary VGA card. However, the memory window mapped at `vga_getgraphmem()` is only 64K large. `vga_setpage()` selects the page—that is, the 64K memory chunk—to be visible at position `vga_getgraphmem()`. The fun() and vgtest() demos show the basic use of this function.

#### `void vga_setreadpage(int page)`

Usually, SVGA cards have more than 64K of memory, which suffices for an ordinary VGA card. However, the memory window mapped at `vga_getgraphmem()` is only 64K. Therefore, `vga_setreadpage()` selects the page—that is, the 64K memory chunk—to be visible for reads at position `vga_getgraphmem()`.