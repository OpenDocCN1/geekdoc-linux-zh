
a framework designed to allow workstations access to directory/file shares on a network-based server.

**11.** You need to use fdisk to establish a partition for a new SCSI disk drive you want to add for extra storage space. The original drives are all IDE drives. Which is the correct syntax?

- **A.** `fdisk /dev/SCSI1`
- **B.** `fdisk /dev/IDE`
- **C.** `fdisk /dev/sda`
- **D.** `fdisk /dev/sdb`

Correct answer and explanation: **C**. Answer **C** is correct; the SCSI device notation for the first disk is `/dev/sda`.

Incorrect answers and explanations: **A**, **B**, and **D**. Answers **A** and **B** are incorrect because both do not exist as valid default Linux device names. Answer **D** is incorrect; the SCSI device notation for the second SCSI disk is `/dev/sdb`. The system indicated that this is the first SCSI drive added.

**12.** Which file, when the system initially starts up, will automatically mount file systems?

- **A.** `/etc/fstab`
- **B.** `/boot/fstab`
- **C.** `/dev/devices.map`
- **D.** `/etc/grub.conf`

Correct answer and explanation: **A**. Answer **A** is correct; the `/etc/fstab` file is used to define and automatically mount file systems.

Incorrect answers and explanations: **B**, **C**, and **D**. Answer **B** is incorrect because the file does not exist. Answers **C** and **D** are files used during the loading of the Linux kernel by GRUB.

**13.** What is an ISO loopback device?

- **A.** The transformation of special file into a virtual Linux filesystem
- **B.** A device that returns feedback tests to the monitor
- **C.** The `/null` driver device
- **D.** The IP address 127.0.0.1

Correct answer and explanation: **A**. Answer **A** is correct; the Linux operating system offers support for an additional unique type of filesystem. This type of filesystem is known as the loopback filesystem. Most Linux distributions have the loopback device compiled into the kernel. The kernel supports the transformation of a special file containing an image of another filesystem into a device that can be used like any other Linux partition or device. Linux loopback devices are commonly used for CD/DVD ISO images. The disk image created of the CD/DVD disc contains the UDF or ISO 9660 filesystem format. Before accessing the loopback device, the ISO image must be downloaded and mounted. The Linux mount command is used to attach the virtual filesystem image.

Incorrect answers and explanations: **B**, **C**, and **D**. Answer **B** is incorrect because the Linux echo command will return feedback to the monitor. Answer **C** does not exist. Answer **D** is the network adaptor loopback address for testing network connectivity.

**14.** Which Linux command is used to designate a specific file or partition for swapping?

- **A.** `/swap`
- **B.** `filesaap`
- **C.** `swapon`
- **D.** GRUB

Correct answer and explanation: **C**. Answer **C** is correct; `swapon` is the Linux command used to designate a specific file or partition for swapping.

Incorrect answers and explanations: **A**, **B**, and **D**. Answer **A** is incorrect; `/swap` is a precreated `swap` partition created during the initial installation. Answer **B** is incorrect because it is an invalid Linux command. Answer **D** is incorrect; GRUB is the Linux bootloader program.

**15.** What is the purpose of the Linux `exportfs` command?

- **A.** It functions as the Linux bootloader
- **B.** To partition a storage device
- **C.** To designate a specific file or partition for swapping
- **D.** To activate the access of shared NFS directories

Correct answer and explanation: **D**. Answer **D** is correct; `exportfs` is the Linux command used to activate the access of shared NFS directories on the NFS server.

Incorrect answers and explanations: **A**, **B**, and **C**. Answer **A** is incorrect; GRUB is the Linux bootloader program. Answer **B** is incorrect; `fdisk` is the Linux command used to partition a storage device. Answer **C** is incorrect; `swapon` is the Linux command used to designate a specific file or partition for swapping.

## CHAPTER 4: BOOTING LINUX

**1.** You need to access your department's Linux server to perform system maintenance. To perform the necessary administrative tasks, all users need to be logged out of the system and they are not allowed to log back into the system while the system maintenance activities are underway. Which runlevel only grants root access?

- A. 6
- B. 0
- C. 2
- D. 1

Correct answer and explanation: **D**. Answer **D** is correct because runlevel 1 is used for root level access only in single user mode.

Incorrect answers and explanations: **A**, **B**, and **C**. Answer **A** is incorrect; runlevel 6 reboots your system. Answer **B** is incorrect because runlevel 0 shuts down the system. Answer **C** is incorrect; runlevel 2 allows multiple users to log into the system. However, users are not allowed network connectivity. Login locally is the only option available.

**2.** Your department's manager would like all Linux users to access their workstations by using a graphical user interface and have network connectivity. Which runlevel uses a graphical user interface by default and grants network connectivity?

- A. 2
- B. 0
- C. 5
- D. 1

Correct answer and explanation: **C**. Answer **C** is correct because runlevel 5 grants network connectivity and the system starts up in graphical user interface mode.

Incorrect answers and explanations: **A**, **B**, and **D**. Answer **A** is incorrect; runlevel 2 does not provide network connectivity. Answer **B** is incorrect because runlevel 0 shuts down the system. Answer **D** is incorrect because runlevel 1 is used for granting root level access only in single user mode.

**3.** Your department's manager would like all Linux users to access their workstations by using a command line mode [no graphical user interface] and have network connectivity. Which runlevel uses a command line mode for multiple users and grants network connectivity?

- A. 2
- B. 0
- C. 3
- D. 1

Correct answer and explanation: **C**. Answer **C** is correct because runlevel 3 grants network connectivity and with a command line mode [no graphical user interface].

Incorrect answers and explanations: **A**, **B**, and **D**. Answer **A** is incorrect; runlevel 2 does not provide network connectivity. Answer **B** is incorrect because runlevel 0 shuts down the system. Answer **D** is incorrect because runlevel 1 is used for granting root level access only in single user mode.

**4.** What is the purpose of the computer system BIOS?

- A. Loads the Linux kernel before loading GRUB
- B. Allows the user to log into the Linux operating system and change the kernel
- C. Presents the biography of Linus Torvalds, creator of Linux
- D. Commences the Linux boot process

Correct answer and explanation: **D**. Answer **D** is correct; the system BIOS, after powering up your system, commences the Linux boot process. The system BIOS identifies, tests, and initializes critical system components such as the hard and floppy disk drives, RAM, keyboard, video display card, hard disk, and other hardware. It determines what device will be used to boot the operating system. For this subtask, system BIOS is able to select from various devices for booting [for example, floppy disk drive, hard disk drive, CD/DVD drive] the operating system. The system BIOS selects the first drive and loads the disk geometry characteristics [for example, cylinders, heads, sectors]. Finally, it reads the first sector of the boot device to load the Linux bootloader. Then, it transfers the control to the Linux bootloader.

Incorrect answers and explanations: **A**, **B**, and **C**. Answer **A** is incorrect; the Linux bootloader is used to retrieve the Linux kernel. The bootloader is retrieved by the system BIOS. Answer **B** is incorrect
