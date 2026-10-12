# Installing the Modules

If you select any modules during the kernel configuration, the kernel building step also builds the modules. All you have to do is install them. Perform this task with the following commands:

```
```
cd /usr/src/linux*
make modules_install
```
```

The **make modules_install** command copies all the modules to a new subdirectory named **2.6.3-2.1.240custom** in the **/lib/modules** directory. Appending the word **custom** to the kernel version number creates the directory name.

Now you can install the kernel and make it available for GRUB to boot.

# Creating the Initial RAM Disk File

The new kernel needs a new initial RAM disk file that you can create by using the **mkinitrd** command. Usually, the initial RAM disk image is stored in a file whose name begins with **initrd**. As you might have guessed, **initrd** is shorthand for **initial RAM disk**, and the **mkinitrd** command is so named because it makes an **initrd** file.

The **mkinitrd** program is in the **/sbin** directory, and you have to **log in** as **root** and use a command line of the following form to create the **initrd** file:

```
```
/sbin/mkinitrd /boot/initrd-filename.img module-directory
```
```

The **initrd** file has to be in the **/boot** directory where the kernel is also located. You can use any filename for **initrd-filename**. The **module-directory** is the name of the directory in **/lib/modules** where the module files for the new kernel are located. The **make modules_install** step places the modules in a directory whose name is the kernel version number with the word **custom** appended to it. For example, if your kernel version (as reported by the **uname -r** command) is **2.6.3-2.1.240**, the **module-directory**, after the **make modules_install** step, is **2.6.3-2.1.240custom**.

Another common practice is to use an **initrd** filename created by appending the module directory name to the **initrd-** prefix. Thus, for module directory **2.6.3-2.1.240custom**, the **initrd** file is **initrd-2.6.3-2.1.240custom.img**.

To create the initial RAM disk image for the newly built kernel, type the following command:

```
```
/sbin/mkinitrd /boot/initrd-2.6.3-2.1.240custom.img 2.6.3-2.1.240custom
```
```