read. An example of how MADV_SEQUENTIAL can be used on a range shown below.

```
if ((addr = mmap((caddr_t)0, length, PROT_READ,
      MAP_SHARED, fd, offset)) == NULL) {
    perror("map failed");
    exit(1);
}

(void) madvise(addr, length, MADV_SEQUENTIAL);
(void) munmap(addr, length);
```

If we run a simple process that reads sequentially through a process, we can see by looking at the output of the vmstat command that memory is freed as it is read.

```
# ./mmmap seqread test
# vmstat 3
procs memory free re mi pi po de disk faults in fo2 s3 s5 cpu cs us sy id
r b w w/s kr/s kw/s wait act svc_t tw %b
0 0 155864 3100 1 53 336 336 0 0 0 0 205 131 57 0 1 99
0 0 155864 3100 1 53 339 339 0 0 0 0 205 131 57 0 1 99
0 0 155864 3100 1 53 332 332 0 0 0 0 205 131 57 0 1 99
0 0 155864 3100 1 53 338 338 0 0 0 0 205 131 57 0 1 99
```

Another benefit of MADV_SEQUENTIAL is that files are read in advance, in groups of 64 kilobytes. You can see this by looking at the I/O sizes with the iostat command. Our iostat example, shows that 98 I/Os per second are being read, and a total of 6272 kilobytes per second is being read, with an average I/O size of 64 kilobytes.

```
# iostat -x 5
device r/s w/s kr/s kw/s wait act svc_t tw %b
fd 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
sd6 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
sssd1 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
sd12 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd13 98.0 0.0 0.0 0.0 0.0 3.7 73.7 0 93
ssd15 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd16 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
ssd17 0.0 0.0 0.0 0.0 0.0 0.0 0.0 0 0
```

# 11.5.2 The MADV_RANDOM Flag

By default, read-ahead is implemented on file reads (as described for the MADV_SEQUENTIAL flag). In some cases, we may know that our access pattern will be completely random. In such cases, read-ahead offers no benefit and, in fact, additional overhead, since I/Os will be done in 64-kilobyte chunks rather than page-sized chunks (usually 8 kilobytes). We can disable read-ahead by specifying the MADV_RANDOM flag, as shown in the following example.