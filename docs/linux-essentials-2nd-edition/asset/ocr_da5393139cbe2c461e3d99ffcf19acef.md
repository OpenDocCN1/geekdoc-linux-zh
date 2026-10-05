# Chapter 7 • Managing Files

# TABLE 7.2 (Continued)

| Option (long form) | Option (short form) | Description |
| --- | --- | --- |
| --directory | -d | Normally, if you type a directory name as an option, ls displays the contents of that directory. The same thing happens if a directory name matches a wildcard. Adding this parameter changes this behavior to list only the directory name, which is sometimes preferable. |
| 
| N/A | -l | The ls command displays filenames only. The -l parameter (lowercase l) produces a long listing that includes information such as the file's permission string, owner, group, size, and creation date. |
| --classify | -F | This option appends an indicator code to the end of each name so you know what type of file it is. |
| --recursive | -R | The -R --recursive causes ls to display directory contents recursively: if the target directory contains a subdirectory, ls displays both the files in the target directory and the files in its subdirectory. The result can be a huge-list if a directory has many subdirectories. |

You may optionally give ls one or more file or directory names, in which case ls displays information about files or directories, as in this example:

```
$ ls -F /usr /bin/bin/ls
/bin/ls
```

```
/usr/
X11R6/ games/ include/ man/ src/
bin/ i386-glibc20-linux/ lib/ merge/ tmp/
doc/ i486-linux-libc5/ libexec/ sbin/
etc/ i586-mandrake-linux/ local/ share/
```