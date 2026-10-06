
# rm: Removes a Link

When you create a file, there is one hard link to it. You can delete the file, or using GNU/Linux terminology, remove the link with the rm utility. When you remove the last hard link to a file, you can no longer access the information stored in the file, and the operating system releases the space occupied on the disk for by other files. The space is released even if symbolic links remain. When there is more than one hard link to a file, you can remove a hard link and still access the file from any remaining link.

When you remove all the hard links to a file, you will not be able to access the file through a symbolic link. In the following example cat reports that the file total does not exist, because it is a symbolic link to a file that has been removed:

```
$ ls -l sum
-rw-r--r-- 1 alex pubs 981 May 24 11:05 sum
$ ls -sum total
$ rm sum
cat total
cat: No such file or directory
$ ls -l total
lrwxrwxr-x 1 alex pubs 6 May 24 11:09 total -> sum
```

When you remove a file, be sure to remove all symbolic links to it. Remove a symbolic link in the same way you remove other files:

```
$ rm total
```

# Chapter Summary

GNU/Linux has a hierarchical, or treelike, file structure that makes it possible to organize files so that you can find them quickly and easily. The file structure contains directory files and ordinary files. Directories contain other files, including other directories, whereas ordinary files generally contain text, programs, or images. The ancestor of all files is the root directory named /,

Most GNU/Linux filesystems support 255-character filenames. Nonetheless, it is a good idea to keep filenames simple and intuitive. Filename extensions can help make filenames more meaningful.

An absolute pathname starts with the root directory and contains all the filenames that trace a path to a given file. Such a pathname starts with a slash representing the root directory and contains additional slashes between the other names in the path.

- 1. Unlike DOS/MS Windows, there is no easy way to undelete a file once you have removed it. A skilled hacker, in some cases, piece the file together with time and effort.

A relative pathname is similar to an absolute pathname, but starts the path tracing from the working directory. A simple filename is the last element of a pathname and is a form of a relative pathname.

When you are logged in, you are always associated with a working directory. Your home directory is your working directory from the time you log in until you use cd to change directories.

A GNU/Linux filesystem contains many important directories including /usr/bin, which stores most of the GNU/Linux utility commands, and /dev, which stores device files, many of which represent a physical device of hardware. An important standard file is /etc/passwd; it contains information about users, such as the user ID and name.

Among the attributes associated with each file are access permissions. These determine who can access the file and the manner in which it may be accessed. Three groups of user(s) can access the file: the owner, members of a group, and all other users. A regular file can be accessed in three ways: read, write, and execute. The ls utility with the -l option displays these permissions. For directories, execute is redefined to mean that the directory can be searched, meaning that it can be used as part of a pathname.

The owner of a file or Superuser can use the chmod utility to change the access permissions of a file at any time. This utility defines read, write, and execute permissions for the owner, the file's group, and all other users on the system.

A link is a pointer to a file. You can have several links to a single file, so that you can share the file with other users or have the file appear in more than one directory. Because there is only one copy of a file with multiple links, changing the file through any one link causes the changes to appear in all the links. Hard links cannot cross directories or span file systems, whereas symbolic links can.

# Utilities Introduced in this Chapter

| Command | Description |
| :--- | :--- |
| cd | Associates you with another working directory (page 108) |
| chmod | Changes the access permissions on a file (page 119) |
| ln | Makes a link to an existing file (page 124) |
| mkdir | Creates a directory (page 106) |
| pwd | Displays the pathname of the working directory (page 107) |
| rmdir | Deletes a directory (page 115) |

# Exercises

- 1. Is each of the following an absolute pathname, a relative pathname, or a simple filename?
  a. milk_co
  b. correspond/business/milk_co
  c. /home/alex
  d. /home/alex/literature/promo
  e. . .
  f. letter.0610

- 2. List the commands you can use to:
  a. Make your home directory the working directory
  b. Identify the working directory

- 3. If your working directory is /home/alex with a subdirectory named literature, give three sets of commands that you can use to create a subdirectory named classics under literature. Also give several sets of commands that you can use to remove the classics directory and its contents.

- 4. The df utility displays all mounted filesystems along with information about each. Use the df utility with the -h (humanly readable) option to answer the following questions.
  a. How many filesystems are on your GNU/Linux system?
  b. Which filesystem stores your home directory?

- 5. Assuming that your answer to 4a is two or greater, attempt to create a hard link to a file on another filesystem. What error message do you get? What happens when you attempt to create a symbolic link to the file instead?

- 6. Suppose you have a file that is linked to a file owned by another user. What can you do so that changes to the file are no longer shared?

- 7. You should read permission for the /etc/passwd file. To answer following questions, use cat or less to display /etc/passwd. Look at the fields of information in /etc/passwd for the users on your system.
  a. What character is used to separate fields in /etc/passwd?
  b. How many fields are used to describe each user?
  c. How many users are on your system?
  d. How many different login shells are in use on your system? (Hint: Look at the last field.)
  e. The second field of /etc/passwd stores user passwords in encoded form. If the password field contains an x, your system uses shadow passwords and stores the encoded passwords elsewhere. Does your system use shadow passwords?

- 8. If /home/jenny/draft and /home/alex/letter are links to the same file and the following sequence of events occurs, what will be the date in the opening of the letter?
  a. Alex gives the command vi letter.
  b. Jenny gives the command vi draft.
  c. Jenny changes the date in the opening of the letter to January 31, 2003, writes the file, and exits from vi.
  d. Alex changes the date to February 1, 2003, writes the file, and exits from vi.

- 9. Suppose that a user belongs to a group that has all permissions on a file named jobs_list, but the user, as the owner of the file, has no permissions. Describe what operations, if any, the user can perform on jobs_list. What command that the user can give will grant the user all permissions on the file?

- 10. Does the root directory have any subdirectories that you cannot search? Does the root directory have any subdirectories that you cannot read? Explain.

- 11. Assume that you are given the directory structure shown in Figure 4-2 and the following directory permissions:

```
d--xr-x--- 3 jenny pubs 512 Mar 10 15:16 business
drwxr-xr-x 2 jenny pubs 512 Mar 10 15:16 business/milk_co
```

For each category of permissions—owner, group, and other—what happens when you run each of the following commands? Assume that the working directory is the parent of correspond and that the file cheese_co is readable by everyone.
  a. cd correspond/business/milk_co
  b. ls -l correspond/business
  c. cat correspond/business/cheese_co

# Advanced Exercises

- 19. Create a file named -x in an empty directory. Explain what happens when you try to rename it. How can you rename it?

- 20. Suppose that the working directory contains a single file named andor. What error message do you get when you run the following command line?

```
$ mv andor /or
```

Under what circumstances is it possible to run the command without producing an error?

- 21. The -i command displays a filename preceded by the inode number of the file (page 126). Write a command to output inode/filename pairs for the files in the working directory, sorted by inode number. (Hint: Use a pipe.)

- 22. Do you think that the system administrator has access to a program to decode user passwords? Why or why not (see exercise 6)?

- 23. Is it possible to distinguish a file from a hard link to a file? That is, a filename, can you tell whether it was created using an ln command? Explain.
