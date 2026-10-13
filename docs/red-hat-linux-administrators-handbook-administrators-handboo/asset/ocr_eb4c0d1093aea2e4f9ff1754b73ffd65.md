When the default is left alone and the ftpconversions file is not modified, all the users who use the FTP service are able to compress files on the fly. For example, a user who wants to get the entire contents of a directory as a compressed file can enter the command get directoryname.tar.gz, and a compressed tar file will be downloaded.

# tar

Syntax: tar yes|no classg [class . . .]
Default: tar yes all

This keyword enables or disables the tar (tape archive file) feature for specified classes. The default setting allows the compression feature for the class called all, which, by default, covers all the real, anonymous, and guest users. When the default is left alone and the ftpconversions file is not modified, all the users who use the FTP service are able to tar files on the fly. For example, a user who wants to get the entire contents of a directory as a compressed file can enter the command get directoryname.tar, and a tar file will be downloaded.

# shutdown

Syntax: shutdown path
Default: shutdown /etc/shutmsg

This keyword specifies the file that the FTP server monitors from time to time to detect a shutdown event. This file can be created using the ftpshut command. For example, to shut down the server immediately, run the following command:

```
ftpshut now
```

You also can schedule a shutdown in such a way that the logged-in users have some time before the shutdown begins. For example, suppose the current date is Monday, July 03, 2000, and the time is 1600 (in 24-hour format). To shut down the system in an hour, issue the following command:

```
ftpshut -d 30 1700
```

This creates the /etc/shutmsg file, as follows:

```
2000 06 03 17 00 0010 0030
System shutdown at $s
```