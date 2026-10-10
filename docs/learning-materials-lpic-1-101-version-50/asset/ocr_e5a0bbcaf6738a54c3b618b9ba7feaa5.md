The first character in the output indicates the file type:

+   -
+       for a regular file.

+   **d**
+       for a directory.

+   **c**
+       for a special file.

To show the file sizes in a human readable format add the option `-h`:

```
$ ls -lh
total 60K
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Desktop
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Documents
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Downloads
-rw-r--r-- 1 frank frank 21 Sep 7 12:59 emp_name
-rw-r--r-- 1 frank frank 20 Sep 7 13:03 emp_salary
-rw-r--r-- 1 frank frank 8.8K Apr 1 2018 examples.desktop
-rw-r--r-- 1 frank frank 10 Sep 1 2018 file1
-rw-r--r-- 1 frank frank 10 Sep 1 2018 file2
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Music
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Pictures
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Public
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Templates
drwxr-xr-x 2 frank frank 4.0K Apr 1 2018 Videos
```

To list all files including hidden files (those starting with .) use the option `-a`:

```
$ ls -a
.                .dbus     file1      .profile
..               Desktop   file2      Public
.bash_history    .dmrc     .gconf     .sudo_as_admin_successful
```

Configuration files such as `.bash_history` which are by default hidden are now visible.

In general, the `ls` command syntax is given by: