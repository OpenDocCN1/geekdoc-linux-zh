
Its contents. The same applies if you delete `NewLink`; `MyFile` will still be there. However, if you also delete `NewLink`, the file is gone for good. If you use the `ls` command with the `-i` option, you will see that both files have the same inode number:

```
ls -i MyFile NewLink
3798 MyFile		3798 NewLink
```

You can see the number of links a file has by using `ls` with the `-l` option:

```
ls -l MyFile NewLink
-rw-r--r--  2 haddens haddens 23 Aug 13 11:35 MyFile
-rw-r--r--  2 haddens haddens 23 Aug 13 11:35 NewLink
```

Remember, as far as the operating system is concerned, these two pointers are equal, and it does not care which one was created first.

Although the existing file and new link can be in the same directory, links are usually created in a different directory. To create a hard link, type:

```
ln MyFile /NewDirectory/NewLink
```

If only the new directory location is specified then the new link will have the same name as the original file.

Some limitations of hard links are that users can't make hard links to directories and the links must be on the same filesystem. root, however, can create a hard link to a directory by using either the `-d` or `-F` option.

## Symbolic Links

A *symbolic or soft link* is an indirect pointer to the file. It is a new directory entry that contains the path to the existing file. Symbolic links were created to overcome the limitations of hard links. They can be created to a:

- Directory by a user
- Nonexistent file
- File on another filesystem

Symbolic links are created using the `ln` command with the `-s` option:

```
ln -s MyFile /NewDirectory/SymLink
```

When using the `ls` `-l` command to look at a symbolic link, you will notice a few differences. The type of file is listed as `l` (the first character), the path to the original file is listed, and the file attributes are different. For example, if both the original file and the symbolic link are located in the pwd, the `ls -l` command would display the following:

```
ls -l MyFile SymLink
.rw-r--r-- 1 hadden hadden 23 Aug 13 11:35 MyFile
lrw-rw-rw- 1 hadden hadden 4 Aug 13 12:13 SymLink -> MyFile
```

You can delete the original file without removing any symbolic links; however, any symbolic links will no longer work. Because a symbolic link contains only the path to the original file, when the original file is deleted the link is pointing to a nonexistent file.

To create a link to a directory, use the `-F` option. However, symbolic links to directories can't work exactly like you expect when using the `cd` command. Different shells will act differently.

You can use a symbolic link to a directory as the argument to the `cd` command. Under the bash shell, if you then issued the `pwd` command, it would return the symbolic name of the directory. However, if you issue the command `cd ..` to move up one level in the directory structure, you are placed in the directory containing the symbolic link, rather than the parent directory of the directory referenced by the symbolic link.

In other shells, issuing the `pwd` command returns the name of the original directory rather than the symbolic link. When you issue the `cd ..` command, you are placed in the parent directory of the link itself.

### Key Concept

A link provides access to a file from different locations. Remember that all hard links to a file have the same inode number as the original file. This means that each link (filename) is associated with the same physical location on the disk. A soft link, however, contains only the path to the original file. Any one of the hard links can be deleted without preventing access via other hard links to that file. If the original file is deleted then all soft links to that file will no longer work.

## Managing System Files

In Chapter 3 we discussed the hierarchical nature of the Linux file system. How this directory hierarchy is organized is important in maintaining your system, installing software, and managing users. You will need to understand it for the exam.

Each distribution has some differences in where files are stored and how the directory structure should be organized. Over time, these differences have resulted in problems with software installation or going from one distribution to another, especially regarding where configuration files are stored.

As a result, an effort toward standardization has been undertaken. It is defined by the Filesystem Hierarchy Standard, which can be viewed at http://linuxpowerev.com/html/tutorials/fhs/fhs-toc.html. Although this standard was first defined to cover the Linux filesystem, it has been expanded to apply to other UNIX systems.

For the exam, you will need to know the standard locations for files. On the distribution-specific exam, you will need to know the locations specific to that distribution.

## Hierarchy

There are some directories that always should be present and that contain specific types of files. A good place to start is root, which is represented by / . This is the top or beginning of your directory structure.

The / is the container for various other directories. Think of it as the glue that holds your system together. As a rule, this directory should not contain other files. Table 6.9 shows the major directories, what they contain, and their purposes. These are the directories that you should be familiar with for the exam.

**Table 6.9 The Contents of the Root Directory and the Purpose of Each**

| Directory | Contents and Use |
|---|---|
| bin | Contains binaries that are required for system startup. |
| boot | Contains the kernel and any configuration files necessary for the boot loader. |
| dev | Contains files necessary for accessing all types of peripheral devices, not just those present on your system. |
| etc | Contains the system configuration files and scripts such as shell startup scripts. |
| etc/skel | Contains skeleton user files to be placed in user's home directory when his account is created. See Chapter 7 for more information on this directory. |
| etc/X11 | Contains X Window configuration files. |
| etc/rc.d | Contains startup scripts and the rc directories. See Chapter 2, "Booting Linux," for more information on the use and structure of this directory. |
| home | Contains subdirectories for each user except root to be used as home directories; every regular user needs a home directory to be able to log in. Additional subdirectories can be used to further classify users. |
| lib | Shared libraries and kernel modules. |
| Lost+found | Directory used for recovered files. |
| mnt | Temporary point to which to connect devices. |
| proc | This is a virtual directory that contains system information on the kernel, running processes, and how system resources are being used. |
| root | Home directory for the root user; can use the / directory itself in some distributions. |
| sbin | Contains administrative binaries and tools to be used only by the system administrator, root. |
| tmp | Contains temporary files; read, write execute access for everyone. |
| usr | Contains binaries, libraries, applications, and packages such as X Windows that should be accessible to regular users. Often contains links to files stored in var. |
| usr/bin | Contains most user applications and should be in the user's path. |
| usr/sbin | Contains non-essential administration utilities. |
| usr/local | Contains software that is not part of the operating system itself. Simplifies backups. |
| usr/local/bin | Contains binary files for software installed after installation of the operating system and should be on user's path. |
| usr/local/sbin | Contains locally installed administration utilities. |
| usr/include | Contains standard C/C++ header files. |
| usr/lib | Contains static libraries as well as subdirectories for libraries for non-C/C++ languages; configuration files for ldconfig. Contains links to X Windows files. |
| usr/src | Contains source files for most software installed on the system with a separate subdirectory for each package. |
| usr/src/linux | Linux source directory. |
| usr/X11R6 | Usually a link to another directory containing X Windows files. The organization of this directory might be different depending on the window manager being used. |
| var | Contains variable data such as logs and spooling directories for mail and news. Often contains links to files stored in var. |
| var/log | Contains log files. Can grow very large and should be monitored. |
| var/spool | Used to store temporary files for printing, mail, and news. Can grow very large and should be monitored. |
