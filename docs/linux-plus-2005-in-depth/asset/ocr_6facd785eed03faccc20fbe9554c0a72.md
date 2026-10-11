```
[root@server1 root]# bzip2 -v samplefile samplefile2
samplefile1: 2.63f:1, 3,034 bits/byte, 62.08% saved, 20239 in,7675 out.
samplefile2: 1.463:1, 5,394 bits/byte, 32.58% saved, 574 in,387 out.
[root@server1 root]# ls -1
total 16
drwx------ 3 root root 4096 Jul 21 08:15 Desktop
-rw-rw-r-- 1 root root 387 Jul 21 08:18 samplefile2.bz2
-rw-r-r-- 1 root root 7675 Jul 21 08:15 samplefile.bz2
[root@server1 root]# _
```

Because the compression algorithm is different than the one used by the compress and gzip utilities, you must use the **bcat command** to display the contents of compressed files to Standard Output, as shown in the following example:

```
[root@server1 root]# bcat samplefile2.bz2
Hi there, I hope this day finds you well.
```

Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I especially wished to see the model of the Highland Inn and the train station in the dining room.

I have been reading on the history of Algonquin Park but no where could I find a description of where the Highland Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth

```
[root@server1 root]# _
```

# NOTE

A **bzmore command** and a **bless command** also exist, which can be used to view the contents of a bzip2-compressed file page-by-page.