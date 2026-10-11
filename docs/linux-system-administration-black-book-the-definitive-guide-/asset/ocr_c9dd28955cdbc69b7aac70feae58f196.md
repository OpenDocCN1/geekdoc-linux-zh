8. Type “make dep” to build a list of source dependencies. See Chapter 22 for more on working with C source code.

> *NOTE:* *Keep in mind that although each of these make steps is short to read, they can take several minutes or longer, depending on your CPU’s speed.*

+   9. Type “make clean” to clean out the temporary files used up to this point.
+   10. Type “make bzImage” to compile the base kernel.
+   11. Type “make modules” to compile the modules that the kernel will load on the fly.
+   12. The compiler places the kernel source in the directory /usr/src/linux/arch/i386/boot/bzImage. Copy this file into the /boot directory.
+   13. Rename /boot/bzImage to /boot/vmlinuz-version with the mv command, where version is the new kernel version you are in the process of installing.
+   14. Copy the file /boot/System.map to /boot/System.map-old.
+   15. Copy the file /usr/src/linux/System.map to the /boot directory.
+   16. Type “make modules_install” to install the modules to /lib/modules/version.
+   17. Although not necessary, it is a good policy to create a special boot version of the kernel containing modules that are needed by boot time hardware— for example, if your primary hard drive is SCSI. To do so, use mkinitrd /boot/initrd-version version.
+   18. Proceed to the section “Updating LILO” at the end of the chapter. You will not be able to boot with the new kernel until you tell LILO where to find it.

| Related solutions: | Found on page: |
| :----------------- | :-------------- |
| Opening Or Creating Tarballs | 110 |
| Installing RPMs | 114 |

# ## Configuring The Kernel With config

The config kernel configuration tool is entirely text-based with no bells and whistles. It takes some time to work through the entire configuration process, as config obtains the new kernel configuration by asking questions one at a time. Although an end user probably shouldn’t use this option, it is useful for system administrators to try it a few times just to get a feeling for how many choices they can make if they want to. Rather than provide a sample run-through, which is a