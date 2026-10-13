example.txt, answer c is incorrect. Because files are downloaded with this command, answer d is incorrect.

# Question 25

Answer b is correct. Linux can find your lilo.conf file, but it is having trouble finding your secondary boot loader, /boot/boot.b. Because Linux finds your lilo.conf file in your master boot record (MBR), answers a and d are incorrect. The vmlinuz file contains the Linux kernel. The Linux kernel loads after a selection is made at the full LILO boot: prompt; therefore, answer c is incorrect.

# Question 26

Answers a, c, and d are correct. If you don't see the LILO boot: prompt, you have a problem with your master boot record (MBR). The /sbin/lilo command does restore the contents of your lilo.conf file to your MBR. Booting your computer with a Linux boot disk or installation CD can help you get to your lilo.conf file. The Linux installation CD can work as well as the boot disk if it has a rescue mode. Because the fdisk /mbr command restores an MS-DOS MBR, answer b is incorrect.

# Question 27

Answer b is correct. You can't integrate GPL software with proprietary software unless you release the integrated package under the GPL. You can sell GPL software for a profit; therefore, answer a is incorrect. You can freely get the source code for GPL software, and you can modify it to meet your needs. Therefore, answer c is incorrect. Because you can access documentation for GPL software, answer d is incorrect.

# Question 28

Answer b is correct. When you type the linux single command at the LILO boot: prompt, you start Linux in single-user mode without needing a login. You can then use the passwd command to change the root user password. To change into single-user mode from within Linux, you need to have root or superuser access. Because this password has been forgotten, answers a, c, and d are incorrect. You can't get to the point where you could use the init command, nor could you log in to Sarah's root account on her computer without her password.