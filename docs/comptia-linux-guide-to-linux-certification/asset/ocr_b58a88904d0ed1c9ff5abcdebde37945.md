# Project 5-3

In this hands-on project, you mount DVDs to the directory tree and view their contents.

+   1. Switch to a graphical terminal (tty1) by pressing **Ctrl+Alt+F1** and log in to the GNOME desktop using the user name of *user1* and the password of *LNxrocksl*.

+   2. Click the **Activities** menu and select the **Files** icon to open the Files application.

+   3. In your virtualization software, attach the DVD ISO image for Fedora Linux (Fedora-Live-Desktop-x86_64-20-1.iso) to the DVD drive for the virtual machine. After you have completed this action, view your Files application. Is there an icon that represents your Fedora Live Desktop DVD in the left pane? Place your mouse over this icon to view the mount point directory. Which directory was your DVD automatically mounted to?

+   4. Take a few moments to explore the contents of the DVD within the Files application. When finished, click the eject button next to the Fedora Live Desktop DVD icon to eject the DVD.

+   5. Switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the GNOME desktop using the user name of *root* and the password of *LNxrocksl*.

+   6. In your virtualization software, attach the DVD ISO image for Fedora Linux (Fedora-Live-Desktop-x86_64-20-1.iso) to the DVD drive for the virtual machine. After you have completed this action, type `mount` and press `Enter`. Is the DVD automatically mounted?

+   7. Next, type `mount /dev/cdrom /mymount` at the command prompt, and press `Enter`. What warning did you receive? Was the DVD successfully mounted to the /mymount directory?

+   8. At the command prompt, type `ls -F /mymount` and press `Enter`. Do you see the same files as you did in Step 4? Why?

+   9. At the command prompt, type `ls -l /dev/cdrom` and press `Enter`. What target file does the /dev/cdrom symbolic link point to?

+   10. At the command prompt, type `mount` and press `Enter`. Note the line at the bottom that lists your mounted DVD. What filesystem was automatically detected earlier when you mounted your DVD? Is the device file identical to the target file shown in Step 9?

+   11. Next, type `umount /mymount` at the command prompt and press `Enter`. Was the DVD successfully unmounted from the /mymount directory? Type the `mount` command at a command prompt and press `Enter` to verify this.

+   12. In your virtualization software, detach the DVD ISO image for Fedora Linux (Fedora-Live-Desktop-x86_64-20-1.iso) to the DVD drive for the virtual machine. This performs the same action as ejecting the DVD from the physical DVD drive.

+   13. Type `exit` and press `Enter` to log out of your shell.

![](bbox=[0.92, 0.28, 0.99, 0.33])

# Project 5-4

In this hands-on project, you work with standard hard disk partitions. You will first create a hard disk partition using the fdisk utility. Next, you create an ext4 filesystem on the partition and mount it to the directory tree. Finally, you use the /etc/fstab file to automatically mount the partition at boot time.

+   1. Switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of *root* and the password of *LNxrocksl*.