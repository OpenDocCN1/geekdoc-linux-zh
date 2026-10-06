# The Linux Command Line

There are a couple of things to notice in the file listing. First, you'll notice that the test5 file has a different inode number than the test1 file, indicating that the Linux system treats it as a separate file. Second, the file size is different. A linked file is to store only information about the source file, not the actual data in it. The filename area of the listing shows the relationship between the two files.

Instead of using the cp command, if you want to link files you can also use the ln command. By default the ln command creates hard links. If you want to create a soft link, you'll still need to use the s parameter.

Be careful when copying linked files. If you are linked to another source file, you're all making another copy of the source file. This can quickly get confusing. Instead of copying the linked file, you can create another link to the original file. You can have many links to the same file with no problems. However, you also don't want to create soft links to other soft-linked files. This creates a chain of links that can not be confusing but also easily broken, causing all of problems.

# Renaming files

In the Linux world, renaming files is moving. The mv command is available to move both files and directories to another location:

```
$ mv test2 test6
$ ls -il *
1954793 -rw-r--r-- 2 rich rich 6 Sep 09:51 test1
1954888 -rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
1954793 -rw-r--r-- 2 rich rich 6 Sep 09:51 test4
1954891 lrwxr-xr-x 1 rich rich 5 Sep 09:56 test5 -> test1
1954794 -rw-r--r-- 1 rich rich 0 Sep 09:39 test6
```

Notice that the moving changed the filename but kept the same number and the time-value. Moving a file with soft links is a:

```
$ mv test1 test8
$ ls -il *
total 16
1954888 -rw-r--r-- 1 rich rich 0 Dec 25 2008 test3
1954793 -rw-r--r-- 2 rich rich 6 Sep 09:51 test4
1954891 lrwxr-xr-x 1 rich rich 5 Sep 09:56 test5 -> test1
1954794 -rw-r--r-- 1 rich rich 0 Sep 09:39 test6
1954793 -rw-r--r-- 2 rich rich 6 Sep 09:51 test8
[rich@test2 clsc]$$ mv test8 test1
```

The test4 file that uses a hard link uses the same inode number, which is perfectly fine. However, the test5 file now points to an invalid file, and it is no longer a valid link.

You can also use the mv command to move directories:

```
$ mv dir2 dir4
```