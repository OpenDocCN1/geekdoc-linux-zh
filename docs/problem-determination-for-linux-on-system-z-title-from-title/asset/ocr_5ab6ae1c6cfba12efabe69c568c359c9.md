```
open("file.txt", 0_RDONLY)          = -1 ENOENT (No such file or
directory)
fstat(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 1), ...}) = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1,
0) = 0x2000001b000
write(1, "Could not open the file \n", 25) = 25
munmap(0x2000001b000, 4096)          = 0
exit_group(0)                        = ?
```

# 3.3.3 ltrace

The ltrace utility intercepts and records the dynamic library calls from the executed process and the signals that are received by that process. It can also intercept and print the system calls executed by the program.

As with strace, ltrace is also very similar to obtaining the traces. The ltrace utility can be used for debugging with two methods:

+   - Invoke the user program or application with the ltrace utility (Example 3-41).

Example 3-41 Example for obtaining ltrace for ls command

```
lnx02:~ # ltrace -o out_file -tt -f echo .hello.
.hello.
lnxihs:~ # cat out_file
9901 21:02:44.476858 __libc_start_main(0x800014b0, 2, 0x3ffffa0f348,
0x80003344, 0x80003340 <unfinished ...>
9901 21:02:44.477045 getenv("")
= "SIXLY_CORRECT"
9901 21:02:44.477126 setlocale(6, "")
= "247|364|375|203|343)\2610"
9901 21:02:44.477687 bindtextdomain("/usr/share/locale",
"/usr/share/locale") = "/usr/share/locale"
9901 21:02:44.477791 textdomain("/usr/share/locale")
= "coreutils"
9901 21:02:44.477877 __cxa_atexit(0x80001a84, 0, 0, 0x20000065610,
0x80003828) = 0
9901 21:02:44.477957 getopt_long(2, 0x3ffffa0f348, "", 0x80005028,
NULL) = -1
9901 21:02:44.478044 fputs_unlocked(0x3ffffa0f638, 0x2000018ba80,
0x8000162c, 1, 1) = 1
9901 21:02:44.478152 __overflow(0x2000018ba80, 10, 0x8000157c,
0x20000027007, 0) = 10
9901 21:02:44.478335 exit(0 <unfinished ...>
```