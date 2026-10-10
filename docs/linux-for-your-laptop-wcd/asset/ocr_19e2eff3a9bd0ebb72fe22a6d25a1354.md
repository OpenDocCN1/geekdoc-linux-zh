You can then insert the **password=** entry, along with an unencrypted password. (Hint: Don't use the same password that you use to log in to Linux!) For example:

```
"""
image=/boot/vmlinux
  label=linux
  password=abcd
  initrd=/boot/initrd
"""
```

Make your changes and save the file (press **Ctrl+X** if using **pico**). You must then run **lilo** to write the new boot loader, like this:

```
# /sbin/lilo
```

The next time you reboot, you'll see the **LILO** prompt:

```
LILO boot:
```

Press **Enter**, and you'll see this:

```
Password:
```

Enter your password and press **Enter** to boot. (Super Hint: You can assign a different password to each operating system boot section configured in **/etc/lilo.conf**! If you have enabled your notebook's BIOS startup password, this means that three passwords might be required to use Linux!)

One potential problem with booting can happen if you install Linux and then install another operating system, such as Windows. Other operating systems typically wipe out the MBR of your notebook's hard drive, and LILO will disappear, potentially rendering you unable to boot to Linux. The best approach is to install LILO after all other operating systems have been installed on your notebook. This includes the BSDs, BeOS, and OS/2.

LILO can also help you install Red Hat Linux on notebooks with troublesome IDE controllers. The LILO boot prompt can be used to pass messages, or arguments, to the Linux kernel. For example, experienced IBM ThinkPad 600x (and perhaps 570) users would use this:

```
linux hda=1558,240,63 hdc=cdrom
```

at the LILO boot: prompt to enable Linux to recognize the internal hard drive and CD-ROM drive (if available). The **hda=** entry specifies the device name of the hard drive (**/dev/hda**) and provides settings inscribed on the drive. These settings represent the number of cylinders, sectors, and heads in the hard drive. These op-