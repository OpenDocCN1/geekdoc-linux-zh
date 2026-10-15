Permissions are normally represented in one of two ways. The first is as a string of 10 characters, the first of which indicates the file type (ordinary file, directory, and so on), the remaining 9 of which represent the permissions in groups of 3 for the owner, the group, and all other users. For instance, here are some sample files:

```
-rwxr-xr-x 1 rodsmith users 10572 Jun 19 12:44 vplay
-rw-r--r-- 1 rodsmith users 2598 Jun 20 13:18 wp-fontinstall.txt
drwxr-x--- 2 rodsmith users 2048 Jul 1 11:00 wp-icons
```

The first file, vplay, is a program file—its permission string -rwxr-xr-x indicates that it has execute (x) permission for the owner, the group, and all users. (Dashes indicate no permission, and r, w, and x indicate read, write, or execute permission, respectively.) The second file, wp-fontinstall.txt, is a text file with read and write permission for both the owner and the file's group (users), and read-only access for all others. The third file, wp-icons, is actually a directory (indicated by the d in the first field of the permissions string) with read and write access for the owner, read access for members of the users group, and no access for others.

Execute permission carries a special meaning for directories: It means that the directory's contents are accessible. If a directory can be read but not executed, you can find some information about the contents, but you can't access the files in the directory. If the directory can be executed but not read, you can't obtain a directory listing, but you can access the files in the directory if you know their filenames. Thus, directories normally have both read and execute permission. To restrict access to a directory, you need to remove both execute and read permissions.

The second way to represent permissions is as a three- or four-digit octal (base 8) number, such as 754 or 0754. Each octal digit is 3 bits in size, and can be expressed as a binary number; for instance, 7 is 111, 5 is 101, and 4 is 100. Link the binary representations together, and you have a permissions string, with 0 equivalent to a dash (-) and 1 equivalent to whatever character is appropriate for the position in question. For instance, 754 is equivalent to -rwxr-xr--. (The leading digit in the 4-digit representation carries special meaning. Aside from to represent directories, you don't normally need to concern yourself with it, and even the directory coding is handled automatically.)

From within Linux, you can alter ownership and permissions with the chown, chgrp, and chmod commands:

+   - chown—Changes the ownership of the file, and optionally the group. Type chown user.name.group filename to do this. You can omit the period and group name if you want to change only the username.

+   - chgrp—Changes the group association of the file. This command works much like chown.