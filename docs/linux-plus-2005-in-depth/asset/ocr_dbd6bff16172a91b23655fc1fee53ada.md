```
If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
```

```
[root@server1 root]# _
```

![](bbox=[0.13, 0.26, 0.87, 0.38])

To decompress files that have been compressed with the `compress` utility, simply use the **uncompress command** followed by the names of the files to be decompressed. This restores the original filename. The following output decompresses and displays the filenames for the samplefile.Z and samplefile2.Z files created earlier:

```
[root@server1 root]# uncompress -v samplefile.Z samplefile2.Z
samplefile.Z: -- replaced with samplefile
samplefile2.Z: -- replaced with samplefile2
[root@server1 root]# ls -l
total 28
drwx------     3 root  root    4096 Jul 21 08:15 Desktop
-rw-r--r--     1 root  root    20239 Jul 21 08:15 samplefile
-rw-rw-r--     1 root  root      574 Jul 21 08:18 samplefile2
[root@server1 root]# _
```

![](bbox=[0.13, 0.65, 0.87, 0.78])

You can omit the `.Z` extension when using the `uncompress` command; the command `uncompress -v samplefile samplefile2` would achieve the same results as the command shown in the preceding output.

Furthermore, the `compress` utility is a filter command that can take information from Standard Input and send it to Standard Output. For example, to send the output of the `who` command to