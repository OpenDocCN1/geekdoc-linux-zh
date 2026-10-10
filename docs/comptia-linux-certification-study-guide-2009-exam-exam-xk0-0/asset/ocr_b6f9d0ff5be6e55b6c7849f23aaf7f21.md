a framework designed to allow workstations access to directory/file
shares on a network-based server.

+   11. You need to use fdisk to establish a partition for a new SCSI disk drive you want to add for extra storage space. The original drives are all IDE drives. Which is the correct syntax?
+   **A.** `fdisk /dev/SCSI1`
+   **B.** `fdisk /dev/IDE`
+   **C.** `fdisk /dev/sda`
+   **D.** `fdisk /dev/sdb`
+   Correct answer and explanation: **C**. Answer **C** is correct; the SCSI
+   device notation for the first disk is `/dev/sda`.
+   Incorrect answers and explanations: **A**, **B**, and **D**. Answers **A** and
+   **B** are incorrect because both do not exist as valid default Linux device
+   names. Answer **D** is incorrect; the SCSI device notation for the sec-
+   ond SCSI disk is `/dev/sdb`. The system indicated that this is the first
+   SCSI drive added.

+   12. Which file, when the system initially starts up, will automatically
+   mount file systems?
+   **A.** `/etc/fstab`
+   **B.** `/boot/fstab`
+   **C.** `/dev/devices.map`
+   **D.** `/etc/grub.conf`
+   Correct answer and explanation: **A**. Answer **A** is correct; the
+   `/etc/fstab` file is used to define and automatically mount file systems.
+   Incorrect answers and explanations: **B**, **C**, and **D**. Answer **B** is
+   incorrect because the file does not exist. Answers **C** and **D** are files
+   used during the loading of the Linux kernel by GRUB.

+   13. What is an ISO loopback device?
+   **A.** The transformation of special file into a virtual Linux filesystem
+   **B.** A device that returns feedback tests to the monitor
+   **C.** The `/null` driver device
+   **D.** The IP address 127.0.0.1
+   Correct answer and explanation: **A**. Answer **A** is correct; the
+   Linux operating system offers support for an additional unique type of
+   filesystem. This type of filesystem is known as the loopback filesys-
+   tem. Most Linux distributions have the loopback device compiled