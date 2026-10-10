because system BIOS is not a program that interfaces with the Linux User community. Answer **C** is incorrect because the system BIOS does not present the biography of the creator of Linux.

5. You need to access your department's Linux server to perform system maintenance. You need to power down the system to install new hardware components. Which runlevel shuts down your system?

+   * **A.** 6
+   * **B.** 0
+   * **C.** 2
+   * **D.** 1

Correct answer and explanation: **B.** Answer **B** is correct because runlevel 0 is used to shut down a system.

Incorrect answers and explanations: **A, C**, and **D.** Answer **A** is incorrect; runlevel 6 reboots your system. It does not power down, only reboots. Answer **C** is incorrect; runlevel 2 allows multiple users to log into the system. However, users are not allowed network connectivity. Login locally is the only option available. It does not power down your system. Answer **D** is incorrect because runlevel 1 is used for root level access only in single user mode.

6. The Linux servers in your department all use IDE hard disk drives. Your supervisor requested that you reinstall GRUB into the first partition on the IDE first hard disk while the machine is still running. To install GRUB on the IDE hard disk drive's first partition, which shell command should you use?

+   * **A.** `grub ide`
+   * **B.** `grub-install /dev/hda1`
+   * **C.** `grub-install /dev/sda1`
+   * **D.** `grub-runlevel /dev/hda1`

Correct answer and explanation: **B.** Answer **B** is correct because /hda1 is the correct naming convention for the IDE hard disk drive's first partition. `grub-install` is the command used to install GRUB while the Linux server is still running.

Incorrect answers and explanations: **A, C**, and **D.** Answer **A** is incorrect because ide is not the proper Linux syntax for the IDE hard disk drive. To install GRUB on a running system, the grub shell command is not used. Answer **C** is incorrect because the disk device syntax is for a SCSI Drive. Answer **D** is incorrect; `grub-runlevel` is not a command.