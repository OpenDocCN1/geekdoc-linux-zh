true physical catastrophe, but it also raises another issue—the need for appropriate security in the storage location you select.

For some reasons that you wouldn't leave the door to your house propped open and then go on vacation and wouldn't put a system that uses passwords on the Internet, you shouldn't store your backups in an insecure location. This is especially important if you are in charge of computer systems that are being used for business. Wherever you store your company's current and historical backup media should have a level of security comparable to wherever your computers are in the first place. Although your local cat burlar might not actively target a stack of CDs or removable disks, or a storage locker full of backups, any competitors would probably be ecstatic to be able to read and analyze the complete contents of your company's computer systems. Why not just everybody time and mail your source code and customer lists?

# Different Types of Backups

Now that I've discussed how to do backups and some of the basic issues related to storing them, let's review the strategy behind actually doing backups. As mentioned, backups take time and have associated costs such as backup media, but there are a variety of ways to manage and minimize these costs.

There are three basic types of backups:

+   * Archive backups: Provide a complete snapshot of the contents of a filesystem at a given time.
* Incremental backups: Reflect the changes to the contents of a filesystem since a previous backup.
* Spot backups: Provide a snapshot of specific files or the contents of one or more important directories at a given time.

# Note

Spot backups are the most common type of backups by home computer users writing a copy of your current projects, mail folders, or even your entire home directory to CD-Rs or DVD-Rs is relatively fast and cheap. There isn't much to say about this approach, because it can be easily done using drag-and-drop, so the rest of this section focuses on the classic backup models of archives and incremental backups. I'll use some techniques for spot backups later in this chapter. ■

Archive backups, often referred to as full backups, are the ultimate solution for restoring data because they usually contain a copy of every file and directory on a filesystem or under certain directory on your computer at the time the backup was made. In an ideal world, it would be great to do daily archive backups simply because this would guarantee that no one could ever lose more than a day's work, regardless of the type of calamity that occurred to your computer system. Unfortunately, archive backups have some drawbacks:

+   * They take the maximum amount of time that backups could require because they make a copy of every file and directory on every filesystem on all of your computer systems.