Protect your system

During Red Hat Linux installation, you should have created an emergency boot disk. This floppy disk allows you to boot your Linux system in case the new kernel doesn't boot or in case your grub.conf file doesn't work (so that the boot loader fails). If you did not create one, or if you can't find it, insert a blank floppy disk in the first floppy drive and type the following:

```
# mkbootdisk --device /dev/fd0 2.4.18-0.13
```

Replace the number 2.4.18-0.13 with the version number of your kernel. Press Enter to continue, as prompted.

Setting up the configuration

To begin reconfiguring the kernel, you should be in a bash shell. (If you are not sure, type bash at the command line.) Then go to the /usr/src/linux-2.4* directory and type:

```
# make mrproper
```

This prepares you to create the new kernel configuration. It thoroughly cleans up the kernel configuration directories.

Making the configuration

To choose the kernel options that you want, you must run make with the config, menuconfig, or xconfig options. By far, the easiest option is xconfig, though it requires that you run an X desktop (such as GNOME or KDE). Here is an example:

```
# make xconfig
```

If you are not running X, you can use config or menuconfig. Using make config presents you with a pure text-based, question-and-answer way of rebuilding your kernel. Typing make menuconfig from /usr/src/linux* provides a menu-driven interface (which runs in a character terminal).

Besides being a bit nicer to look at, the menuconfig and xconfig kernel configuration tools enable you to select only those areas of the kernel that you want to change. With make config, you have to step through each category. With the xconfig tool, you see all selections available in a category, though if a category is turned off, selections within that category are grayed out. Also, if you make a mistake, just select the category again.

Checking for dependencies

When you are done configuring the kernel, save the changes. After you have made the kernel configuration changes that you want, you have to go back to the /usr/src/linux* directory and type the following:

```
# make dep
```