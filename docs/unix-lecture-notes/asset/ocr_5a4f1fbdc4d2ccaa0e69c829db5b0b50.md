```
$ time -p cp1 bigfile copy_of_bigfile
```

I got the following output on one of the UNIX systems at Hunter College:

```
real  4.05
user  0.01
sys   0.02
```

What accounts for the difference between the sum of user and system times and the elapsed time? It is the time that the process spent waiting for I/O to complete. When a process issues a request for I/O, it is blocked until the I/O is complete. The time that it spends in this blocked, or waiting, state is part of the elapsed (real) time. cp1 spent about 4 seconds waiting for I/O. Although the amount of time that a process spends waiting for I/O depends heavily on what else the system is doing, the more calls it makes, the longer it will take, on average. The reason for this will be explained below.

As we use cp1 on larger and larger files, we will see worse performance. To create a spreadsheet with the results of the time command I used a different option to it:

```
/usr/bin/time -f "\t%re\t%U\t%S"
```

The -f option expects a format string, which I supplied as a tab-separated string of real-time, user-time, and system-time format symbols. This allowed me to open the output with a spreadsheet program for analysis:

| File Size (bytes) | Real | User | Sys |
|---|---|---|---|
| 19,004,256 | 17.28 | 0.00 | 0.05 |
| 38,008,512 | 39.17 | 0.01 | 0.11 |
| 76,017,024 | 73.69 | 0.00 | 0.21 |

Notice that the real and system times increase roughly in proportion to the size of the file over this small sample.

# 2.8.5 Buffering and its Impact on Performance

Consider the cp1 program above. Suppose that N is the size of the file to be copied, measured in bytes. Then the while loop in lines 32 through 36 iterates ⌈N/BUFFERSIZE⌉ times, since each iteration copies BUFFERSIZE bytes. It follows that as BUFFERSIZE is increased the number of iterations decreases inversely, i.e., if we double the buffer size, we halve the number of calls to both read() and write(). The question is, how is the total running time affected as the buffer size increases, in general? Is the amount of time to make a single call to read() proportional to the number of bytes to be read, or are there other components of its running time that are not related to the size of the read?

To answer this question, we will first perform a little experiment. We will revise the cp program so that the buffer size is an input parameter, and run the program on a very large input file with