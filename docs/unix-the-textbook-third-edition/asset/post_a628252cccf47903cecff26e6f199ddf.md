
x ./final, 0 bytes, 0 tape blocks
x ./final/ch1.doc, 41984 bytes, 82 tape blocks
x ./final/ch2.doc, 54272 bytes, 106 tape blocks
x ./final/ch3.doc, 142848 bytes, 279 tape blocks
x ./final/ch4.doc, 86528 bytes, 169 tape blocks
x ./final/ch5.doc, 396288 bytes, 774 tape blocks
x ./final/ch6.doc, 334848 bytes, 654 tape blocks
x ./current, 0 bytes, 0 tape blocks
x ./current/ch07.doc, 204288 bytes, 399 tape blocks
x ./current/ch08.doc, 87552 bytes, 171 tape blocks
x ./current/ch09.doc, 86016 bytes, 168 tape blocks
x ./current/ch10.doc, 121344 bytes, 237 tape blocks
x ./current/ch11.doc, 152576 bytes, 298 tape blocks
x ./current/ch12.doc, 347648 bytes, 679 tape blocks
$ ls -l
drw------- 2 sarwar 512 Jul 22 13:21 current
drw------- 2 sarwar 512 Jul 22 13:21 final
-rw------ 1 sarwar 2064896 Jul 22 13:47 unixbook.tar
$

The unixbook.tar file remains intact after it has been unpacked. This result makes sense considering that the primary purpose of the tar archive is to back up files, and it should remain intact after restoration in case the system crashes after the file is restored but before it is archived again. After restoration of the unixbook.tar file, your directory structure looks like that shown in Figure 23.16.

At times, you might need to restore a subset of files in a tar archive. System administrators often do this after a system crashes (usually caused by a disk head crash resulting from a power surge) and destroys some user files with it. In such cases, system administrators restore only those files from the tape archive that reside on the damaged portion of the disk. Selective restoration is possible with the function option x as long as the pathnames of the files to be restored are known. If you do not remember the pathnames of the files to be restored, you can use the function option t to display the pathnames of files and directories on the archive file. The output of the tar command with the t option is in a format similar to the output of the ls -l command, as shown in the following session. As marked in the sample, the first field specifies file type and access

![](img/02e070097d401d3bf7de4bf1c470b267_1146_0.png)

permissions, the second field specifies user ID/group ID of the owner of the file, the third field shows the file size in bytes, the next several fields show the time and date that the file was last modified, and the last field shows the pathname of the file as stored in the archive.

If an archive contains a large number of files, you can pipe the output of the tar t command to the more command for page-by-page view. If you know the name of the file but not its pathname, you can pipe output of the tar command with the t option to the grep command. Files can also be restored, or their pathnames viewed, selectively. The following session illustrates these points.

```
$ tar -tvf unixbook.tar
drw------- 121/152 0 Jul 22 13:47 2015 ./
drw------- 121/152 0 Jul 22 13:21 2015 ./final/
-rw------ 121/152 41984 Jul 19 13:06 2015 ./final/ch1.doc
-rw------ 121/152 54272 Jul 19 13:06 2015 ./final/ch2.doc
-rw------ 121/152 142848 Jul 19 13:06 2015 ./final/ch3.doc
-rw------ 121/152 86528 Jul 19 13:06 2015 ./final/ch4.doc
-rw------ 121/152 396288 Jul 19 13:06 2015 ./final/ch5.doc
-rw------ 121/152 334848 Jul 19 13:06 2015 ./final/ch6.doc
drw------- 121/152 0 Jul 22 13:21 2015 ./current/
-rw------ 121/152 204288 Jul 19 13:06 2015 ./current/ch07.doc
-rw------ 121/152 87552 Jul 19 13:06 2015 ./current/ch08.doc
-rw------ 121/152 86016 Jul 19 13:06 2015 ./current/ch09.doc
-rw------ 121/152 121344 Jul 19 13:06 2015 ./current/ch10.doc
-rw------ 121/152 152576 Jul 19 13:06 2015 ./current/ch11.doc
-rw------ 121/152 347648 Jul 19 13:06 2015 ./current/ch12.doc
$ tar -tvf unixbook.tar | grep ch10.doc
-rw------ 121/152 121344 Jul 19 13:06 2015 ./current/ch10.doc
$
```

If you want to restore the file ch10.doc in the ~/unixbook/current directory, you can use the following command sequence. Be sure that you give the pathname of the file to be restored, not just its name.
