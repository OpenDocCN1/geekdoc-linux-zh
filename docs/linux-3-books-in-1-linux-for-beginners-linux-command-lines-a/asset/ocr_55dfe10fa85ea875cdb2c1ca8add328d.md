```
gparted /dev/sdb
```

You should now have one partition in your drive which has the Kali Linux image on it. The next thing to do is create another partition in the drive by right-clicking on the drive and selecting the ‘New’ option from the menu. This will appear once you select the partition menu available in the Menu bar. The following are the steps you need to follow, and they may vary depending on the machine you use:

+   - The unallocated space in the drive is greyed out

+   - You should now select the new option from the partition using the drop-down menu

+   - You can specify the size of the drive using a graphical slider

+   - Now, choose the file system and update it to ext4

+   - Select the add option and click on the drop-down menu. You need to select the option to apply all the operations on your system

+   - When you see a prompt, click ok, and the settings will update

You can add a persistence function to the USB drive using the following commands.

```
mkdir /mnt/usb
mount /dev/sdb2 /mnt/usb
echo "/ union" ../mnt/usb/persistence.conf
umount /mnt/usb
```

That is it. You have now created a persistent Live Kali Linux USB. Reboot your system and you should be able to boot the Kali Linux operating system from the USB drive.