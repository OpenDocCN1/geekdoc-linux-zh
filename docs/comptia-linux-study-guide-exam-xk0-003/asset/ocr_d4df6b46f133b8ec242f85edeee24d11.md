![](bbox=[0.15, 0.1, 0.35, 0.25])

Most computers’ actions are tied very closely to their disk partitions and the files they contain. Web servers must be able to deliver Web files stored on disk, workstations must be able to run applications and store data on disk, and so on. Therefore, it’s important that you can manage these files and the filesystems that contain them where you work with a Linux computer. Much of this chapter is devoted to this topic, starting with a look at the underlying hardware and Linux’s interfaces to it, then moving on to partition management, and finally looking at the Linux filesystem layout.

> Objective 2.7 is covered partly in this chapter and partly in Chapter 10, “Configuring Network Servers.”

> The term “filesystem” has two meanings. First, it may refer to an organized collection of files, stored in some specific set of directories. For instance, certain filesystem standards for Linux specify in what directories certain types of files reside. Second, “filesystem” may refer to the low-level data structures used to organize files on a hard disk partition or removable disk. Several different filesystems of this second variety exist, such as ext3fs, ReiserFS, and FAT. This chapter covers both types of filesystems; which meaning is intended is usually clear from the context. When it isn’t, I clarify by using terms such as “directory structure” or “directory tree” for the first type or “low-level filesystem” for the second variety.

# # Storage Hardware Identification

Before delving into the details of how Linux manages partitions and files, you should understand some of the basics of storage devices. Several types of storage devices exist, and specific types have characteristics that can influence how Linux interacts with them. Understanding how Linux interacts with the hardware (device filenames, for instance) is also critically important.

> Chapter 1, “Getting Started with Linux,” describes low-level hardware concerns in more detail.