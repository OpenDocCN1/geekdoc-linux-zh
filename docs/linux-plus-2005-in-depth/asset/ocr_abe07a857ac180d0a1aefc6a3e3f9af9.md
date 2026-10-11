```
[root@server1 root]# mkdir /tarfest
[root@server1 root]# cd /tarfest
[root@server1 tarfest]# tar -xvf /backup.tar
Desktop/
Desktop/starthere.desktop
samplefile
samplefile2
[root@server1 tarfest]# ls -F
Desktop/ samplefile samplefile2
[root@server1 tarfest]# _
```

After an archive has been created in a file on a filesystem, that file can be sent to other computers across a network such as the Internet. Unfortunately, the `tar` utility does not compress files inside the archive; thus, the time needed to transfer the archive across a network is high. To reduce transfer times, you can compress the archive using a compression utility before transmission. Because this is a common task, the `tar` command accepts options that allow you to compress an archive immediately after creation using the `compress`, `gzip`, or `bzip2` utilities.

To create a `gzip`-compressed archive called `/backup.tar.gz` that contains the contents of the current directory and view the results, you can use the following commands:

```
[root@server1 root]# tar -czcvf /backup.tar.gz * 
Desktop/
Desktop/starthere.desktop
samplefile
samplefile2
[root@server1 root]# ls -l /backup.tar*
-rw-r--r-- 1 root root 40960 Jul 27 10:49 /backup.tar
-rw-r--r-- 1 root root 12207 Jul 27 11:18 /backup.tar.gz
[root@server1 root]# _
```

Note from the preceding output, that the `-z` option indicated compression using the `gzip` utility, and that we chose to end the filename with the `.tar.gz` extension. In addition, the size of the `/backup.tar.gz` file is much less than the `/backup.tar` file created earlier.

> **NOTE**
> Filenames that end with the `.tar.gz` or `.tgg` extensions are commonly called **tarballs** and represent gzip-compressed tar archives.