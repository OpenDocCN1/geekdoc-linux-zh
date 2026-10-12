sets the i attribute of a file in an ext2 file system. When this attribute is set, the file cannot be modified, deleted, or renamed by anyone. No links can be added to point to this file, either. This attribute can be set or cleared only by the root user. So, you can use this attribute to protect against file accidents. When you need to clear the attribute, run

```
chattr -i filename
```

A few other interesting features of the ext2 system, such as the undelete attribute, are not yet implemented but will become available in a future ext2 file system version. If you start using the chattr command, you may notice that sometimes you can’t modify or delete a file even though you have the permission to do so. This happens when you forget that you previously set the immutable attribute of the file by using chattr; because this attribute does not show up in the ls output, it can be a bit confusing. To see which files have what ext2 attributes, use the lsattr program.

Unfortunately, what you know now about file and file system security might is also known by informed hackers. Using tools such as chattr maybe make damaging your files or file systems a bit harder for hackers, but it won’t make it impossible for them to do so. In fact, if a miscreant gets root level privileges, ext2 attributes provide only a simple hide-and-seek game. One major problem after a break is to determine whether you can trust your files. You might wonder whether the miscreant has installed a Trojan horse application or embedded a virus to infect new files and possibly provide access to other computers. None of the methods discussed in this section handles this aspect of a security problem. The solution is to run a file integrity checker program, such as Tripwire.

# Using Tripwire to ensure file integrity

Simply speaking, Tripwire is a file and directory integrity checker that creates a database of signatures for all files and directories and stores them in a single file. When Tripwire is run again, it computes new signatures for current files and directories and compares them with the original signatures stored in the database. If a discrepancy exists, the file or directory name is reported along with information about the discrepancy.