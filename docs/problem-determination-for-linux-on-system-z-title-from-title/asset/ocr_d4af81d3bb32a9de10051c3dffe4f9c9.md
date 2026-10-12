It is also possible to obtain only the trace of the open() system call using the option “-e trace=open.

For our demonstration of the strace, we wrote a simple program that tries to open a file descriptor that has not been initialized at all. Even though the program does not fail, using strace, we would be debug and see that the program has some flaws. In Example 3-40 strace points out that the program tries to open a file that is not available.

# Example 3-40 Debugging a invalid file descriptor problem using strace

```
lnx02:~ # strace -o report.txt ./unmemory
Could not open the file
lnx02:~# cat report.txt
execve("./unmemory", ["./unmemory"], [/* 53 vars */]) = 0
uname({sys="Linux", node="lnx02", ...}) = 0
brk(0)                                 = 0x80002000
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1,
0) = 0x2000001a000
open("/etc/ld.so.preload", O_RDONLY)   = -1 ENOENT (No such file or
directory)
open("/etc/ld.so.cache", O_RDONLY)     = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=90768, ...}) = 0
mmap(NULL, 90768, PROT_READ, MAP_PRIVATE, 3, 0) = 0x2000001b000
close(3)                               = 0
open("/lib64/tls/libc.so.6", O_RDONLY) = 3
read(3, "\177ELF\2\1\0\0\0\0\0\0\0\0\0\3\0\26\0\0\0\1\0\0\0"...,
640) = 640
lseek(3, 624, SEEK_SET)                = 624
read(3, "\0\0\0\4\0\0\0\0\20\0\0\0\1GNU\0\0\0\0\0\0\0\2\0\0\0\6"...,
32) = 32
fstat(3, {st_mode=S_IFREG|0755, st_size=1542487, ...}) = 0
mmap(NULL, 1331616, PROT_READ|PROT_EXEC, MAP_PRIVATE, 3, 0) =
0x20000032000
madvise(0x20000032000, 1331616, MADV_SEQUENTIAL|0x1) = 0
mmap(0x20000157000, 118784, PROT_READ|PROT_WRITE,
MAP_PRIVATE|MAP_FIXED, 3, 0x124000) = 0x20000157000
mmap(0x20000174000, 12704, PROT_READ|PROT_WRITE,
MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x20000174000
close(3)                               = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1,
0) = 0x20000178000
munmap(0x2000001b000, 90768)           = 0
brk(0)                                 = 0x80002000
brk(0x80023000)                        = 0x80023000
brk(0)                                 = 0x80023000
```