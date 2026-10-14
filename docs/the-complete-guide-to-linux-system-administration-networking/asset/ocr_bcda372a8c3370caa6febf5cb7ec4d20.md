that is sometimes used for backup operations is dd. The dd command does a “data dump” between any two devices or files.

A number of the graphical utilities for backing up your system that are listed later in this section rely on tar, cpio, or dump and restore in the background. Popular commercial backup utilities include features such as tracking tapes for you, keeping online indexes of each backup that you have performed, and automating schedules for unattended backups (similar to the options provided by the crontab command).

It’s common to use Linux backup utilities across a network—a single system equipped with a tape drive or other backup device is used to back up file systems located on machines all over the network. You can do this using many techniques, such as remotely mounting file systems using NFS or Samba software, or downloading files using Linux FTP server software. Most full-featured backup utilities create their own network connections between software components installed on the machine to be backed up and the machine where the tape drive is located. The documentation for specific utilities describes their networking capabilities; basic Linux utilities such as those described in the next section rely on services such as NFS to access networked data.

![](bbox=[0.18, 0.55, 0.28, 0.65])

Networking topics such as NFS, Samba, FTP, and more are covered in Guide to Linux Networking and Security (Course Technology 2003, ISBN 0-619-00094-5).

The commands tar, cpio, dump, and restore can operate either with a tape drive or with backup devices that rely on a standard Linux file system or standard mounting operation, such as an Iomega Jaz drive or a writable DVD drive. When you are using tape drives that are not randomly accessible (as a CD is), you may want to use additional tools to manage tape indexes, tape rewinding and searching, and so forth. One graphical tool for managing data backup operations is ark, part of the KDE desktop.

The complexities of maintaining large numbers of backup media for large volumes of data led manufacturers long ago to create specialized software to help with the task. Fortunately, several of these tools have made their way to the Linux platform:

+   - BRU (Backup and Restore Utility) from Enhanced Software Technologies has been popular among Linux users for many years. It provides multiple levels of data verification, unattended operation with scheduled backups, and support for numerous types of backup devices. See www.bru.com.
+   - Arkeia is another popular Linux backup tool. Arkeia is an enterprise network backup solution that is designed to control backup of multiple remote systems from a single location, saving or restoring data from anywhere on the network. See www.arkeia.com. Figure 13-4 shows a sample Arkeia screen.
+   - Storix provides system backup and disaster recovery designed specifically for IBM AIX and Linux operating systems. You can learn more at www.storix.com.