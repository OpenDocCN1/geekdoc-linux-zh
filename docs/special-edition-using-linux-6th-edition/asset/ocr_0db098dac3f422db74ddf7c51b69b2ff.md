> **Caution**
> 
> Caldera has converted to GRUB, and although LILO is available, it has not been configured in a new installation of OpenLinux. You can tell whether your system is using GRUB because you will see the following:
> 
> `stage 1 stage 2`
> 
> flash on the screen just before the graphical boot screen comes up. If you want to continue using GRUB, do not use the `make bzilo` command. Also, do not run lilo, but follow the steps for using GRUB in Chapter 12, “Boot Loaders.”

```
make bzdisk
```

This method performs exactly the same task as the make bzImage method, but after the compilation is complete, it automatically copies the newly built kernel to a floppy disk. This new disk can then be used to boot the system; the new kernel will then be active. This method is typically used to test a kernel with the system on which it was built, or it is used in testing the kernel on other hardware.

> **Note**
> 
> This method can be used to create an emergency boot disk. However, it might not be usable for a different system. The kernel image contains a pointer to the root filesystem from the system it was created on. This pointer must be changed if used on a system whose root filesystem is on a different partition than that of the system where the kernel was built.

```
make bz lilo
```

This is the recommended method of building and installing a new kernel, but you must have lilo prepared ahead of time. This method does not move the associated kernel map file, can overwrite a good kernel, and is wrought with pitfalls, so it is not recommended. However, if after several kernel builds you decide to try this method, it can save you one extra step. This method is exactly like the make bzImage method except that it automatically performs an additional step. After the compilation completes, the newly built kernel is copied to the `/` directory as `vmlinuz` (a backup copy is made of the original `vmlinuz`), and `lilo` is run to reinstall the boot loader (to recognize the new kernel).

```
make modules AND make modules_install
```

The last two commands that complete the actual build process are make modules and make modules_install. The make modules does exactly what it says: It builds the modules that correspond to the kernel you built in the previous step. The make modules_install command moves those modules from within the kernel source tree to `/lib/modules/<kernel-version>/kernel/<module-type>`, the module-type being a category that modules are assigned to, such as block, fs, ipv4, ipv6, misc, net, pcmcia, and so on.