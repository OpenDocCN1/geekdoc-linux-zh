Here, ending characters are used to distinguish files and folders.

+   *   "/" suggest directory.
+   *   "\*"suggest executables.
+   *   "@" suggest symbolic links.

To get more details about the files and directories, use `ls -l`

```
user@Ubuntu14:~/example$ ls -l
total 6464
-rw-r--r-- 1 dave dave      41 Dec 24 12:19 Z.txt
drwxr-xr-x 2 user group   4096 Dec 24 12:00 a_directory
-rw-r--r-- 1 user group      6 Dec 24 12:01 a_file
lrwxrwxrwx 1 user group      6 Dec 24 12:04 a_link -> a_file
-rw-r---r-- 1 user group      6 Dec 24 12:03 a_newer_file
-rw-r----- 1 user group 6586816 Dec 24 12:07 big.zip
```

In this example, the total size of the contents is 6460KB.

Then there is an entry for each file/directory in alphabetical order with upper case before lower case.

The first character is the type (e.g. d - directory, l - link).

The next 9 characters show the permissions for the user, group and other.

This is followed by the number of hard links, then the owner's name and group.

The next field is the size in bytes. This can be displayed in a human friendly form by adding the -h option e.g. 6586816 is displayed as 6.3M

There then follows a timestamp (usually the modification time).

The final field is the name. Note: links also show the target of the link.