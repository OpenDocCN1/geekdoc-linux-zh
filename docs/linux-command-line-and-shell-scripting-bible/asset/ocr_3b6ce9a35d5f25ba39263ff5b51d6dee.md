# Part II Shell Scripting Basics

The first time the script runs, the $HOME/testing file is in the rich group, and the -G comparison succeeds. Next, I changed the group to the sharing group, which I'm also a member. However, the -G comparison failed, since it only compares the default groups, not any additional groups I belong to.

# Checking file date

The last set of comparisons deal with comparing the creation times of two files. This comes in handy when writing scripts to install software. Sometimes you don't want to install a file that is older than a file already installed on the system.

The -nt comparison determines if a file is newer than another file. If a file is newer, it will have a more recent file creation time. The -ot comparison determines if a file is older than another file. If the file is older, it will have an older file creation time:

```
$ cat test20
!/bin/bash
# testing file dates

if [ ./test19 -nt ./test18 ]
then
    echo "The test19 file is newer than test18"
else
    echo "The test18 file is newer than test19"
fi

if [ ./test17 -ot ./test19 ]
then
    echo "The test17 file is older than the test19 file"
fi
$ ./test20
The test19 file is newer than test18
The test17 file is older than the test19 file
$ ls -l test17 test18 test19
-rw-xr-r-- 1 rich rich 167 2007-09-30 16:31 test17
-rw-xr-r-- 1 rich rich 185 2007-09-30 17:46 test18
-rw-xr-r-- 1 rich rich 167 2007-09-30 17:50 test19
```

The filepaths used in the comparisons are relative to the directory from where you run the script. This can cause problems if the files you're checking can be moved around. Another problem is not whether these comparisons check if the file exists first. Try this test:

```
$ cat test21
!/bin/bash
# testing file dates

if [ ./badfile -nt ./badfile2 ]
```

248