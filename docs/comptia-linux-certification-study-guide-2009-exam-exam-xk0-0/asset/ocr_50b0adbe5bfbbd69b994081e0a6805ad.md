For example:

/hd0/ dev/sda

Incorrect answers and explanations: A, B, and D. Answer A is incorrect because the directory path /etc does not contain device.map. Answer B is incorrect because the directory /boot/grub/boot does not exist. Answer D is incorrect because /etc/init.d is the directory containing the runlevels scripts.

+   14.  The Linux kernel is a critical component in the Linux boot process. Where does it reside on the system?
+   
+   A.  The /kernel directory
+   
+   B.  The /grub/boot/kernel directory
+   
+   C.  The /boot directory
+   
+   D.  The /boot/kernel directory

Correct answer and explanation: C. Answers C is correct, because the Linux kernel is located in the /boot directory.

Incorrect answers and explanations: A, B, and D. Answers A, B, and D are incorrect; these directories do not exist.

+   15.  The Linux bootloader is a very critical component in the Linux boot process. Where does it reside on the system?
+   
+   A.  It resides in the Master Boot Record.
+   
+   B.  It resides inside the Linux kernel.
+   
+   C.  The /etc directory
+   
+   D.  Inside the system BIOS

Correct answer and explanation: A. Answer A is correct; the Linux Bootloader resides in the Master Boot Record (MBR). The MBR is the bootloading sector. The system BIOS reads the first sector of the boot device. This sector is 512 bytes in size. For a hard disk drive, this special sector is known as the MBR.

Incorrect answers and explanations: B, C, and D. Answer B is incorrect; the Linux bootloader is used to retrieve the Linux kernel. Answer C is incorrect because /etc is a folder mounted by the Linux kernel once it obtains control from the Linux bootloader. Answer D is incorrect because the system BIOS reads the first sector of the boot device. This sector contains the Linux boot loading program. The system BIOS loads the bootloader into memory and executes the program.