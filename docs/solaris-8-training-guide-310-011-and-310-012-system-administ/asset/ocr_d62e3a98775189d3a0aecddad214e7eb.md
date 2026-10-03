2. A., C., D. Run level s is the single-user (system administrator) state. Only root is allowed to log in at the console, and any users logged in are logged out when entering this run level. All file systems previously mounted remain mounted and accessible. All services except the most basic OS services are shut down in an orderly manner.

3. C. The init command is used to change run levels, also called init states.

4. D. Security-mode restricts the set of operations that users are allowed to perform at the OpenBoot prompt.

5. B., C., D. On most SPARC-based systems, the bootstrap procedure consists of some basic phases. First, the system hardware is powered on or the system firmware (PROM) executes a power-on self-test (POST). After the tests have been completed successfully, the firmware attempts to autoboot if the appropriate OpenBoot configuration variable (auto-boot?) has been set.

6. C. The uname command, with the -a flag set, displays basic information currently available from the system, including hardware platform and current operating system release.

7. A., C., D. The Solaris Installation program prompts you for the following: hostname, IP address, Subnet mask, whether to install IPv6, name service, whether to install Kerberos security, timezone, root password, and language.

8. C., D. A patch might not be installed if it requires another patch that is not installed or if the patch is incompatible with another, already installed patch.

9. C. The pkgchk command checks the accuracy of a software package installation.

10. B. Max Inactive. This field contains the maximum number of days an account can go without

being accessed before it is automatically locked. A blank field means the account remains active no matter how long it goes unused.

11. C. Bourne and Korn shells initialize with a .profile, whereas the C shell uses .login and .cshrc.

12. A., C. The High Sierra (HSFS) file system is a read-only file system used on CD-ROMs, and the UNIX file system (UFS) is the default disk-based file system used by Solaris. TMPFS resides in memory. Data in this type of file system is destroyed upon reboot. NFS is the Network File System, which is remotely mounted over the network.

13. B. The superblock stores much of the information about the file system. The boot block stores information used when booting the system. An inode stores all information about a file except its name. A storage or data block stores data for each file.

14. C. The df command and its options can be used to see the capacity of each file system mounted on a system, the amount of space available, and the percentage of space already in use.

15. B. The newfs command automatically determines all the necessary parameters to pass to mkfs to construct new file systems. newfs was added in Solaris to make the creation of new file systems easier.

16. The fsck command checks and repairs file systems. Any of the others could be used to copy one file system to another.

17. D. The fuser command can be used to display which processes are using a particular file system. The following example uses the fuser command to find out why /cdrom is busy:

```
fuser -u /cdrom
```