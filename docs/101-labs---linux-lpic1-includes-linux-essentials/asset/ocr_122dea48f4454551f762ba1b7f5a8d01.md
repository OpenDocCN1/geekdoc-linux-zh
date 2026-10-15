
## Task 2

Upon boot, you should be greeted with a GRUB menu. Hit `c` to enter the GRUB prompt. Here, you can run various bootloader commands. Use `ls` to explore your partitions; the format looks a bit different, for example, `(hd0,msdos1)`. There are also commands like `lsmod`, `lspci`, and `parttool`. Do these look familiar? Run `help` for a full list.

Then, hit `ESC` to return to the boot menu.

## Task 3

Back at the boot menu, hit `e` to enter a screen where you can modify the boot commands. Depending on your implementation, there may be a lot here, but you are looking for a line beginning with `linux*`. This is the line that loads the Linux kernel, and is the most commonly modified line for editing boot options.

At the end of that line, append `libata.force=[number]:disable`, where `[number]` is the number you noted above, such as `3.00`.

Now, hit `Ctrl+X` to boot your computer.

## Task 4

After a couple of minutes, you may notice that something has gone wrong! You have disabled your primary hard disk, causing Linux to be unable to boot. It may have looked like it was booting initially, though. That’s because the next step of the boot process is to load the initial RAM disk (`initrd`), prior to loading the kernel. The `initrd` was successful whereas the kernel step failed, which is why you should have ended up at a `(initramfs)` prompt.

In short, the Linux boot process goes like this:

1. BIOS/UEFI enumerates hardware and loads code from the configured boot device (not Linux-specific).
2. GRUB bootloader loads, parses boot commands and options.
3. `initrd` is loaded, bootstraps various filesystems and modules, and then loads the kernel.
4. The `init` process is launched, which in turn executes all startup processes as configured within Linux.

Type `reboot` to reboot your computer/VM and return it to normalcy.
