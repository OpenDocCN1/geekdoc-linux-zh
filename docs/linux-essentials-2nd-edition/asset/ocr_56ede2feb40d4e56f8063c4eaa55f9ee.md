# Navigating Files and Directories

This output shows both the /bin/ls program and the contents of the /usr; the latter consists mainly of subdirectories, indicated by a trailing slash (/) when -p is used. By default, ls creates a listing that's sorted by filename, as in this example. Note, though, uppercase letters (as in X116) appear before lowercase letters (as in bin).

One of the most common options is -l, which creates a list like this:

```
$ ls -lt
-rwxr-xr-x 1 rich 111 Apr 13 13:48 test
-rw-r--r-- 1 rich 176322 Dec 16 09:34 httpppd-2.20b-1.1686.rpm
-rw-r--r-- 1 rich 1838045 Apr 24 18:52 tomsrtbt-1.7.269.tar.gz
-rw-r--r-- 1 rich 3265821 Apr 22 23:46 tripwire.rpm
```

This output includes permission strings (as -rwxr-xr-x), ownership (an owner of rich and a group of rich for all of these files), file sizes, and file creation dates in filenames. This example also illustrates the use of the * wildcard, which matches any string: t* matches any filename that begins with t.

> A trailing at-sign (@) denotes a symbolic link, which is a file that points to another.

# Changing Directories

The cd command changes the current directory in which you're working. Although your current directory doesn't matter for many commands, it does when you begin to refer to files. As described in the next section, “Using Absolute and Relative References,” some types of files depend on your current directory.

When you change your directory, your shell's prompt may change (depending on your distribution's settings), to something like this:

```
$ cd /usr/bin
```

Many distributions' default configurations display only the final part of the current directory—bin rather than /usr/bin in the preceding example. If you need to know the complete path of your location, you can use pwd:

```
$pwd
/usr/bin
```

![](bbox=[0.78, 0.415, 0.928, 0.455])

Linux uses a slash (/) character as a directory separator. You are familiar with Windows, you may know that Windows uses a backslash (\) for this purpose. Don't confuse the two! In Linux, a backslash serves as a "quote" or "escape" character to enter otherwise hard-to-specify characters, such as spaces, or part of a filename. Also, note that a slash is not a legal character in a Linux filename for this reason.

![](bbox=[0.78, 0.515, 0.928, 0.555])

In this book, we will shorten shell prompts to a single character, as $, when display commands on their own lines.

![](bbox=[0.78, 0.585, 0.928, 0.605])

![](bbox=[0.072, 0.955, 0.928, 0.975])