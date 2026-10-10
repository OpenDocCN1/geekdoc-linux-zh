GRUB, in the second form, is as an executable program [known as GRUB Shell] accessible from the root prompt. This executable program offers the following options:

+   
+   * To change the disk order
+   * To view other boot loaders
+   * To view the hard disk partition details
+   * To modify partition settings
+   * To boot user-defined configuration files
+   * To password protect the system during the bootloading process

GRUB, in the second form, emulates the first form of GRUB, and you can install or test GRUB configuration settings before applying the modifications to the system during the next boot process.

# **EXERCISE 4.1: Establishing a Boot Password for GRUB**

The Linux system grants anyone access to your system files during the GRUB boot process. To prevent an unauthorized person from accessing files on your Linux system during the boot process, a boot password needs to be assigned. In this exercise, we will assign a boot password to the system during interactive mode. To password protect other menu items, the “lock” keyword must be entered. You can also use the “password” command to provide a unique password for each menu item. Complete the following:

+   1. Sign into the system using administrator [root] privileges.
+   2. From the root command prompt, type the `grub` command to enter an encrypted password: `# grub-md5-crypt`.
+   3. Press the **Enter** (Return) key.
+   4. The system will display *Password: Enter <New password>*.
+   5. The system will display *Retype password: enter <Retype New password>*.
+   6. The system will display *Encrypted: $1$59aS3$/irAjfiPOy/hAwB51ng1* [only with your encrypted password].
+   7. Copy and paste the above encrypted string into the global section of the menu.lst file. The entry should look like the following:

```
`password -m: $1$59aS3$/irAjfiPOy/hAwB51ng1`
```