
This makes the file readable and writable only by you because you've enabled read (4) + write (2) for yourself and no one else. To change the file permissions back to the original access permissions, you would want to enable read (4) + write (2) for you (6) and your group (6) and read-only permissions for all others (4), and use the octal number 664:

```
# chmod 664 afile
# ls -l afile
-rw-rw-r-- 1 bball users 0 Dec 26 14:50 afile
```

You can also change file directory permissions and either let other people list the contents of your directory or have access only to the files in a directory and not be able to list the directory contents. For example, to protect a directory from prying eyes (again, from everyone but the root operator), you can try

```
# mkdir temp
# cd temp
# touch file1 file2 file3
# cd ..
# chmod 700 temp
# ls -ld temp
drwx------ 2 bball users 1024 Dec 26 14:52 temp
```

If anyone else tries to look into your directory, they will see

```
# ls /home/bball/temp
ls: /home/bball/temp: Permission denied
```

What if you want to allow others to read files in the directory without being able to list the contents? To do this, you can enable execute permission of your directory:

```
# chmod 711 temp
# ls -ld temp
drwx--x--x 2 bball users 1024 Dec 26 14:52 temp
```

Now, no other users will be able to list the contents of your directory but can read files that you tell them are within. For example:

```
# ls -l /home/bball/temp
ls: /home/bball/temp: Permission denied
# ls -l /home/bball/temp/file1
-rw-r--r-- 1 bball users 0 Dec 26 14:52 /home/bball/temp/file1
```

As you can see, using the chmod command's octal notation is not hard. What you have to decide is to whom you want to grant access and what kind of access you'd like your files to have. The chmod command also has a command-line form:

```
ugoa +- = rwxXsugo
```

This book doesn't go into all the details of this notation (you can read the chmod command's manual page for more details), but the next few examples duplicate chmod's actions using the previous examples. You can protect a file from anyone else with

```
# ls -l file1
-rw-r--r-- 1 bball users 0 Dec 26 14:52 /home/bball/temp/file1
# chmod go-rwx file1
# ls -l file1
-rw------- 1 bball users 0 Dec 26 14:52 file1
```

As you can see, the file is now readable and writable only by you because you have specified that your group (g) and others (o) do not (-) have read, write, or execute (rwx) permission. Now, you can protect your directory from prying eyes as follows:

```
# chmod go-rwx temp
```

To mimic the last example, to enable others to read files in the directory but not list the directory contents, you can use

```
# chmod go+x temp
```

You're now familiar with file and directory permissions and using the chmod command. The next section shows how you can change ownership of files or directories using the chown command.

## Changing File Ownership with the chown Command.

The chown (change ownership) command, found in the /bin directory, is used to change, either permanently or temporarily, the ownership of files or directories. If you recall the previous discussion of the /etc/group file in this hour, you'll remember that your users can be assigned to different groups. Using the chown command, you can assign ownership to different users or groups, permitting reading, writing, or deletion of files and directories.

For example, if you've created a text file, you can share it with members of your group or others with the chmod command. By using chown, you can tell Linux specifically what other users or groups can have access to your file. You can use the groups command to find out what groups you belong to:

```
# groups
users
```

This shows that the user, bball, belongs to the group users. As the root operator, you belong to the group root, for example:

```
# groups
root
```

To find out who belongs to a group, look at the /etc/group file, or use the name of a user:

```
# groups cloobie
cloobie : users
```

This shows that cloobie belongs to at least one group, called users. To assign one of your files to the users group, and give cloobie access, you can use the chown command's syntax of user:group:

```
# chown :users myfile
# ls -l myfile
-rw-r--r-- 1 bball users 0 Dec 26 15:19 myfile
```

You might think that to assign specific ownership, you can use the following:

```
# chown cloobie:users myfile
chown: myfile: Operation not permitted
```

What happened? This shows why Linux has groups. You can assign access of one of your files to a group, but unless you're the root operator, you cannot assign one of your files to appear to have been either created by or owned by another user. Make sure you're logged in as the root operator, and use

```
# chown cloobie:cloobie myfile
# ls -l myfile
-rw-rw-r-- 1 cloobie cloobie 0 Dec 26 15:19 myfile
```

As you can see, even though the file myfile was created by the user bball, as the sysadmin, you can assign ownership to any users and any group. If you just want to change the group ownership of a file or directory, you can use the chgrp command, and if you want to change your users or your own group, you can use the newgrp command.

## Changing Groups and Ownerships with the chgrp and newgrp Commands

The chgrp (change group) command, found in the /bin directory, is used only to change group ownerships. In this regard, it is not as flexible as the chown command, which can do both. The chgrp command accepts a group name or group ID (GID), for example:

```
# ls -l myfile
-rw-r--r-- 1 bball users 0 Dec 26 15:26 myfile
```

This shows that the file belongs to user bball and group users. To change the group ownership and grant access to other members of the group, use

```
# groups bball
bball : bball users
# chgrp users myfile
# ls -l myfile
-rw-rw-r-- 1 bball users 0 Nov 23 14:16 myfile
```

Now, other members of the users group can access the file. Along with the chgrp command, you can use the newgrp command, which is found in the /usr/bin directory. Although the chgrp command will change group ownership of one of your files or directories to a group you belong to (or if you're the root operator, any group), you can use newgrp to shift your current group membership:

```
# groups
bball users
# touch file1
# ls -l file1
-rw-rw-r-- 1 bball bball 0 Nov 23 14:53 file1
# newgrp users
# groups
users bball
# touch file2
# ls -l file2
-rw-rw-r-- 1 bball users 0 Nov 23 14:54 file2
# newgrp bball
```

This shows that the user bball originally belonged to the default group bball. This was verified by creating a file showing the current user and group ownership. Next, the user bball changed to the users group, created a file, and verified that the created file has the new group's access. Finally, the user bball changed back to the original group, bball.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_519_0.png)

> > The newgrp command will launch a new shell, and you must use the shell's exit command to return to your original prompt. If you only need to run a single command as the member of a different group, use the sg command, which will not replace your shell.

As you can see, Linux offers you a great deal of flexibility in assigning file ownerships and permissions. By using different combinations of directory and file ownership and permissions, you can organize your system along lines of types of work, types of users, or types of files.

## Managing Linux Software with rpm, lisa, and kpackage

Software installation and removal under OpenLinux is accomplished with the Red Hat Package Manager, or rpm command. The rpm command works by using software packages and databases of installed software for your system under the /var/lib/rpm directory. A software package is an archive of files, information, and scripts used before and after files are decompressed and saved into your file system. The rpm command, its databases, and the format of the software packages are the backend system for front-end utilities such as lisa and the kpackage client.

This section introduces you to the rpm command and then shows you how to use the kpackage client and the lisa command to install or remove software.

### Using the rpm Command

You use the rpm command to install, query, upgrade, uninstall, and verify software. What makes rpm so handy is that you can use it to easily track what software is installed and which version of a software package is installed and then upgrade the software package, and if desired, uninstall the software—all with a single command line!

The rpm command has many different command-line options, but most users will only use five of its options, or modes:

- -i, or install
- -e, or uninstall
- -q, or query
- -U, or upgrade
- -V, or verify

To install a software package (usually with a filename ending in .rpm), use the -i option, followed by the name of a software package. Software package names usually include the name of the program, its version, what computer platform the software is designed for, and an .rpm extension. You must be logged in as the root operator or have root permission before installing or removing software. For example, to install the taper backup software package from your OpenLinux CD-ROM, insert and mount the CD-ROM and then use rpm:

```
# rpm -i /mnt/cdrom/Packages/RPMS/taper-6.8.2-2.1386.rpm
```
