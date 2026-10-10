```
lrwxrwxrwx 1 root root 10 nov 4 08:40 ae71b214-0aec-48e8-80b2-090b6986b625 -> ../../sda1
```

In the example above, the UUID for /dev/sda1 is `ae71b214-0aec-48e8-80b2-090b6986b625`. Should you wish to set it as the root device for GRUB 2, the command would be `search --set=root --fs-uuid ae71b214-0aec-48e8-80b2-090b6986b625`.

When using the `search` command it is common to add the `--no-floppy` parameter so GRUB will not waste time searching on floppy disks.

The `linux` line indicates where the kernel for the operating system is located (in this case, the `vmlinuz` file at the root of the file system). After that, you can pass command line parameters to the kernel.

In the example above we specified the root partition (`root=/dev/sda1`) and passed three kernel parameters: the root partition should be mounted read-only (`ro`), most of the log messages should be disabled (`quiet`) and a splash screen should be shown (`splash`).

The `initrd` line indicates where the initial RAM disk is located. In the example above the file is `initrd.img`, located at the root of the file system.

Most Linux distributions do not actually put the kernel and initrd at the root directory of the root file system. Instead, these are links to the actual files inside the `/boot` directory or partition.

The last line of a menu entry should contain only the character `}`.

# Interacting with GRUB 2

When booting a system with GRUB 2 you will see a menu of options. Use the arrow keys to select an option and `Enter` to confirm and boot the selected entry.

If you see just a countdown, but not a menu, press `Shift` to bring up the menu.

To edit an option, select it with the arrow keys and press `E`. This will show an editor window with the contents of the `menuentry` associated with that option, as defined in `/boot/grub/grub.cfg`.

After editing an option, type `ctrl` + `X` or `F10` to boot, or `Esc` to return to the menu.

To enter the GRUB 2 shell, press `c` on the menu screen (or `ctrl` + `C` on the editing window). You will see a command prompt like this: `grub >`

Type `help` to see a list of all available commands, or press `Esc` to exit the shell and return to the menu screen.