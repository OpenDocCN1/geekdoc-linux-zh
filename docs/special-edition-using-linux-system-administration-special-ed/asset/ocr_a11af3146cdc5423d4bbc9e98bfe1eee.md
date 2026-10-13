# TESTING THE KERNEL WITHOUT USING A BOOT FLOPPY

You can test the newly built kernel without first installing it onto a floppy disk. This can be done using LILO because you can configure LILO to provide booting from alternate kernel images. For instance, if your new kernel is stored at `/usr/src/linux/arch/i386/boot/bzImage`, copy the kernel image to `/boot` with a name such as `vmlinuz-2.2.14`, and append the following lines to the `/etc/lilo.conf` file:

```
image = /boot/vmlinuz-2.2.14
label = linux.new
root = /dev/hda1
```

The image statement specifies the location of the new kernel image. The label statement gives a new name to this image, and the root statement specifies the hard drive partition where the root file system resides. Make sure the root partition you specify correctly matches your system configuration.

> > **Tip**
> > Make sure you copy the new kernel image to `/boot` or `/` with an alternate name like `/boot/vmlinuz-2.2.13` before testing it. If the kernel image is placed in a partition that falls beyond 1023 cylinders, you will not be able to boot the system. This is a limitation of the PC's BIOS, which cannot access disk cylinders beyond 1023 at boot time.

Once the lilo.conf file has been edited, run lilo:

```
# /sbin/lilo
```

When you reboot your system, press Shift when LILO starts and you will see the LILO prompt where you can enter linux.new to boot from the new kernel.

# INSTALLING MODULES

After you have successfully booted up the new kernel either using a boot floppy or using LILO to boot an alternate kernel image, you are ready to install any newly compiled modules.

To install the modules, use the following commands:

```
# cd /usr/src/linux
# mv /lib/modules /lib/modules.old
# make modules_install
```

This will install the module binaries in the `/lib/modules` directory. Note that we have saved our old modules as `/lib/modules.old`. If we discover problems with the new modules we will be able to backtrack to the old kernel and the old modules.