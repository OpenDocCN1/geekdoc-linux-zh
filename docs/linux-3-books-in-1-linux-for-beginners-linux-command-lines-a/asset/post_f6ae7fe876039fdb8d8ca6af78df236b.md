
Let us go through the most common commands.

The **date** command will display the current date and time that has been set on your Linux system. You can also use the same command to set a new date and time if required. The command can be followed up with a + sign as an argument if you want to display the date and time in a specific format.

```
[student@desktop ~]$ date

Sat Aug 5 08:15:30 GMT 2019

[student@desktop ~]$ date +%R

08:15

[student@desktop ~]$ date +%x

08/05/2019
```

The **passwd** command is used to change the password for a user in the Linux system. The command will request you to enter the user’s existing password before it allows you to set a new password. The Linux system expects a strong password comprising letters in upper and lower case, numbers, and symbols. Moreover, the password cannot be a dictionary word. A non-root user can only change their password through the command line. A root user has the right to change any user’s password through the command line.

```
[student@desktop ~]$ passwd

Changing password for user student.

Changing password for student.

(current) UNIX password: type old password here

New password: Specify a new password here

Retype new password: Type new password again

passwd: all authentication tokens updated successfully.
```

As opposed to file formats in Windows, files in the Linux file system are not specified using any extensions. You can still use the **file** command if you wish to know the format of any file. The file needs to be passed along with the command as an argument.

```
[student@desktop ~]$ file /etc/passwd
/etc/passwd: ASCII text
```

If you pass a directory instead of a file to this command, the output will tell you that it is a directory.

```
[student@desktop ~]$ file /home
/home: directory
```

You can use the **head** and **tail** command to print the first 10 lines or the last 10 lines of a file, respectively. These commands also take the **-n** option that can be used to specify a custom number of lines to be output.

```
[student@desktop ~]$ head /etc/passwd
```

This command will print the first 10 lines of the passwd file.

```
[student@desktop ~]$ tail -n4 /etc/passwd
```

This command will print the last four lines of the passwd file.

You can pass a file as an argument with the **wc** command to get the number of lines, words, and characters in a file. The command supports the **-l, -w, -c** options that represent lines, words, and characters, respectively.

```
[student@desktop ~]$ wc /etc/passwd
40    80    2000 /etc/passwd
```

This shows that the passwd file has 40 lines, 80 words, and 2000 characters.

As you can see, if you do not specify any option with the wc command, the output shows everything. If you pass a particular option with the command, it will only show the output for only that particular parameter.

The **history** command will show you all the commands that you have typed in the past. These commands will also have a number next to them. You can then type ! with the command number to know the complete command that was typed by you.

```
[student@desktop ~]$ history
1 clear
2 who
3 pwd
[student@desktop ~]$ !3
/home/student
```

You can see that !3 expanded the entire command for pwd and even showed the output for the user’s present working directory.

You can use the keyboard arrow keys to navigate through the output of the history command. The up arrow key takes you to the commands on top, while the down arrow key takes you to the commands below. The left and right arrow keys will help you edit the command that you are on at present.

## File Management Through the Command Line

This section will go through some important commands that will help you manage files and directories on Linux. You will learn commands that will let you create, delete, copy, move, and organize files and directories.

### Linux File System Hierarchy

To understand the Linux file system properly, you need to understand the Linux file system hierarchy first. The Linux file system hierarchy visually looks like an inverted tree with the root at the top and then branching downwards to form other parts.

The root directory is represented as / and is located at the top of the file system hierarchy. The / character is also used to represent file paths in Linux. For instance, **var** is a subdirectory under the root directory and is represented as /var. Similarly, there is a subdirectory called **log** under the var directory, and its path is represented as /var/log.

The root directory has a particular set of subdirectories under it that store specific files. For instance, the **boot** subdirectory will have files that are responsible for the boot process of the Linux system.

Let us go through the main subdirectories under the root directory.

- **/usr**

This subdirectory has files of software that is common to all users. It is further subdivided as follows.

- /usr/bin: User command files
- /usr/sbin: Commands used in system administration
- /usr/local: Files of software that has been customized locally

- **/etc**

Files related to system configuration are stored in this subdirectory.

- **/var**

This subdirectory stores files that change dynamically, such as databases, logs, etc.

- **/run**

Certain files that get created during runtime are stored in this subdirectory. These files will get recreated again on the subsequent boot.

- **/home**

This subdirectory has all the different users of the Linux system listed under it. Every user has their particular home directory as well. A user can store all their data under their home directory. A user cannot access the home directory of another user.

- **/root**

This is the home directory for the root user, and no one other than the root user can access it.

- **/tmp**

As the name suggests, this subdirectory stores all temporary files. If files in this directory are older than ten days and haven't been accessed, the system deletes them automatically. A similar directory exists at /var/tmp that has temporary files too. The files here, if not accessed in the last 30 days, get deleted automatically.

- **/dev**

Hardware devices on the Linux system are stored as files under this subdirectory.

### File and Directory Management

Managing a file or a directory on the Linux operating system refers to creating, modifying, and deleting files or directories. Let us go through the common commands that are used to manage files and directories in Linux.

| Activity | Single Source | Multiple Source |
| :--- | :--- | :--- |
| Copy file | cp file1 file2 | cp file1 file2 file3 dir |
| Move file | mv file1 file2 | mv file1 file2 file3 dir |
| Delete file | rm file1 | rm -f file1 file2 file3 |
| Create directory | mkdir dir | mkdir -p par1/par2/dir |
| Copy directory | cp -r dir1 dir2 | cp -r dir1 dir2 dir3 dir4 |
| Move directory | mv dir1 dir2 | mv dir1 dir2 dir3 dir4 |
| Delete directory | rm -r dir1 | rm -rf dir1 dir2 dir3 |

```
mv file1 file2
```

This command renames file1 to file2

```
cp -r dir1 dir2
```

This command will copy the contents of dir1 to dir2

```
rm -r dir1
```

This command will delete the contents of dir1

-r is used to process the source directory recursively

```
mv dir1 dir2
```

This command will copy the contents of dir1 to dir2 if dir2 exists. If dir2 does not exist, dir1 will be renamed to dir2

```
cp file1 file2 file3 dir
mv file1 file2 file3 dir
cp -r dir1 dir2 dir3 dir4
mv dir1 dir2 dir3 dir4
```

Files or directory contents are copied or moved to the directory specified at the end.

```
rm -f file1 file2 file3
```

```
rm -rf dir1 dir2 dir3
```

This command deleted the files or directories. Kindly use this carefully as the -f uses a force option will delete everything without any confirmation prompt

```
mkdir -p par1/par2/dir
```

The command will create new directories. Kindly use this carefully as using -p will keep creating directories starting from the parent and irrespective of typing errors

Let us see through examples how these commands work.

### Directory Creation

You can use the **mkdir** command to create directories and subdirectories. The directory should be created without issue as long as the specified name does not exist or the parent directory is specified properly. If not, then you will get an error. If you use the **-p** option while creating directories, the parent directory will get created if it does not exist. You need to be careful with this
