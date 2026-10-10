![](bbox=[0.14, 0.1, 0.35, 0.27])

Protecting data includes creating and managing *backups*. A backup, often called an *archive*, is a copy of data that can be restored sometime in the future should the data be destroyed or become corrupted.

Backing up your data is a critical activity, but even more important is planning your backups. These plans include choosing backup types, determining the right compression methods to employ, and identifying which utilities will serve your organization’s data needs best. You may also need to transfer your backup files over the network. In this case, ensuring that the archive is secure during transit is critical as well as validating its integrity once it arrives at its destination. All of these various topics concerning protecting your data files are covered in this chapter.

# ## Understanding Backup Types

There are different classifications for data backups. Understanding these various categories is vital for developing your backup plan. The following backup types are the most common types:

+   ■ System image
+   ■ Full
+   ■ Incremental
+   ■ Differential
+   ■ Snapshot
+   ■ Snapshot clone

Each of these backup types is explored in this section. Their advantages and disadvantages are included.

**System Image**   A *system image* is a copy of the operating system binaries, configuration files, and anything else you need to boot the Linux system. Its purpose is to quickly restore your system to a bootable state. Sometimes called a *clone*, these backups are not normally used to recover individual files or directories, and in the case of some backup utilities, you cannot do so.

**Full**   A *full backup* is a copy of all the data, ignoring its modification date. This backup type’s primary advantage is that it takes a lot less time than other types to restore a