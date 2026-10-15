```
-rw------  1  sarwar  334848  Jul 19  13:06 ch6.doc
$
```

If you want to create an archive of the unixbook directory on a tape drive /dev/rmt/t0 (the name might be different on your system), you can use the following command after changing the directory to unixbook. The v (verbose) option is used to view the files and directories that are being archived. Unless you are the system administrator, in all likelihood you do not have access permission to use (read or write) the tape drive. Thus, the shell will give you the following error message:

```
$ tar cvf /dev/rmt/t0 .
tar: /dev/rmt/t0: Permission denied
$
```

However, if you do have proper access permissions for the tape drive, an archive of the unixbook directory is created on the tape. Not only do you need access privileges to /dev/rmt/t0, but you also need to mount it first.

However, you can also create an archive on a disk file—in a directory that you have the write permission for—by using the following command. Here we made ~/unixbook our current directory and created a tar archive of this directory in a file called unixbook.tar. Note that .tar is not an extension required by the tar utility. We have used this extension because it allows us to identify tar archives by looking at the file name. With no such extension, we have to use the file command to identify our tar archive files, as shown in the last command line in the session (in case you need reminding what the file command does).

```
$ cd ~/unixbook
$ tar cvf unixbook.tar .
tar: ./unixbook.tar same as archive file
a ./final/0K
a ./final/ch1.doc 41K
a ./final/ch2.doc 53K
a ./final/ch3.doc 140K
a ./final/ch4.doc 85K
a ./final/ch5.doc 387K
a ./final/ch6.doc 327K
a ./current/0K
a ./current/ch07.doc 200K
a ./current/ch08.doc 86K
a ./current/ch09.doc 84K
a ./current/ch10.doc 119K
a ./current/ch11.doc 149K
a ./current/ch12.doc 340K
$ ls -l
```