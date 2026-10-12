After you've created the initial ramdisk, you need to modify the /etc/lilo.conf file to configure LILO for the new kernel.

# Configuring LILO

Configuring LILO is critical to your kernel installation, and you must not reboot the system until you have reconfigured LILO as discussed here. Using your favorite text editor, add a new configuration segment such as the following to your /etc/lilo.conf file:

```
image=/boot/vmlinuz-2.x.xx-x
    label=new-linux
    root=/dev/hda1
    initrd=/boot/initrd-2.x.xx-x.img
    read-only
```

Remember to replace 2.x.xx-x with the appropriate kernel version number for both the image= and initrd= lines. The label= line should be set to an arbitrary string of your choice. The root= line should point to your root disk partition. For example, if your current root partition is /dev/sda1, you should make sure the root= line is set to that partition. After you've modified and saved the /etc/lilo.conf file, run the following command:

```
/sbin/lilo
```

This makes LILO read the new configuration file and updates the boot sector of the appropriate root partition. You can use the -v option with the preceding command to make LILO a bit more verbose. After you've run LILO, you're ready to reboot the system.

# Booting with the new kernel

Use the shutdown -r now command to reboot your system as usual. At the LILO prompt, press the Tab key to see your choices. The labels you enter (in the label= lines) for your old and new kernels appear on the screen. Enter the label for your new kernel (in the example in the previous section, this label is new-linux) at the LILO prompt to boot the system with the new kernel.

The next step mostly depends on your facial expression after you tell LILO to start the new kernel. If you find yourself smiling, your new kernel