You can look at the kernel address space with the `as` adb macro, using the kernel address space pointer. The `as` macro will show the kernel address space and the pointer to the list of kernel segments.

```
```text
# adb -k
physmem b91a
kas$<as

10423320:      contents (mutex)
10423320:      owner/waiters
               0
10423328:      flags     vbits   cv
               0         0       0
10423330:      hat       hrm             seglast
               300000ebf88  0       300002a9f88
10423350:      lock (rwlock)
10423350:      wwht
               0
10423368:      segs      size            tail
10433678      2052c000       104230e0
10423380:      nsseg     lrep    hilevel
               6         0       0
10423386:      unused    updatedir       objectdir
               0         01            0
10423390:      sizezdir  wrpage          nwpage
               0         0               0
10423340:      userlimit
               0
```
```

You can then use the `seglist` adb macro to print a list of the kernel’s memory segments.

```
```text
10434678<seglist

ktxtseg:
ktxtseg:      base              size            as
              10000000          4a0000          10423320
ktxtseg+0x18: next              prev            ops
              1041fd60          0               segkmem_ops
ktxtseg+0x30: data
              0

kvalloc:
kvalloc:      base              size            as
              104a0000          e20000          10423320
kvalloc+0x18: next              prev            ops
              104233a0          10434678        segkmem_ops
kvalloc+0x30: data
              0

kvseg32:
kvseg32:      base              size            as
              78000000          4000000         10423320
kvseg32+0x18: next              prev            ops
              300002a9f88       1041fd60        segkmem_ops
kvseg32+0x30: data
              0
```
```