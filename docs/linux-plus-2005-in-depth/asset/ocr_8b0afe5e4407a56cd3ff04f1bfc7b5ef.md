# Chapter 4 **EXPLORING LINUX FILESYSTEMS**

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
**Mackenzie Elizabeth**
`[root@server1 root]#_`

You can also use the **cat command** to display the line number of each line in the file in addition to the contents by passing the `**-n**` option to the **cat** command. In the following example, the number of lines in the `project4file` are displayed:

```
`[root@server1 root]# cat -n project4`
```
1  Hi there, I hope this day finds you well.
2
3  Unfortunately we were not able to make it to your dining
4  room this year while vacationing in Algonquin Park - I
5  especially wished to see the model of the Highland Inn
6  and the train station in the dining room.
7
8  I have been reading on the history of Algonquin Park but
9  no where could I find a description of where the Highland
10 Inn was originally located on Cache Lake.
11
12 If it is no trouble, could you kindly let me know such that
13 I need not wait until next year when I visit your lodge?
14
15 Regards,
16 Mackenzie Elizabeth
`[root@server1 root]#_`
```
```

In some cases, you might want to display the contents of a certain text file in reverse order, which is useful when displaying files that have text appended to them continuously by system services. These files, also known as **log files**, contain the most recent entries at the bottom of the file. To display a file in reverse order, use the **tac command** (tac is cat spelled backwards), as shown next with the file `project4`:

```
`[root@server1 root]# tac project4`
```
Mackenzie Elizabeth
Regards,

I need not wait until next year when I visit your lodge?
If it is no trouble, could you kindly let me know such that

Inn was originally located on Cache Lake.
no where could I find a description of where the Highland
I have been reading on the history of Algonquin Park but
```
```