
**CHAPTER PREREQUISITE**
Working with files and directories and typing at the command line; Chapter 4, “File Management,” and Chapter 5, “GNU and UNIX Commands.” The Linux filesystem and how it is organized, Chapter 3, “Linux Filesystem.”

## Permissions

### WHILE YOU READ

1. How can a file owner change ownership of files?
2. You have a directory of files containing payroll information that you want to share with other employees in the payroll department. As the system administrator, what would be the best way to do this?
3. You have a new employee, Mary, who replaced Bill. How can you give Bill’s files and directories in the *data/bill* directory to Mary?
4. One of the accounting department’s directories contain information that should be changed only by the head accountant, but should be readable by all accounting employees. How do you set the permissions?
5. How do you set the permission block on the employee evaluation files so that only the HR director can read or change them?
6. All the salespeople save their quotes to a directory called *sales/quotes*. Some of them have complained to you that files are being lost. How could you address this problem?
7. You have a user who tells you that every time he creates a new file it has its permissions set as `-rw-rw-r--`. He wants the new permissions to be `-rw-r---r---`. How can you configure his settings to make this happen?

![](img/8c0f494a2e9a2273fb49af52267f311e_223_0.png)

Lab
SEE
APPENDIX F

## Owners and Groups

The management of permissions is a complex subject that is a large part of any system administrator's job. You can count on seeing questions that address access issues both from a straightforward approach as to how to set permissions and from a troubleshooting approach. The question might not specifically state it is about permissions, but when you analyze the problem, you will see that setting appropriate permissions is the answer.

Every file has both an owner and a group whether it is a text file, directory, or device. To see the owner and group associated with a specific file, use the `ls -1` command, which produces an output like the following:

```
drw-rw-r-- 1 haddex haddex 17249 Sep 7 10:08 dict
.rw-rw-r-- 1 haddex haddex 69 Sep 7 10:25 files
```

Usually, the owner is the individual who created the file and the group is whatever group was the owner's default group when the file was created. Both the group and owner can be changed.

### Key Concept

> Every file, whether it is a directory, device, binary, or text file, has an owner and a group associated with it. A user is anyone who is not the owner or a group member.

## Changing the Owner

To change the owner of a file, use the *chown* command along with the name of the new owner. If you know the user's ID, you can use that instead of the name. Only root can change the ownership of a file. The syntax for *chown* is

```
chown [options] newowner file(s)
```

So, to change the ownership of all the files that begin with *memo* to *martinez*, while logged on as root, you would type

```
chown martinez memo*
```

Changing the owner does not change the owner's permissions. Instead, it changes only who can exercise those permissions defined for the owner.

When you run the *chown* command, it first checks to verify that you have provided a valid username by searching the */etc/passwd* file. If this check succeeds, the ownership of the file is changed. Table 9.1 shows the options that can be used with the *chown* command.

| Option | Action |
| :-- | :-- |
| -c | Displays information on all changed files |
| -v | Displays information on all files whether or not the ownership change was successful |
| -f | Does not display error messages |
| -R | Applies changes recursively down the directory tree |

## Changing the Group

Groups are merely a way to organize users. Because every file has a group associated with it and permissions can be applied to groups, groups are an excellent tool for managing access to files and directories. Groups and group management are covered in Chapter 7, “Users and Groups.”

You can change the group for a file using either the chown or chgrp command. You must be the owner or root to change a file’s group.

As the owner of a file, if you want to change a file from one group to another, you must be a member of the new group. Root, however, can change the group to any group, regardless of whether root is a member of that group.

Performing an ls -l on the file MyFile shows you the current owner and group, as in

```
-rw-rw-r--   1 haddan     user     370 Sep  5 14:42 MyFile
```

To use the chown command to change the owner and group, you must separate the owner and group names by a colon, as in the following:

```
chown martinez:wp MyFile
```

This will change the owner of the file MyFile to martinez, as well as change its group from user to wp. Now, when you perform an ls -l on MyFile you see

```
-rw-rw-r--   1 martinez wp      370 Sep  5 14:42 MyFile
```

You could have changed only the group on MyFile by issuing the following command:

```
chown :wp MyFile
```

This would have changed the group to wp without changing the owner of the file. An ls-l command would now show

```
-rw-rw-r--   1 haddan    wp      370 Sep  5 14:42 MyFile
```

Notice that the group's name must be prefaced with a colon (:) when using the `chown` command to change only the group.

The other command you can use to change the group is the `chgrp` command. The syntax of the `chgrp` command is

```
chgrp newgroup file
```

To use the `chgrp` command to change the group ownership on the files beginning with memo, you would type

```
chgrp wp memo*
```

### Key Concept

Remember, only the owner of a file or root can change the file's group. If the owner attempts to change the group, she must also be a member of the new group.

When changing a group, the `chgrp` command verifies that you have entered a valid group by searching the /etc/group file. `chgrp` has the same options as `chown`. Refer to Table 9.1.

You can use the `chown` and `chgrp` commands to change the group on multiple files by using wildcards:

```
chown :wp memo*
```

However, it will fail on any files that you do not own unless this command is executed by root.

## Accessing Files and Directories

Permissions to files are managed using the permission block, which is displayed when displaying a long listing by using the `ls -l` command. You will need to be able to interpret the permission block to answer questions pertaining to permissions. The permission block is the first 10 characters that are displayed:

```
·rwxrwxrwx·   1  hadden  hadden    39 Oct 19 18:30 ABill
·rwxrwxrwx·   1  hadden  hadden    35 Sep 6 19:47 AlphaFileList
·rwxrwxrwx·   1  hadden  hadden    69 Sep 7 10:25 FileList
·rwxrwxrwx·   1  hadden  hadden    39 Oct 19 18:28 phone
·rwxrwxrwx·   1  hadden  hadden  10240 Sep 6 12:46 catalog
·rwxrwxrwx·   1  hadden  hadden  17249 Sep 7 10:08 dict
·rwxrwxrwx·   1  hadden  hadden    69 Sep 7 10:25 files
·rwxrwxrwx·   1  hadden  hadden   169 Oct 19 20:58 flex
drwxrwxr-x 2 hadden hadden 1024 Oct 20 10:55 letters
-rw-rw-r-- 1 hadden hadden 69 Oct 19 18:28 myfile
-rwxrwxr-x 1 hadden hadden 101 Sep 6 12:46 mywhich
lrwxrwxrwx 1 hadden hadden 4 Sep 6 16:44 softday -> days
-rw-rw-r-- 1 hadden hadden 4354 Sep 7 13:48 x
```

The first character represents the file type. As discussed in Chapter 3, there are several different types (see Table 9.2).

Table 9.2 Linux File Types

| Character | File Type |
| :--- | :--- |
| - | Ordinary file |
| b | Block device |
| c | Character device |
| d | Directory |
| l | Link |

Permissions are interpreted differently depending on the file type, which is why this character is important when interpreting what permissions will be applied.

The next nine characters of the permission block define the actual permissions being applied. The characters are interpreted in three groups of three. Each group consists of read, write, and execute permissions, which are either granted or denied. The three groups are the permissions for owner, group, and all others or users.

Three basic permissions can be assigned to any file or directory, each of which is represented by a single letter:

- r (read)
- w (write)
- x (execute)

Access to files of all types is determined by assigning one or more of these permissions to that file.

Nine permissions are listed for each file immediately following the file’s type. Figure 9.1 shows the permission block and its associated user(s).

The first block represents the three permissions of the owner of that file. The second block of permissions contains the permissions of the group that owns the file and anyone who is a member of that group. The third set of permissions refers to anyone who is not the owner or a member of the specified group.
