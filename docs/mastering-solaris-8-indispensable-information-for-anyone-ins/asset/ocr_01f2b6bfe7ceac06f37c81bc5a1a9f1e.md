Use the `list` command to determine the specific file type of any file in a directory that you are interested in. When you specify the long output form of the `list` command, the very first letter, shown here by the placeholder `<?>`, tells you the file type:

```
```bash
ls -1 <pathname>/<f11ename>
  <>rwr-xr 1 <foldrname> <groupname> 3268 Dec 18 2000 <f11ename>
```
```

In the following sections, I’ll describe the different types of files you’ll work with.

# ### Regular File

A *regular file* (the first letter designation of the `list` command is -), or as it is sometimes called, an ordinary file, is the most prevalent file type used by Solaris. Regular files can be text files, extended text files used by applications, and binary format executable or program files. Regular files can be any size, from very small to very large. The data in a regular file is in a format that Solaris can write and read, but it isn’t a requirement that Solaris be able to actually use the data in any way. For example, the data can be application specific or it can describe a program that Solaris can’t actually execute.

Even if you determine that a file is of the regular file type, you know very little that is useful about the file. You might want to know if it is a program file, a data file, or something else. The `file` command offers more information about the purpose that regular file types serve.

One example of a regular file is the core file that you may see appear in any of Solaris’s directories. This file is a dump file. Solaris writes into a core file information that describes an error condition that occurred. You can delete any of these files without concern, particularly after they haven’t been accessed for a while.

# ### Block-Special File

A *block-special file* (the first letter designation of the `list` command is b) is one of the two device files that Solaris maintains. This file format provides a method for transferring large amounts (blocks) of data to and from device drivers in the Solaris file system. Block file transfer is used by parallel ports and SCSI buses. Most block-special files are used to describe removable media and hard drives. Consider the `ls -1` command run against the `/dev/sda` file. It returns the following:

```
```text
brw-rw-- 1 root disk 8, 0 Dec 18 20:32 /dev/sda
```
```

Note that the b character indicates a block-special file and that files of this type have both major and minor device numbers (8 and 0, respectively) that Solaris uses to determine what class of device driver (and what specific device driver within that category of device drivers) this data can communicate with. Chapter 6 discusses this concept in more detail.