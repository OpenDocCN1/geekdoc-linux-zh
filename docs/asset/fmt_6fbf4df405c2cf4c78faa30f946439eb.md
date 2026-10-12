
```
$ strace /usr/bin/id
execve("/usr/bin/id", ["/usr/bin/id"], ...) = 0
brk(0) = 804c4c8
open("/etc/ld.so.preload", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY) = 3
fstat6(3, {st_mode=S_IFREG|0644, st_size=76061, ...}) = 0
old_map(NULL, 70661, PROT_READ, MAP_PRIVATE, 3, 0) = 0x40160000
close(3) = 0
open("/lib/libc.so.6", O_RDONLY) = 3
read(3, "\x17\x46\x71\x01\x00\x01\x00\x03\x03\x01\x00\x00\x30\x04") = 1024
fstat6(3, {st_mode=S_IFREG|0644, st_size=145807, ...}) = 0
old_map(NULL, 126836, PROT_READ, PROT_EXEC, 3, 0) = 0x40029000
mprotect(0x401500, 27748, PROT_NONE)
old_map(0x401500, 20480, PROT_READ, PROT_WRITE, MAP_FIXED, 3, 0x0) = 0x4002000
old_map(0x401500, 7268, PROT_READ, PROT_WRITE, MAP_ANONYUS, -1, 0) = 0x4015d00
close(3) = 0
old_map(NULL, 4096, PROT_READ, PROT_WRITE, MAP_PRIVATE, -1, 0) = 0x401f00
munmap(0x401600, 70661) = 0
brk(0) = 804c4c8
brk(0x400d48) = 0x400d48
brk(0) = 0x400e00
uid(32) = 1000
gid(32) = 1000
egid(32) = 100
fstat6(1, {st_mode=S_IFCHR|0700, st_dev=makedev(136), ...}) = 0
old_map(NULL, PROT_READ, PROT_WRITE, MAP_ANONYUS, -1, 0) = 0x4001000
socket(PF_UNIX, SOCK_STREAM, 0) = 3
connect(3, {sa_family=AF_UNIX, path="/var/run/.socket"}, 110) = -ENOENT (No file or directory)
close(3) = 0
open("/etc/nswitch.conf", O_RDONLY) = 3
fstat6(3, {st_mode=S_IFREG|0644, st_size=103, ...}) = 0
old_map(NULL, PROT_READ, PROT_WRITE, MAP_ANONYUS, -1, 0) = 0x4001700
read(3, "\n# /etc/switch.conf\n#...", 4096) = 103
read(3, "#...") = 6
close(3) = 0
munmap(0x4001700, 4096) = 0
open("/etc/ld.so.cache", O_RDONLY) = 3
fstat6(3, {st_mode=S_IFREG|0644, st_size=70661, ...}) = 0
old_map(NULL, 70661, PROT_READ, MAP_PRIVATE, 3, 0) = 0x401600
open("/lib/ns1.so.2", O_RDONLY) = 3
read(3, "\x77ELF\x1f\x01\x01\x00\x00\x00\x03\x03\x01\x00...", 1024) = 1024
fstat6(3, {st_mode=S_IFREG|0755, st_size=49707, ...}) = 0
old_map(NULL, 84928, PROT_READ, PROT_EXEC, MAP_PRIVATE, 3, 0) = 0x4017300
mprotect(0x4018500, 11200, PROT_NONE) = 0
old_map(0x4018500, 4096, PROT_READ, PROT_WRITE, MAP_FIXED, 3, 0x0) = 0x4018000
old_map(0x4018600, 7104, PROT_READ, PROT_WRITE, MAP_ANONYUS, -1, 0) = 0x4018600
close(3) = 0
```

(Continuing with `strace` output)

```
exit_group(0) = 0
close(3) = 0
munmap(0x401600, 70661) = 0
```

## 300 Linux 网络安全

```
close(3)                                = 0
munmap(0x04002300, 4096)                     = 0
open("/etc/group", O_RDONLY)                 = 3
fcntl164(3, F_GETFD)                            = 0
fcntl164(3, F_SETFD, FD_CLOEXEC)               = 0
fstat64(3, {st_mode=S_IFREG|0644, st_size=485, ...}) = 0
old_map(NULL, PROT_READ, PROT_WRITE, MAP_PRIVATE|MAP_ANONYUS, -1, 0) = 0x4002300
lseek(3, 0, [0], SEEK_CUR) = 0
read(3, "root:0:0::root/bin/bash...", 4096) = 485
close(3) = 0
munmap(0x40023000, 4096) = 0
socket(PF_UNIX, SOCK_STREAM, 0) = 3
connect(3, {sa_family=AF_UNIX, path="/var/run/.socket"}, 110) = -ENOENT (No file or directory)
close(3) = 0
open("/etc/group", O_RDONLY) = 3
fcntl164(3, F_GETFD) = 0
fcntl164(3, F_SETFD, FD_CLOEXEC) = 0
fstat64(3, {st_mode=S_IFREG|0644, st_size=485, ...}) = 0
old_map(NULL, PROT_READ, PROT_WRITE, MAP_PRIVATE|MAP_ANONYUS, -1, 0) = 0x4002300
lseek(3, 0, [0], SEEK_CUR) = 0
read(3, "root::0:0bin:root,bin,da...", 4096) = 485
close(3) = 0
munmap(0x40023000, 4096) = 0
getgroups(32,0) = 2
getgroups(32, 0x0204d90) = 2
open("/etc/group", O_RDONLY) = 3
fcntl164(3, F_GETFD) = 0
fcntl164(3, F_SETFD, FD_CLOEXEC) = 0
fstat64(3, {st_mode=S_IFREG|0644, st_size=485, ...}) = 0
old_map(NULL, PROT_READ, PROT_WRITE, MAP_PRIVATE|MAP_ANONYUS, -1, 0) = 0x4002300
lseek(3, 0, [0], SEEK_CUR) = 0
read(3, "root:rootbin:root,bin,da...", 4096) = 485
```

## 逃离 `chroot` 监狱

不幸的是，Linux 的 `chroot` 實作並不十分安全（與 FreeBSD 和 OpenBSD 上的 BSD jail 系統相比）。特別是，`chroot` 從來不是設計用於監禁以 `root` 身份運行的程序，而具有 `root` 權限的程序可以輕易通過一個大的逃逸

# 系统加固 301

公开技术的数量。在某些方面，这是一种悖论，因为以 `root` 身份运行的进程特别容易受到攻击。
