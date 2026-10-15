
```bash
lnx02:~ # strace -o report.txt ./unmemory
Could not open the file
lnx02:~# cat report.txt
execve("./unmemory", ["./unmemory"], [/* 53 vars */]) = 0
uname({sys="Linux", node="lnx02", ...}) = 0
brk(0)                                 = 0x80002000
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x2000001a000
open("/etc/ld.so.preload", O_RDONLY)   = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY)     = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=90768, ...}) = 0
mmap(NULL, 90768, PROT_READ, MAP_PRIVATE, 3, 0) = 0x2000001b000
close(3)                               = 0
open("/lib64/tls/libc.so.6", O_RDONLY) = 3
read(3, "\177ELF\2\1\0\0\0\0\0\0\0\0\0\3\0\26\0\0\0\1\0\0\0"..., 640) = 640
lseek(3, 624, SEEK_SET)                = 624
read(3, "\0\0\0\4\0\0\0\0\20\0\0\0\1GNU\0\0\0\0\0\0\0\2\0\0\0\6"..., 32) = 32
fstat(3, {st_mode=S_IFREG|0755, st_size=1542487, ...}) = 0
mmap(NULL, 1331616, PROT_READ|PROT_EXEC, MAP_PRIVATE, 3, 0) = 0x20000032000
madvise(0x20000032000, 1331616, MADV_SEQUENTIAL|0x1) = 0
mmap(0x20000157000, 118784, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED, 3, 0x124000) = 0x20000157000
mmap(0x20000174000, 12704, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x20000174000
close(3)                               = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x20000178000
munmap(0x2000001b000, 90768)           = 0
brk(0)                                 = 0x80002000
brk(0x80023000)                        = 0x80023000
brk(0)                                 = 0x80023000
open("file.txt", O_RDONLY)             = -1 ENOENT (No such file or directory)
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 1), ...}) = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x2000001b000
write(1, "Could not open the file \n", 25) = 25
munmap(0x2000001b000, 4096)           = 0
exit_group(0)                         = ?
```

### 3.3.3 `ltrace`

`ltrace` 实用工具可以拦截并记录由执行进程发出的动态库调用以及该进程接收到的信号。它还可以拦截并打印程序执行的所有系统调用。

与 `strace` 类似，`ltrace` 也非常擅长获取跟踪信息。`ltrace` 实用工具可以通过以下两种方法进行调试：

- 使用 `ltrace` 实用工具启动用户程序或应用程序（示例 3-41）。

#### 示例 3-41 获取 `ls` 命令的 `ltrace` 示例

```bash
lnx02:~ # ltrace -o out_file -tt -f echo .hello.
.hello.
lnx02:~ # cat out_file
9901 21:02:44.476858 __libc_start_main(0x800014b0, 2, 0x3ffffa0f348, 0x80003344, 0x80003340 <unfinished ...>
9901 21:02:44.477045 getenv("")
= "LC_ALL"
9901 21:02:44.477126 setlocale(6, "")
= "C"
9901 21:02:44.477687 bindtextdomain("/usr/share/locale", "/usr/share/locale") = "/usr/share/locale"
9901 21:02:44.477791 textdomain("/usr/share/locale")
= "coreutils"
9901 21:02:44.477877 __cxa_atexit(0x80001a84, 0, 0, 0x20000065610, 0x80003828) = 0
9901 21:02:44.477957 getopt_long(2, 0x3ffffa0f348, "", 0x80005028, NULL) = -1
9901 21:02:44.478044 fputs_unlocked(0x3ffffa0f638, 0x2000018ba80, 0x8000162c, 1, 1) = 1
9901 21:02:44.478152 __overflow(0x2000018ba80, 10, 0x8000157c, 0x20000027007, 0) = 10
9901 21:02:44.478335 exit(0 <unfinished ...>
9901 21:02:44.478378 __fpending(0x2000018ba80, 0, 0x80001a84, 0x2000018a8a8, 0)
= 0
9901 21:02:44.478631 ++ exited (status 0) +++
```

- 使用 `ltrace` 实用工具挂接到正在运行的进程的 PID（示例 3-42）。

#### 示例 3-42 PID 1834 的 `ltrace`

```bash
ltrace -o out_file -tt -f -p 1834
```

注意：`ltrace` 无法跟踪线程进程。如果某个进程生成了一个共享同一地址空间的线程（即使用参数 `CLONE_VM` 和 `CLONE_THREAD` 调用 `clone` 系统调用），被跟踪的进程将因收到 `SIGILL` 信号而终止。

这里展示的另一个简单示例是使用 `ltrace` 获取系统调用统计信息，如调用次数、时间和调用列表。在示例 3-43 中，我们将 `ls` 命令作为被跟踪的可执行文件传入。从示例 3-43 中，我们可以看到哪个函数被调用得最多并消耗大量 CPU 周期。通过这种方式，开发人员可以优化其代码以提高运行效率。

#### 示例 3-43 使用 `ltrace` 进行调用跟踪
