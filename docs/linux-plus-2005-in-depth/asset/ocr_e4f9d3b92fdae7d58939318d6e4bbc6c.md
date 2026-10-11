To view the contents of a gzlp-compressed archive, you must use the -z option in addition to the -t option followed by the archive to view. The detailed contents of the /backup.tar.gz file can be viewed using the following command:

```
[root@serverl root]# tar -ztvf /backup.tar.gz
drwx----- root/root 0 2005-07-21 08:15:09 Desktop/
-rw-r--r root/root 3595 2005-06-21 20:32:48 Desktop/starthere.desktop
-rw-r--r- root/root 20239 2005-07-21 08:15:35 samplelfile
-rw-r--r- root/root 574 2005-07-21 08:18:08 samplefile2
[root@serverl root]#
```

Similarly, when extracting a gzlp-compressed archive, you must supply the -z option to the tar command. To extract the contents of the /backup.tar.gz file to a new directory called /tartest2 and view the results, you can issue the following commands:

```
[root@serverl root]# mkdir /tartest2
[root@serverl root]# cd /tartest2
[root@serverl tartest2]# tar -zxvf /backup.tar.gz
Desktop/
Desktop/starthere.desktop
samplefile
samplefile2
[root@serverl tartest2]# ls -F
Desktop/ samplefile samplefile2
[root@serverl tartest2]#
```

Backing up files to a compressed archive on a filesystem is useful when transferring data across a network, but is ill suited to backing up large amounts of data for system recovery. Devices such as tapes are better suited for this task. To back up files to a device, you can use the -f option to the tar command to specify the pathname to the appropriate device file. Files are then transferred directly to the device, overwriting any other data or filesystems that might be present.

For example, to create an archive on the first rewinding SCSI tape device containing the contents of the current directory, you can use the following command:

```
[root@serverl root]# tar -cvf /dev/st0 *
Desktop/
Desktop/starthere.desktop
samplefile
samplefile2
[root@serverl root]#
```

You can then view the contents of the archive on the tape device used in the preceding example using the command tar -tvf /dev/st0 or extract the contents of the archive on the tape device using the command tar -xvf /dev/st0 in a similar fashion to the examples shown earlier.