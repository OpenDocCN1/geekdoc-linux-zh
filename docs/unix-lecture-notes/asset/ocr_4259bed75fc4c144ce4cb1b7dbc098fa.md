```
Number of X lines : 1000
Number of y lines : 1000
X lines in first 1000 : 515
y lines in first 1000 : 485
X lines in last 1000 : 485
y lines in last 1000 : 515
Xy lines : 0
yX lines : 0
```

The last two lines show that all writes were atomic because there are no lines that contain an Xy or yX combination. Now edit the program by commenting out the line

```
#define ATOMIC
```

and recompile it. This flag determines how large the chunk is. When it is turned off, the chunk is larger than PIPE_BUF bytes. Run the script again. The output will most likely look something like this:

```
Number of X lines : 1443
Number of y lines : 1437
X lines in first 1000 : 758
y lines in first 1000 : 718
X lines in last 1000 : 685
y lines in last 1000 : 719
Xy lines : 577
yX lines : 586
```

which shows that when the chunk size of a write exceeds PIPE_BUF, the writes will not be atomic.

# 8.2.2.1 More About fpathconf()

Almost all systems comply with the POSIX requirement that result of the call

```
pipe_size = fpathconf(fd, _PC_PIPE_BUF);
```

is the system's current value of PIPE_BUF. But not all do. Some systems using recent versions of the GNU C Library will use a different version of fpathconf(). This version returns the pipe capacity, not the value of PIPE_BUF, but only if the kernel supports it. Linux kernels after 2.6.35 do for certain. What this implies is that you cannot reliably use the result of fpathconf() to determine the maximum number of bytes in an atomic write on all systems.