# HANDS-ON PROJECTS

# Project 9-1

In this project, you learn about the Linux kernel running on your system. To complete this project you should have an installed Linux system.

+   1. Log in to Linux.
+   2. If you logged in using a graphical login screen, open a terminal window. Use the su command to change to root access.
+   3. Enter the command uname -r to see which version of the Linux kernel is running on the computer. What kernel version are you running?
+   4. Enter the command uname -v to see the timestamp of the Linux kernel.
+   5. Enter the command cat /proc/version. How does the information displayed compare to the output of the uname command? Compare this output with the output of the uname -a command.
+   6. Review the contents of the grub.conf file by entering the command less /boot/grub/grub.conf.
+   7. Locate the indented line in the file that begins with "kernel," and note the directory and file name to which it refers. Do you see any boot parameters on the kernel line?
+   8. Press q to exit the less command.
+   9. Enter the command cd /boot to change to the directory where the kernel is located.
+   10. Enter the command ls -l to see the files in the boot directory. Can you locate the file named in the kernel line grub.conf? That file is the Linux kernel. How large is the file? Why? What is the real kernel size?
+   11. Enter the command dmesg | less to review the kernel boot messages. What parts of the system hardware do you recognize in the output? How might this output help you manage the system's hardware?
+   12. Press q to exit the less command.
+   13. Close all open windows and log out of Linux.

# Project 9-2

In this project, you review the initialization process for your Linux system. To complete this project you should have an installed Linux system.

+   1. Log in to Linux. (Don't use the root account, even if you have that password.)
+   2. If you logged in using a graphical login screen, open a terminal window.