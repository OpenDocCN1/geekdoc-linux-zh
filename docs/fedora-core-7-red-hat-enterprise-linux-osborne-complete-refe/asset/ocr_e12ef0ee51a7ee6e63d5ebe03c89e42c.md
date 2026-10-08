You can now install the kernel. As a safety precaution, you should preserve your old kernel in case the new one does not work out for some reason. This involves installing with the `install` (-1) option instead of the `update` (-U) option, creating a separate RAM disk for the new kernel, and then modifying **grub.conf** to have GRUB start up using the new kernel.

```
# rpm -ivh kernel-2.6.version.i686.rpm
```

If your system has a SCSI controller or any other specialized hardware, RPM will also create a RAM disk to hold appropriate support modules (you can create a RAM disk manually with the **mkinitrd** command). The RAM disk is named **initrd-kernel-version.img** and is located in the **/boot** directory, as in **/boot/initrd-2.6.version.img**.

On most distributions, kernels are installed in the **/boot** directory. Performing an **ls -1** operation on this directory lists all the currently installed kernels. A file for your old kernel and a file for your new one now exist. If you took the precautions described in the preceding section, you may have already renamed the older kernel. If you are using a boot loader such as GRUB, you need not change its configuration file (**/boot/grub.conf**) to add the entry to invoke the new kernel. The kernel boots using the selected **/boot/vmlinuz-version** kernel file. In your **grub.conf** file, you need a kernel line to reference this kernel file. You also need to include a line for the RAM disk, **initrd**.

```
kernel /boot/vmlinuz-version ro root=/dev/hda3
initrd /boot/initrd-version.img
```

> **Tip** *Although it is not included with Fedora, user-mode Linux (UML) is an optional version of the kernel designed to run as a stand-alone program separate from the kernel. In effect, it creates a virtual machine with disk storage complemented on a user file. UML is often used to test software or experiment with kernel configurations, without harming the real system. You can also use UML to implement virtual hosting, by running several virtual machines on one physical host. With a virtual machine, you can control the access to the host system, providing greater security. You can find out more about user-mode Linux at user-mode-linux.sourceforge.net.*

# Precautionary Steps for Modifying a Kernel of the Same Version

If you want to modify your kernel configuration and build a new one, you should retain a copy of your current kernel. In case something goes wrong with your modified version, you can always boot from the copy you kept. You do not have to worry about this happening if you are installing a new version of the kernel. New kernels are given different names, so the older one is not overwritten.

To retain a copy of your current kernel, you can make a backup copy of it, letting the original be overwritten. An installed version of a kernel makes use of several files in the **/boot** directory. Each file ends with that kernel version’s number. These include the **vmlinuz** file, which is the actual kernel image file, along with several support files, **System.map, config,** and **initrd.** This **System.map** file contains kernel symbols needed by modules to start kernel functions. For example, the kernel image file is called **vmlinuz-version**, where **version** is the