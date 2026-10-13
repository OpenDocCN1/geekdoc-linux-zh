# Hour 3

+   1. Invisible files are files with names that start with the . character. You can list them by specifying the -a option to ls.
+   2. No. Each of these commands will produce the same results.
+   3. On Solaris, HPUX and BSD (including MacOS X), use the command
+      `$ wc -ln`
+      On Linux use the command
+      `$ wc -lc`
+   4. (b) and (c) will generate error messages indicating that homework is a directory.

# Hour 4

+   1. (a) and (d) are absolute pathnames. (b) and (c) are relative pathnames.
+   2. The pwd command will output the full path to your home directory.
+   3. The following command will work:
+      `cp -r /usr/local /opt/pgms`
+   4. The following commands will work:
+      `cp -r /usr/local /opt/pgms ; rm -r /usr/local`
+   5. No, you cannot use the rmdir command, because the directory is not empty. You can use the following command:
+      `$ rm -r backup`

# Hour 5

+   1. The file descriptors associated with STDOUT, STDERR, and STDIN are 0, 2, and 1 respectively.
+   2. You can use the following printf statements:
+      `printf "%o %o %o \n" 16 255 65535`
+      `printf "%x %x %x\n" 16 255 65535`
+   3. The output ends up in the file out.txt.

# Hour 6

+   1. The file types of these files are
+      `/dev/rskc0t1d0`          character special file
+      `/etc/passwd`             regular file