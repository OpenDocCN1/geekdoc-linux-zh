# INTRODUCTION

NOTE
This chapter covers objectives for exams Part I and Part II; however, the majority of the information relates to the first exam. (The second exam has limited questions related to file systems.) I'll make a notation when the material relates to the Part II exam.

In Chapter 6, “Introduction to File Systems,” I described how to create, check, mount, and display file systems with Solaris 8. I explained file system structure, disk geometry, disk slices, and the format utility. In Chapter 16, “Device Administration and Disk Management,” disk devices and device names are covered in detail. (Although Chapter 16 covers objectives for the Part II exam, I recommend reading that chapter to answer questions you might have after reading this chapter. File systems and devices go hand-in-hand but are not covered on the same exam; therefore, device configuration and naming are covered in Section II of this book.)

In this chapter, I continue the discussion of file systems. Specifically, I cover the objectives outlined at the beginning of this chapter.

# CONSTRUCTING A FILE SYSTEM

Constructing file systems is a topic covered on both exams. In Chapter 6, I described how newfs was the friendly front end to the mkfs command. The newfs command automatically determines all the necessary parameters to pass to mkfs to construct new file systems. newfs was added in Solaris to make the creation of new file systems easier. It’s highly recommended that the newfs command be used to create file systems, but it’s also important to see what is happening “behind the scenes” with the mkfs utility. The syntax for mkfs is as follows:

```
/usr/sbin/mkfs [options] <character device name>
```

Its options are described in Table 7.1.

TABLE 7.1
THE mkfs COMMAND

| Option | Description |
|---|---|
| -F | Used to specify the file system type. If this option is omitted, the /etc/vfstab and /etc/default/fs files are checked to determine a file system type. |