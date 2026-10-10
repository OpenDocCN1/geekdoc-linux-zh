option syntax tar's option syntax is somewhat unusual, in that it is possible (as is elsewhere) to “bundl” several options after a single dash, including (extraordinarily) ones such as -f that take a parameter. Option parameters need to be specified after the “bundl” and are matched to the corresponding parameter-taking options within the bundl e in turn.

You may leave out the dash in front of the first “option bundl”—you will often see commands like

tar cvf …

However, we don’t recommend this.

The following example archives all files within the current directory whose names begin with data to the file data.tar in the user’s home directory:

```
```
# tar -cvf ~/data.tar data*
data1
data10
data2
data3
<<<<<
```
```

The -c option arranges for the archive to be newly created, “~/data.tar” gives the name for the archive. The -v option does not change anything about the result; it only causes the names of files to appear on the screen as they are being archived. (If one of the files to be archived is really a directory, the complete content of the directory will also be added to the archive.)

directories tar also lets you archive complete directories. It is better to do this from the enclosing directory, which will create a subdirectory in the archive which is also recreated when the archive is unpacked. The following example shows this in more detail.

```
```
# cd /
# tar -cvf /tmp/home.tar /home
```
```

The system administrator root stores an archive of the /home directory (i. e., all user data) under the name of home.tar. This is stored in the /tmp directory.

If files or directories are given using absolute path names, tar automatically stores them as relative path names (in other words, the “/” at the start of each name is removed). This avoids problems when unpacking the archive on other computers (see Exercise 11.6).

You can display the “table of contents” of an archive using the -t option:

```
```
$ tar -tf data.tar
data1
data10
data2
<<<<<
```
```

The -v option makes tar somewhat more talkative:

```
```
$ tar -tvf data.tar
-rw-r--r-- joe/joe   7 2009-01-27 12:04 data1
-rw-r--r-- joe/joe   8 2009-01-27 12:04 data10
-rw-r--r-- joe/joe   7 2009-01-27 12:04 data2
<<<<<
```
```