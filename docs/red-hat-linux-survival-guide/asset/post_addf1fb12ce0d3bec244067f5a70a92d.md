
command to mount it. You should be able to access the floppy from the /mnt/floppy directory. If you're using the X Window System and are utilizing a graphical environment such as GNOME, simply insert the disk into the disk drive and double-click the floppy disk icon to view the contents of the floppy disk.

## Determining a file’s type with file

Unlike Windows, Linux does not rely on file extensions to determine file types. In Linux, you use the file command to determine a file’s type. For example, the following command shows what type of file /usr/bin/file (itself) is:

```
file /usr/bin/file
```

Here is an example of the output of this command:

```
/usr/bin/file: ELF 32-bit LSB executable, Intel 80386, \
version 1, dynamically linked, not stripped
```

## Viewing the access statistics of a file or directory with stat

You can use the stat command to get statistics on a file or directory. The syntax for the stat command is stat file_or_directory_path. For example, the following command shows statistics on the /tmp directory:

```
stat /tmp
```

Here is an example of its output:

```
File: "/tmp"

    Size: 2048      Filetype: Directory

    Mode: (1777/drwxrwxrwt)     Uid: (  0/ root)   Gid: (  0/ root)

Device: 3,0   Inode: 16321      Links: 22

Access: Sun Feb  7 02:00:35 1999(00000.00:01:11)

Modify: Sun Feb  7 02:01:01 1999(00000.00:00:45)

Change: Sun Feb  7 02:01:01 1999(00000.00:00:45)
```

## Copying files and directories with cp

Use the cp command to copy files from one location to another. For example, the following command copies a file called important.txt from the /some directory to the /new/place directory:

```
cp /some/important.txt /new/place/
```

![](img/9eb7e89292d2f85707b4d49102c865b7_200_0.png)

You can also specify a new destination filename, if necessary, by adding a new filename to the end of the destination path in the command.

To copy a file to a location where another file exists with the same name, you can force cp to copy over the existing file with the -f option. For example, the following command copies the important.txt file even if a file by that name is already in the /new/place directory:

```
cp -f /some/important.txt /new/place/
```

To copy a directory along with all of its files and subdirectories, use the -r option to copy the directory recursively. The syntax of the command is cp -r source_directory destination_directory. For example, the following command copies the /tmp/foo directory along with the contents of the directory itself and all of its subdirectories to the /zoo/foo directory:

```
cp -r /tmp/foo /zoo/foo
```

## Moving files and directories with mv

To move files or directories, use the mv command. The syntax for mv is mv original_path new_path. For example, the following command moves /file1 to /tmp/file2:

```
mv /file1 /tmp/file2
```

Similarly, you can move a directory recursively along with all of its contents. To do this, use cp with the -r option to copy the directory to the new file system, and then remove the directory (see the next section) from the current location.

![](img/9eb7e89292d2f85707b4d49102c865b7_201_0.png)

mv does not move directories across different file systems. When you need to move a directory from one file system to another, copy the directory by using the cp command with -r flag, as discussed above, and then you can remove the old directory using the rm command, as discussed below.

## Deleting files and directories with rm

To delete a file or directory, use the rm command. The syntax for the rm command is rm file_or_directory_name. For example, the following removes a file called letter.txt:

```
rm letter.txt
```

To remove a directory’s contents recursively, you need to specify the -r option. You can use the -f option to force a removal. For example, the following command removes all the files and subdirectories within the specified directory:

```
rm -rf directory
```

![](img/9eb7e89292d2f85707b4d49102c865b7_201_1.png)

You may set an alias called rm as follows:

```
alias rm 'rm -i'
```

In such a case, the -i option tells the command to prompt you before actually deleting anything.

## Working with Permissions

Permissions allow for security on multiuser systems. In this section I discuss the basics of permissions and some of the common tools with which you can change permissions. I also give you a few sample permission policies that you can either use as-is or customize as you require.

### Understanding file and directory permissions

Linux associates a file or directory with a user and a group, just as all other Unix and Unix-like operating systems do. The term permissions refers to the aspects of a file that determine who has access to read it, write to it, and execute it (for executable files).

By default, the permissions of the file belong to the file’s owner. When a new file is created, the file owner is the file creator, and the group is the owner’s default group. In Red Hat Linux, when a user creates a file or directory, its group is also set as the default group of the user, which happens to be a private group with the same name as the user.

As a regular user, you cannot reassign a file’s or a directory’s ownership to someone else. For example, I cannot create a file as user kabir and reassign its ownership to a user called sheila. The reason for this strict permission structure is security. If a regular user were allowed to reassign file ownership to others, someone could create a nasty program that deleted files, change the program’s ownership to the superuser, and then wipe out the entire file system. So, only a superuser (such as the root user) can reassign file or directory ownership.

You can check the permissions of a file or directory with the ls -l command. For example, to check the permissions for the milkyweb.txt file you would use the ls -l milkyweb.txt command. For example, if user sheila logs into a Red Hat Linux system and uses the ls -l milkyweb.txt command, the following output (or similar) appears:

```
-rw-rw-r-- 1 sheila intranet 512 Feb 6 21:11 milkyweb.txt
```

You can see the following from the preceding output:

- The milkyweb.txt file is owned by a user called sheila.
- As the file’s owner, sheila is the only regular user who can change the access permissions of this file. The only other user who can change the permissions is the superuser.
- The group for this file is intranet.
- Any user who belongs to the intranet group can access (that is, read, write, or execute) the file based on what current group permission is set (by the owner).

Check out how Table 8-4 breaks down the output above piece by piece.

### Table 8-4 Output of an Example ls -l Command

| ls Output | Information Type |
|---|---|
| -rw-rw-r-- | File access permissions |
| 1 | Number of links |
| sheila | User (file owner) |
| intranet | Group |
| 512 | File size (in bytes) |
| Feb 6 | Last modification date |
| 21:11 | Last modification time |

### Managing file and directory permissions

The following sections show you how to use some of the more common command line tools to easily manage permissions.

### Changing file or directory ownership

As root (or as another superuser), you can change the ownership of a file or directory by using the chown command. To change the ownership of a file or directory, run the command as follows:

```
chown newuser file_or_directory
```

For example, the following command makes user sheila the new owner of the file kabirs_plans.txt

```
chown sheila kabirs_plans.txt
```

As root (or another superuser), you can change the group for a file or directory with the chown command at the same time as you change the ownership of the file or directory, as follows:

```
chown newuser.newgroup file_or_directory_name
```

For example, the following not only makes sheila the new owner but also resets the group of the file to be admin:

```
chown sheila.admin kabirs_plans.txt
```

To change the user and/or group ownership of all the files or directories under a given directory, a superuser (such as root) can use the -R option to run the chown command in recursive mode. For example, the following command changes the user and group ownership of the /home/kabir/plans directory and all the files and subdirectories within it:

```
chown -R sheila.admin /home/kabir/plans/
```

### Changing group ownership of file or directory

Although you have to be the superuser to change the ownership of a file, you can still change a file's or directory's group as a regular user by using the chgrp command. The chgrp command lets you change the owner of a file or directory as long as you are also part of the new group.

In other words, you can change groups only if you belong to both the old and new groups or if you are a superuser. For example, if you run the following command to change the group for all the HTML files in a directory, you must also be part of the httpd group:

```
chgrp httpd *.html
```

You can find out what groups you belong to by using the groups command without any argument.

![](img/9eb7e89292d2f85707b4d49102c865b7_204_0.png)

Like the chown command, chgrp also uses -R to recursively change group names of one or more files or directories.

### Using octal numbers to set permissions

Although using octal numbers is my favorite method for setting file or directory permissions, I must warn you that it involves 1s and 0s. If you feel you are mathematically challenged, skip to the next section, which explains how to set the same permissions using a much simpler access string.
