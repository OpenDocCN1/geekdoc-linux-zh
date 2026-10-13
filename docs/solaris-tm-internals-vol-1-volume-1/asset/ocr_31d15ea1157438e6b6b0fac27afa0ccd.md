read. An example of how `MADV_SEQUENTIAL` can be used on a range is shown below.

```
```c
if ((addr = mmap64((caddr_t)0, length, PROT_READ,
    MAP_SHARED, df, 0, (off_t)0)) == NULL) {
        perror("mmap failed");
        exit(1);
}

(void) madvise(addr, length, MADV_SEQUENTIAL);
(void) munmap(addr, length);
```
```

If we run a simple process that reads sequentially through a process, we can see by looking at the output of the `vmstat` command that memory is freed as it is read.

```
```text
# ./mmap_seqread testfile&
# vmstat 3
procs      memory            page              disk            faults      cpu
 r  b  w  swap free  re  mf  pi  po  fr  de  sr  s0  s1  s2  s3  in  sy  cs  us  sy  id
 0  0  0 155864 3100  1  53 336  0 336  0  0  0  0  0  41 205 131  57  0   1  99
 0  0  0 155864 3100  1  53 339  0 339  0  0  0  0  0  41 205 131  57  0   1  99
 0  0  0 155864 3100  1  53 332  0 332  0  0  0  0  0  41 205 131  57  0   1  99
 0  0  0 155864 3100  1  53 338  0 338  0  0  0  0  0  41 205 131  57  0   1  99
```
```

Another benefit of `MADV_SEQUENTIAL` is that files are read in advance, in groups of 64 kilobytes. You can see this by looking at the I/O sizes with the `iostat` command. Our iostat example, below, shows that 98 I/Os per second are being read, and a total of 6272 kilobytes per second is being read, with an average I/O size of 64 kilobytes.

```
```text
# iostat -x 5

device     r/s   w/s   kr/s   kw/s wait actv  svc_t  %w  %b
fd0        0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
sd6        0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd11      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd12      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd13     98.0   0.0 6272.0    0.0  0.0  3.7   73.7   0  93
ssd15      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd16      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
ssd17      0.0   0.0    0.0    0.0  0.0  0.0    0.0   0   0
```
```

# 11.5.2.4 The `MADV_RANDOM` Flag

By default, read-ahead is implemented on file reads (as described for the `MADV_SEQUENTIAL` flag). In some cases, we may know that our access pattern will be completely random. In such cases, read-ahead offers no benefit and may, in fact, add additional overhead, since I/O will be done in 64-kilobyte chunks rather than