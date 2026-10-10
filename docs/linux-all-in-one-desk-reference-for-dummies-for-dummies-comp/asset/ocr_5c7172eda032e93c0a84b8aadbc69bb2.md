# 492 Installing the Modules

The **make** command creates the new kernel as well as any modules that you have specified through the configuration step.

![](bbox=[0.13, 0.18, 0.24, 0.27])

As the kernel is built, you see a lot of messages on-screen. When it’s all over, a new kernel in the form of a compressed file named **bzImage** is in the **arch/i386/boot** subdirectory of where the kernel sources are located.

To use the new kernel, you have to copy the kernel file and the **System.map** file to the **/boot** directory under a specific name and edit the **GRUB** menu to set up GRUB — the boot loader. Before you proceed with the kernel installation, however, you have to install the modules and build a new initial RAM disk.

# ## Installing the Modules

If you select any modules during the kernel configuration, the kernel-building step also builds the modules. All you have to do is install them. Perform this task with the following commands:

```
```bash
cd /usr/src/linux*
make modules_install
```
```

The **make modules_install** command copies all the modules to a new subdirectory in the **/lib/modules** directory. The subdirectory name should be the same as the kernel version number.

Now you can install the kernel and make it available for GRUB to boot.

# ## Creating the Initial RAM Disk File

The new kernel needs a new initial RAM disk file that you can create by using the **mkinitrd** command. Usually, the initial RAM disk image is stored in a file whose name begins with **initrd**. As you might have guessed, **initrd** is shorthand for initial RAM disk, and the **mkinitrd** command is so named because it makes an **initrd** file.

The **mkinitrd** program is in the **/sbin** directory, and you have to log in as **root** and use a command line of the following form to create the **initrd** file:

```
```bash
/sbin/mkinitrd /boot/initrd-filename.img module-directory
```
```

The **initrd** file has to be in the **/boot** directory where the kernel is also located. You can use any filename for *initrd-filename*. The *module-directory* is the name of the directory in **/lib/modules** where the module files for the new kernel are located. The **make modules_install** step places the modules in a directory whose name is the kernel version