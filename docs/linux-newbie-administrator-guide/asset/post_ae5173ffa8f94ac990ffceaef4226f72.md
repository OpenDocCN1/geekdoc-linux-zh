
removed (erased) only the owner of the file, or a member of the group that owns the file, or the root.
Yet other users may be able to modify or erase the content of the file if they are given the permission to do so--read on. The owner and group that owns the file will be shown in the output from the ls -1 command ("list in the long format"). For example, the command:

```
ls -1 junk
```

produced this output on my screen:

```
-rwx------ 1 yogin inca 27 Apr 24 14:12 junk
```

This shows the file "junk," belonging to the owner "yogin" and to the group "inca".

The ownership of a file can be changed using the commands chown (change owner) and chgrp (change group), which are normally executed by root:

```
chown peter junk
chgrp peter junk
ls -1 junk
```

After executing the above 3 lines, the command ls -l junk produces this output on my screen:

```
-rwx------ 1 peter 27 Apr 25 20:27 junk
```

Changing the file ownership comes if you move/copy files as root for use by other users. At the end of your housekeeping you typically want to hand-in the file ownership to the user.

**File Permissions.** Now, an owner of a file can make the file accessible in three modes: read (r), write (w) and execute (x) to three classes of users: owner (u), members of the group (g), others on the system (o). You can check the current access permissions:

```
ls -l filename
```

If the file is accessible to all users (owner, group, others) in all three modes (read, write, execute) it will show:

```
-rwx-xr-x
```

Skip the first "-" (it shows "d" for directories, "-" for normal files, "l" for links, "c" for character dev, "b" for block devices). After this initial character, the first triplet shows the file permission for the owner of the file, the third triplet shows the permissions for other users. A "no" permission is shown as "-". Here is output from the ls -1 command on a file that is owned by root, for which the owner (root) has all permissions, but the group and other can read and execute:

```
drwxr-xr-x 2 root root 21504 Apr 24 19:27 dev
```

The first letter "d" shows that the file is actually a directory.

You can change the permissions on the file which you own using the command chmod=("change mode"). For example, this command will add the permission to read the file "junk" to all (=user=group+others):

```
chmod a+r junk
```

In the command above, instead of "a" ("all"), I could have used "u", "g" or "o" ("user", "group") or "others". Instead of "+" ("add the permission"), I could have used "-" or "=" ("remove the permission" or set the permission). Instead of "r" ("read permission"), I could have used "w" or "x" ("write permission" or execute permission).

For example, this command will remove the permission to execute the file "junk" from others:

```
chmod o-x junk
```

Instead of lists, one can also use numbers to specify the permissions. To understand how it works look at this:

```
read=4
write=2
execute=1
```

The total permission for a class of users is the sum of the three. Thus:

- 1 = execute only (seems unusual)
- 2 = write only (seems unusual)
- 3 = write and execute (seems unusual)
- 4 = read only (common)
- 5 = read and execute (common)
- 6 = read and write (common)
- 7 = read, write and execute (common).

The permission for all the three classes of users (owner, group, others) is obtained by gluing the three digits together one by one. For example, the command

```
chmod 770 junk
```

will give the owner and his/her group the complete of permissions, but no permissions to others. The command:

```
chmod 666 junk
```

gives all three classes of users (owner, group, others) the permissions to read and write (but not execute) the example file named "junk". Please note the "666". It is quite often used, and at least one person I know, it is a proof that Linux (any UNIX for that matter) is a work of the devil >:-.

This command:

```
chmod 411 junk
```

would give the owner the permission to read only, and the group and others to execute only. This one does not seem useful, but might be funny, at least for North American Linux users who 411 (telephone number) for directory assistance. Mail me if you can think of any other funny permissions (maybe 0077).

The numerical way of representing file permissions is called "octal" because the numbers have base 8 (the decimal system base is 10). The highest digit in the system is 7 (octal system has eight digits: 0 to 7, analog to decimal system having ten digits: 0 to 9). The octal representation is a convenient notation for the binary representation of file permissions, where each permission is flagged as "set" or "denied" with a one or zero and the total is represented as a string of zeros and ones, in this diagram:

```
user class: owner group others
example permissions: rwx rw-- r---
absent permissions: --x -wx
binary representation of the binary: 111 110 100
octal representation: 7 6 4
```

Default file permissions with umask. When a new file is created, it is given default permissions. On my system, these are:

```
-rw-r--r--
```

This means that files created by a user can be read and written to the user, but only read by his/her group and others. Still, on my RH5.2 system, users cannot read the files in the other users' home directories because the permissions on the home directories is:

```
drwx------
```

I can check the default file permissions given to my newly created files using:

```
umask -S
```

(The option "-S" stands for "symbolic" and tells umask to display the permissions in an easy-to-read form.)

I can change the default file permissions given to my newly created files using:

```
umask -S
```

(The option "-S" stands for "symbolic" and tells umask to display the permissions in an easy-to-read form.)

I can change the default file permissions given to my newly created files using:

```
umask -S
```

(The option "-S" stands for "symbolic" and tells umask to display the permissions in an easy-to-read form.)
