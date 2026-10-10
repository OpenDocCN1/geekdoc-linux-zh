| Command | Description |
| :--- | :--- |
| mkdir | Creates directories |
| rmdir | Removes empty directories |
| mv | Moves/renames files and directories |
| cp | Copies files and directories full of files (with the -R option) |
| alias | Displays BASH shell aliases |
| rm | Removes files and directories full of files (with the -R option) |

Table 4-2 Common Linux file management commands

# # Finding Files

Before using the file management commands mentioned in the preceding section, you must know the locations of the files involved. The fastest method to search for files in the Linux directory tree is to use the **locate command**. For example, to view all of the files underneath the root directory with the file name “inittab” or with “inittab” as part of the filename, you can simply type `locate inittab` at a command prompt, which produces the following output:

```
[root@server1 ~]# locate inittab
/etc/inittab
/usr/share/vim74/syntax/initab.vim
[root@server1 ~]# _
```

The **locate** command looks in a premade database that contains a list of all the files on the system. This database is indexed much like a textbook for fast searching, yet can become outdated as files are added and removed from the system, which happens on a regular basis. As a result, the database used for the **locate** command ( `/var/lib/mlocate/mlocate.db` ) is updated each day automatically and can be updated manually by running the **updatedb** command at a command prompt. You can configure the directories that are searched by the **updatedb** command by editing the `/etc/updatedb.conf` file.

As the **locate** command searches all files on the filesystem, it returns too much information to display on the screen. To make the output easier to read, you can use the **more** (or **less**) command to pause the output, as in `locate initab | more`. To prevent the problem entirely, you can do more specific searches.

A slower yet more versatile method for locating files on the filesystem is to use the **find command**. The **find** command does not use a premade index of files; instead, it searches the directory tree recursively, starting from a certain directory for files that meet a certain criterion. The format of the **find** command is `find <start directory> -criteria <what to find>`.

For example, to find any files named “inittab” underneath the `/etc` directory, you can use the command `find /etc -name inittab` and receive the following output:

```
[root@server1 ~]# find /etc -name inittab
/etc/inittab
[root@server1 ~]# _
```