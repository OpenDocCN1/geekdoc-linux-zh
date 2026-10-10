
When you have finished with the man page, type q to exit from it.

See Appendix B for answers.

## Quiz

1. What is the effect of executing the following commands in succession?
```
$ cd /home/quixote<Enter>
$ cp file1 file2<Enter>
```

2. What is the effect of executing the following commands in succession?
```
$ cd /home/quixote<Enter>
$ mv file1 newfile<Enter>
```

3. What is the effect of executing the following commands in succession?
```
$ cd /home/quixote<Enter>
$ ln newfile myFile<Enter>
```

4. List the commands that can be used to view the contents of a file.

5. Which of the commands listed in Question 4 is used automatically when you invoke man pages? How do you know?

6. Which of the following are valid filenames?
- !
- aBCde
- -myfile
- myfile
- my.file
- my file
- .myfile

7. Once you have configured printing queues and installed printer drivers, what must you do to enable the printing environment? How would you do it?

8. What file has been updated by configuring the queues and installing the printer drivers?

See Appendix C for answers.

## Linux File Permissions

Along with passwords and authentication systems, file and directory access—known as *permissions*—forms the basis for system security. Although similar in nature, directory permissions and file permissions are not the same—and occasionally, that difference leads to confusion and even security breaches.

We begin the chapter with a review of the `ls -l` command, which you use to view existing file and directory permissions. Then, we focus on information found in the first column of the `ls -l` response information—the permission bits—which provide a summary of the file mode of these entries. We introduce several terms, commands, and issues involved in setting and changing permissions.

### Review of the `ls -l` Command

We described the output of the `ls -l` (long listing) command in detail in Chapter 4, “Files and Directories in Linux.” Example 6.1 and Table 6.1 illustrate our quick review of this frequently used command.

**Table 6.1 Response to the `ls -l` Command**

| FIELD 1      | FIELD 2 | FIELD 3   | FIELD 4   | FIELD 5 | FIELD 6        | FIELD 7   |
|:-------------|:--------|:----------|:----------|:--------|:---------------|:----------|
| total 6      |         |           |           |         |                |           |
| drwxr-xr-x   | 5       | quixote   | knights1  | 4096    | May 26 10:18   | admin     |
| drwxr-xr-x   | 5       | quixote   | knights1  | 4096    | Mar 07 08:11   | Desktop   |
| -rw-r-----    | 1       | penz      | knights1  | 144     | Jul 11 11:42   | manuals   |
| -rw-------    | 1       | quixote   | knights1  | 1116    | May 26 10:18   | mbox      |
| drwxrwxr-x   | 5       | quixote   | knights1  | 4096    | Apr 05 14:30   | misc      |
| drwxr-xr-x   | 5       | quixote   | knights1  | 4096    | Jul 11 15:21   | noble     |

**Example 6.1 The `ls -l` Command**

```
$ pwd<Enter>
/home/quixote
$ ls -l<Enter>
```

The following is a description of the different fields of output:

- **Field 1** consists of the object identifier and file or directory permission bits.
- **Field 2** is the link count. Ordinary files have a link count of 1. Directories have a link count of 2. The `ln` command can increase the link count by 1; removing a file reduces its link count by 1. When the link count reaches 0, the file is removed.
- **Field 3** is the username of the person who owns the entry.
- **Field 4** is the name of the group for which group protection privileges are in effect.
- **Field 5** is the character count of the entry.
- **Field 6** is the date and time the entry was last modified.
- **Field 7** is the name of the file or directory.

To display information about only a particular directory, use the `-d` option with the `ls -l` command. Directories are treated like ordinary files.

### Permissions

In this chapter, we will introduce the term *entry* when we discuss directory and subdirectory contents. Files, directories, linked files, block special files, character special files, symbolic links, named pipes, and sockets are all examples of entries. When a user creates an entry, he or she becomes the owner of that entry. Some people also use the term *object* to indicate an entry.

The owner of an entry generally wants to control who will have access to or use of the entry. Each entry, once created, has attributes called permission bits that are used for access control. Because it is possible to change the nature of these permission bits (or permissions), a term that we will use interchangeably) on an entry, the owner has the power to make the entry either more secure or more widely available.

**Table 6.2 Permission Bits**

|       | ENTRY | OWNER | GROUP | OTHERS |
|:------|:------|:------|:------|:-------|
|       | d     | rwx   | rwx   | rwx    |

Table 6.2 illustrates a breakdown of permission bits available to each entry. The single character on the far left of the permission bit string identifies the type of entry, or object. The leftmost group of three permission bits—in other words, the three located next to the object identifier—refers to the permissions the owner of the entry has with respect to the entry. The middle three are the permissions that the group has for the entry (that is, the group to which the entry will belong). The rightmost three bits are the permissions held by other users who are not owners of the entry and who are also not in the group to which the entry belongs.

For both files and directories, r is the permission to read; w is the permission to write; and x is the permission to execute. Although the names of these permissions are identical for files and directories, the permissions themselves mean different things. You might ask, “What do we mean by that?”

When viewing or establishing the permissions for an ordinary file:

- r permits the viewing of file contents.
- w permits the changing and storing of file contents.
- x permits the execution of the file (r is also needed).

But for a directory:

- r permits the viewing of files in the directory.
- w permits the creation and removal of files in the directory (x is also needed).
- x permits a user to be in the directory (that is, to cd to a directory and to access files from the directory).

The x permission is required to access any files or subdirectories within a directory. In other words, the x permission is required on all directories above the specific directory, as well.

To remove a file from a directory, you need only w and x permissions for the directory. You do not necessarily need permissions on the file itself.

### Changing Permissions: The `chmod` Command

You use the `chmod` (change permission mode) command along with symbolic notation or numeric notation to specify changes to the existing permissions for a file or directory. How do you perform this task? The answer is, by adding or deleting permissions.

#### Symbolic Notation

Symbolic notation requires you to know the existing permissions prior to specifying new permissions. Then, when you specify the new permissions, the specification is made with respect to the existing permissions. The syntax for changing permissions using symbolic notation with the `chmod` command is as follows:

```
$ chmod symbolmode filename<Enter>
```

Table 6.3 summarizes the `symbolmode` parameters. You can specify multiple symbolic modes by separating them with commas. The operations are performed in the order in which they appear (in other words, from left to right). Example 6.2, which deals with the use of symbolic parameters to change permission modes, will illustrate what we mean.

**Table 6.3 Symbolic Parameters**

| SYMBOLMODE | DEFINITION                                     |
|:-----------|:-----------------------------------------------|
| u          | Owner of the file                              |
| g          | Owner's group                                  |
| o          | Other users on the system                      |
| a          | Owner, group, and others                       |
| +          | Add the permission                             |
| -          | Remove the permission                          |
| =          | Clear the existing permission mode, then set to the mode specified |
| r          | Read permission                                |
| w          | Write permission                               |
| x          | Execute permission                             |

When you use the symbolic mode to specify permissions, the first set of parameters you specify set the permission field, as follows:

- u file owner (when discussing permissions, owner permissions are often referred to as user)
- g group
- o all others
- a owner, group, and all others

Using `a` is the same as specifying the `ugo` option. The `a` option is the default permission field. That is, if you omit the permission field, Linux defaults to the `a` option.

The second set of flags determines whether permissions are to be added, taken away, or set as specified:

- `+` adds the specified permissions.
- `-` removes the specified permissions.
- `=` clears the selected permission field and sets it to whatever follows on the command line. If you do not specify a permission mode following the `=`, then Linux will remove all permissions from the selected field.

The third set of parameters determines the permission as shown here:

- r read permission
- w write permission
- x execute permission for files; search permission for directories

To change permissions, you should first issue the `ls -l` command to check the current permission settings (that is, the current file mode). Then, you use the `chmod` command to specify the symbolic modes. Finally, it is a good idea to check these new permissions by issuing the `ls -l` command again. This procedure is followed in Example 6.2.

> **NOTE** With symbolic and numeric notation, you do not separate entries with spaces. This situation is contrary to your experience with entering commands thus far.
