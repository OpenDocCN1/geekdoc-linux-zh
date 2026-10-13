```
# cp file2 xfile

# ls -l
total 672
-rw-r--r-- 1 root other 103306 Apr 13 20:48 file1
-rw-r--r-- 1 root other 103306 Apr 13 20:48 file2
-rw-r--r-- 1 root other 103306 Apr 13 20:48 xfile

# cp xfile /tmp

# ls -l /tmp
total 1496
-rw------- 1 daemon other 19521 Apr 6 00:52 ab2.socat.cache
-rw-r--r-- 1 root other 103306 Apr 6 02:10 comp
-rw-r--r-- 1 root other 307892 Apr 4 18:57 dtdbcache_0
-rw-r--r-- 1 root other 103306 Apr 13 20:49 file1
-rw-r--r-- 1 root other 103306 Apr 13 20:49 file2
-rw-r--r-- 1 root other 5032 Apr 4 18:56 fs_data
-rw-r--r-- 1 root other 200 Apr 9 00:45 svsdtouchck390
-rw-r--r-- 1 root other 103306 Apr 13 20:49 xfile
#
```

# Moving and Renaming Files by Using the mv Command

The mv(1) command can be used to

+   - Move one or more files to another directory.
+   - Rename a file in the current directory.
+   - Move a file to another directory and rename it in the process.

When you’re moving one or more files, the last command-line argument is the target directory and all preceding command-line arguments are the files to be moved. The files to be moved can be complete filenames, multiple files selected with metacharacters, or any combination. The filenames must be separated by spaces, as shown in this example:

```
# ls -R /test
/test:
Solaris

/test/Solaris:
8

/test/Solaris/8:
310-011  310-012  sysadmin

# mv /test/Solaris/8/310-* /test/Solaris/8/sysadmin

# ls -R /test
/test:
Solaris

/test/Solaris:
8
```