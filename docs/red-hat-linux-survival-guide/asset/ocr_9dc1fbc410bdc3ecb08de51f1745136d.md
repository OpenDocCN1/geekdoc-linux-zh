+   5. Now you need to copy the new kernel to the /boot directory as follows:
+   ```
+   cp /usr/src/linux-2.x.x/arch/i386/boot/bzImage /boot/vmlinuz-2.x.x
+   ```
+   6. Also copy and rename the new System.map file to the /boot directory as follows:
+   ```
+   cp /usr/src/linux-2.x.x/System.map /boot/System.map-2.x.x
+   ```
+   7. Now remove the existing symbolic link for System.map as follows:
+   ```
+   rm -f /boot/System.map
+   ```
+   8. Finally, create a new symbolic link called /boot/System.map as follows:
+   ```
+   ln -s /boot/System.map-2.x.x /boot/System.map
+   ```
+   9. You also need to create a new initial ramdisk as follows:
+   ```
+   mkinitrd /boot/initrd-2.x.x.img 2.x.x
+   ```
+   10. The final step before you boot the new kernel is to prepare LILO for the new kernel. See the “Configuring LILO” section earlier in this chapter for details on how you can create a new configuration segment in /etc/lilo.conf for the new kernel. After you have modified the /etc/lilo.conf file and have run /sbin/lilo, you can reboot the system and attempt to use the new kernel, as discussed in the “Booting with the new kernel” section earlier in this chapter.

If all things go well, you have a fresh, new, custom-configured kernel running all of your favorite Linux applications from now on.

![](bbox=[0.07, 0.83, 0.18, 0.92])

Do not forget to make a new boot floppy using the mkbootdisk --device /dev/fd0 2.x.x command.

# Patching a Kernel

You are likely to encounter situations when the entire kernel code does not change, only the small pieces. In such a case you need to know how to patch your kernel source and create a new kernel. It is not uncommon to