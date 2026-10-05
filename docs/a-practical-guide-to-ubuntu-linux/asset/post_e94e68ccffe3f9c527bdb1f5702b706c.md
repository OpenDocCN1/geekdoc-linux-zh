
## 232 CHAPTER 6 THE LINUX FILESYSTEM

When you change directories back to the parent, you end up in the directory holding a symbolic link:

```
$ cd ..
$ pwd
/tmp
$ /bin/pwd
/tmp
```

## rm: REMOVES A LINK

When you create a file, there is one hard link to it. You can delete the file or, using Linux terminology, remove the link with the rm utility. When you remove the last hard link to a file, you can no longer access the information stored there and the operating system releases the space occupied on the disk for use by other files. This space is released if symbolic links to the file remain. When there is more than one link to a file, you can remove a hard link and still access the file from any remaining link. Unlike DOS and Windows, Linux does not provide an easy way to undo a file once you have removed it. A skilled hacker, however, can recover the file with time and effort.

When you remove all hard links to a file, you will not be able to access the file through a symbolic link. In the following example, cat reports that the file total does not exist because it is a symbolic link to a file that has been removed:

```
$ ls -sum
-rw-r--r-- 1 max pubs 981 2010-05-24 11:05 sum
$ ln -s sum total
$ rm sum
$ cat total
cat: No such file or directory
$ ls -l total
lrwxrwxr-x 1 max pubs 6 2010-05-24 11:09 total -> sum
```

When you remove a file, be sure to remove all symbolic links to it. Remove a symbolic link in the same way you remove other files:

```
$ rm total
```

## CHAPTER SUMMARY

Linux has a hierarchical, or treelike, file structure that makes it possible to organize files so you can find them quickly and easily. The file structure contains directory files and ordinary files. Directories contain other files; ordinary files generally contain text, programs, or images. The ancestor of all files is the root directory and is represented by / standing alone or at the left end of a pathname.

Most Linux filesystems support 255-character filenames. Nonetheless, it is a good idea to keep filesystems simple and intuitive. Filename extensions can help file-names more meaningful.

When you are logged in, you are always associated with a working directory. Your home directory is the working directory from the time you log until you use `cd` to change directories.

An absolute pathname starts with the root directory and contains all the filenames that trace a path to a given file. The pathname starts with a slash, representing the root directory, and contains additional slashes following all the directories in the path, except for the root directory in the case of a path that points to a directory.

A relative pathname is similar to an absolute pathname but traces the path starting from the working directory. A simple filename is the last element of a pathname and is in form of a relative pathname; it represents a file in the working directory.

A filesystem contains important directories, including `/usr/bin`, which stores most of the Linux utility commands, and `/dev`, which stores device files, many of which represent physical pieces of hardware. An important standard file is `/etc/passwd`; it contains information about users, such as user's ID and name.

Among the attributes associated with each file are access permissions. They determine who can access the file and how the file may be accessed. Three groups of users can potentially access the file: the owner, members of a group, and all others. An ordinary file can be accessed in three ways: read, write, and execute. The ls with -l option displays these permissions. For directories, execute access is needed to define the directory that can be searched.

The owner of a file or a user working with root privileges can use the chmod utility to change the access permissions of a file. Custom permissions for the file's owner, the group, and all others on the system.

Access Control Lists (ACLs) provide finer-grained control over who can access specific directories and files than traditional Linux permissions. With ACLs you can specify the ways in which each of several users can access a directory or file. Utilities preserve ACLs when working with files.

An ordinary file stores data, such as textual information, programs, or images. A directory is a standard-format disk file that stores information, including names, ordinary files and other directory files. An inode is a data structure, stored on disk, that defines a file's existence and is identified by an inode number. A directory relates each of the files to an inode.

A link is a pointer to a file. You can have several links to a file so you can share the file with other users or have the file appear in more than one directory. Because only one copy of a file with multiple links exists, changing the file through any one link causes the changes to appear in all the links. Hard links cannot link directories or span filesystems, whereas symbolic links can.

Table 6-3 summarizes the utilities introduced in this chapter.

| Utility | Function |
| :--- | :--- |
| cd | Associates you with another working directory (page 209) |
| chmod | Changes access permissions on a file (page 216) |
| getfacl | Displays a file's ACL (page 222) |
| ln | Makes a link to an existing file (page 227) |
| mkdir | Creates a directory (page 208) |
| pwd | Displays the pathname of the working directory (page 204) |
| rmdir | Deletes a directory (page 210) |
| setfacl | Modifies a file's ACL (page 222) |

## EXERCISES

1. Is each of the following an absolute pathname, relative pathname, or simple filename?
   a. /home/max
   b. /home/zach
   c. letter
   d. /home/promo

2. List the commands you can use to perform these operations:
   a. Make your home directory
   b. Identify the working directory
   c. If your answer to 4a is two or more, attempt to create a hard link to another filesystem. What error message do you get? What happens when you create a symbolic link instead?

3. If the working directory is literature, give three sets of commands you can use to create a subdirectory named classics. Also give sets of commands you can use to remove classics and its contents.

4. Use the df with the -h (human-readable) option to answer the following questions:
   a. How many filesystems are mounted?
   b. Which filesystem stores your home directory?
   c. Assuming your answer to a is two or more, attempt to create a hard link to another filesystem.

5. Suppose you have a file that is linked to another user. How can you ensure that changes to the file are no longer shared?

6. You should read permission for /etc/passwd. To answer the following questions, use cat or less to display /etc/passwd.
   a. Which character is used to separate fields?
   b. How many fields are used to describe each user?
   c. How many users are on the system?
   d. How many different shells are in use on your system? (Hint: Look at the last field.)
   e. The second field of /etc/passwd stores passwords in encoded format. If the password file contains an x, your system uses shadow passwords and stores elsewhere. Does your system use shadow passwords?

7. /home/zach/draft and /home/max/letter are links to the same file and the following sequence of events occurs, what will be the date in the opening of the letter?
   a. Max gives the command vim letter.
   b. Zach gives the command vim draft.
   c. Zach changes the date in the opening of the letter to January 31, 2010, writes the file, and exits from vim.
   d. Max changes the date to February 1, 2010, writes the file, and exits from vim.

8. Suppose a user belongs to a group that has all permissions on a file named jobs_list, but the user, as the owner of the file, has no permissions. Describe which operations, if any, the user/owner can perform on jobs_list. Which command can the user/owner give that will grant the user/owner all permissions on the file?

9. Does the root directory have any subdirectories you cannot search as an ordinary user? Does the root directory have any subdirectories you cannot read as a regular user? Explain.

10. Assume you have the directory structure shown in Figure 6-2 on page 201 and the following directory permissions:

```
d--x--x--- 3 zach pubs 512 2010-03-10 15:16 business
drwxr-xr-x 2 zach pubs 512 2010-03-10 15:16 business/milk_co
```

For each category of permissions—owner, group, and other—what happens when you run each of the following commands? Assume the working
