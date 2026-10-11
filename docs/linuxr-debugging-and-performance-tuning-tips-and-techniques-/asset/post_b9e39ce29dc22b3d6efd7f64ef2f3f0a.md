
## 15.5.2.4 Valgrind: A Versatile Tool

The tools described in the previous section all focus on dynamic memory debugging, and indeed this is a significant problem area for many programs. However, dynamic memory problems aren’t the only kind. The GPL-licensed Valgrind program catches a large variety of problems, including those that arise from dynamic memory.

The Valgrind manual describes the program as well or better than we can, so we’ll quote (and abbreviate) it as we go along.

> Valgrind is a flexible tool for debugging and profiling Linux-x86 executables. The tool consists of a core, which provides a synthetic x86 CPU in software, and a series of “skins”, each of which is a debugging or profiling tool. The architecture is modular, so that new skins can be created easily and without disturbing the existing structure.
>
> The most useful “skin” is memcheck: The memcheck skin detects memory-management problems in your programs. All reads and writes of memory are checked, and calls to `malloc/new`/`free/delete` are intercepted. As a result, memcheck can detect the following problems:
>
> - Use of uninitialized memory.
> - Reading/writing memory after it has been `free`’d.
> - Reading/writing off the end of `malloc`’d blocks.
> - Reading/writing inappropriate areas on the stack.
> - Memory leaks—where pointers to `malloc`’d blocks are lost forever.
> - Mismatched use of `malloc/new/new []` vs `free/delete/delete []`.
> - Some misuses of the POSIX pthreads API.
>
> Problems like these can be difficult to find by other means, often lying undetected for long periods, then causing occasional, difficult-to-diagnose crashes.

Other skins are more specialized:

- `cachegrind` performs detailed simulation of the I1, D1, and L2 caches in your CPU and so can accurately pinpoint the sources of cache misses in your code.
- The **addrcheck** skin is identical to **memcheck** except for the single detail that it does not do any uninitialized-value checks. All of the other checks—primarily the fine-grained address checking—are still done. The downside of this is that you don't catch the uninitialized-value errors that **memcheck** can find. But the upside is significant: Programs run about twice as fast as they do on **memcheck**, and a lot less memory is used. It still finds reads/writes of freed memory, memory off the end of blocks and in other invalid places, bugs which you really want to find before release!
- **helgrind** is a debugging skin designed to find data races in multithreaded programs.

Finally, the manual notes:

Valgrind is closely tied to details of the CPU, operating system and to a lesser extent, compiler and basic C libraries. This makes it difficult to make it portable, so we have chosen at the outset to concentrate on what we believe to be a widely used platform: Linux on x86s. Valgrind uses the standard Unix `./configure`, `make`, `make install` mechanism, and we have attempted to ensure that it works on machines with kernel 2.2 or 2.4 and glibc 2.1.X, 2.2.X or 2.3.1. This should cover the vast majority of modern Linux installations. Note that glibc-2.3.2+, with the NPTL (Native POSIX Thread Library) package won't work. We hope to be able to fix this, but it won't be easy.

If you're using GNU/Linux on a different platform or if you're using a commercial Unix system, then Valgrind won't be of much help to you. However, as x86 GNU/Linux systems are quite common (and affordable), it's likely you can acquire one on a moderate budget, or at least find one to borrow! What's more, once Valgrind has found a problem for you, it's fixed for *whatever* platform your program is compiled to run on. Thus, it's reasonable to use an x86 GNU/Linux system for development, and some other commercial Unix system for deployment of a high-end product.

Although the Valgrind manual might lead you to expect that there are separate commands named memcheck, addrcheck, and so on, this isn't the case. Instead, a driver shell program named valgrind runs the debugging core, with the appropriate “skin” as specified by the --skin= option. The default skin is memcheck; thus, running a plain valgrind is the same as 'valgrind --skin=memcheck'. (This provides compatibility with earlier versions of Valgrind that only did memory checking, and it also makes the most sense, since the memcheck skin provides the most information.)

Valgrind provides a number of options. We refer you to its documentation for the full details. The options are split into groups; of those that apply to the core (that is, work for all skins), these are likely to be most useful:

| Option | Description |
| :--- | :--- |
| `--gdb-attach=no\|yes` | Start up with a GDB attached to the process, for interactive debugging. The default is `no`. |
| `--help` | List the options. |
| `--logfile=file` | Log messages to `file.pid`. |
| `--num-callers=number` | Show `num` callers in stack traces. The default is `4`. |
| `--skin=skin` | Use the skin named `skin`. Default is `memcheck`. |
| `--trace-children=no\|yes` | Also run the trace on child processes. The default is `no`. |
| `-v`, `--verbose` | Be more verbose. This includes listing the libraries that are loaded, as well as the counts of all the different kinds of errors. |

Of the options for the memcheck skin, these are the ones we think are most useful:

- `--leak-check=no\|yes`: Find memory leaks once the program is finished. The default is `no`.
- `--show-reachable=no\|yes`: Show reachable blocks when the program is finished. If `--show-reachable=yes` is used, Valgrind looks for dynamically allocated memory that still has a pointer pointing to it. Such memory is not a memory leak, but it may be useful to know about anyway. The default is `no`.

Let’s take a look at Valgrind in action. Remember `ch15-badmem.c`? (See Section 15.5.2.2, “Electric Fence”, page 614.) The `-b` option writes into memory that is beyond the area allocated with `malloc()`. Here’s what Valgrind reports:

```text
$ valgrind ch15-badmem1 -b
1 ==8716== Memcheck, a.k.a. Valgrind, a memory error detector for x86-linux.
2 ==8716== Copyright (C) 2002-2003, and GNU GPL'd, by Julian Seward.
3 ==8716== Using valgrind-20030725, a program supervision framework for x86-linux.
4 ==8716== Copyright (C) 2000-2003, and GNU GPL'd, by Julian Seward.
5 ==8716== Estimated CPU clock rate is 2400 MHz
6 ==8716== For more details, rerun with: -v
7 ==8716==
8 p = <not 30 bytes>
9 ==8716== Invalid write of size 1
10 ==8716== at 0x40B456: main (ch15-badmeml.c:18)
11 ==8716== by 0x42015BD3: __libc_start_main (in /lib/libc-2.2.93.so)
12 ==8716== by 0x4004368: (within /home/arolda/progex/code/ch15/ch15-badmem1)
13 ==8716== Address 0x41048405 is 12 bytes after a block of size 30 alloc'd
14 ==8716== at 0x4025488: malloc (vg_replace_malloc.c:153)
15 ==8716== by 0x4004311: main (ch15-badmeml.c:11)
16 ==8716== by 0x42015BD3: __libc_start_main (in /lib/libc-2.2.93.so)
17 ==8716== by 0x4004368: (within /home/arolda/progex/code/ch15/ch15-badmem1)
18 ==8716==
19 ==8716== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)
20 ==8716== malloc/free: 1 use at exit: 30 bytes in 1 blocks.
21 ==8716== malloc/free: 1 allocs, 0 frees, 30 bytes allocated.
22 ==8716== For a detailed leak analysis, rerun with: --leak-check=yes
23 ==8716== For counts of detected errors, rerun with: -v
```

(Line numbers in the output were added to aid in the discussion.) Line 8 is the output from the program; the others are all from Valgrind, on standard error. The error report on lines 9–17. It indicates how many bytes were incorrectly written (line 9), where this happened (line 10), and a stack trace. Lines 13–17 describe where the memory was allocated from. Lines 19–23 provide a summary.

The `-f` option to `ch15-badmem1` frees the allocated memory and then writes into it through a dangling pointer. Here is what Valgrind reports for this case:

```text
$ valgrind ch15-badmem1 -f
==8719== Memcheck, a.k.a. Valgrind, a memory error detector for x86-linux.
==8719== P = <not 30 bytes>
==8719== Invalid write of size 1
==8719==    at 0x8048498: main (ch15-badmem1.c:21)
==8719==    by 0x420158D3: __libc_start_main (in /lib/i686/libc-2.2.93.so)
==8719==    by 0x4048368: (within /home/arnold/progex/code/ch15/ch15-badmem1)
==8719==    Address 0x41048024 is 0 bytes inside a block of size 30 free’d
==8719==    at 0x4025722: free (vg_replace_malloc.c:220)
==8719==    by 0x8048491: main (ch15-badmem1.c:20)
==8719==    by 0x420158D3: __libc_start_main (in /lib/i686/libc-2.2.93.so)
==8719==    by 0x4048368: (within /home/arnold/progex/code/ch15/ch15-badmem1)
```

This time the report indicates that the write was to freed memory and that the call to `free()` is on line 20 of `ch15-badmem1.c`.

When called with no options, `ch15-badmem1.c` allocates memory and uses it but does not release it. The `--leak-check=yes` option reports this case:

```text
$ valgrind --leak-check=yes ch15-badmem1
1 ==8720== Memcheck, a.k.a. Valgrind, a memory error detector for x86-linux.
...
8 p = <not 30 bytes>
9 ==8720==
10 ==8720== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
11 ==8720== malloc/free: in use at exit: 30 bytes in 1 blocks.
12 ==8720== malloc/free: 1 allocs, 0 frees, 30 bytes allocated.
...
16 ==8720==
17 ==8720== 30 bytes in 1 blocks are definitely lost in loss record 1 of 1
18 ==8720==    at 0x4025488: malloc (vg_replace_malloc.c:153)
19 ==8720==    by 0x8040411: main (ch15-badmem1.c:11)
20 ==8720==    by 0x420158D3: __libc_start_main (in /lib/i686/libc-2.2.93.so)
21 ==8720==    by 0x4048368: (within /home/arnold/progex/code/ch15/ch15-badmem1)
22 ==8720==
23 ==8720== LEAK SUMMARY:
24 ==8720==    definitely lost: 30 bytes in 1 blocks.
25 ==8720==    possibly lost: 0 bytes in 0 blocks.
26 ==8720==    still reachable: 0 bytes in 0 blocks.
27 ==8720==    suppressed: 0 bytes in 0 blocks.
28 ==8720== Reachable blocks (those to which a pointer was found) are not shown.
29 ==8720== To see them, rerun with: -v-show-reachable=yes
```

Lines 17–29 provide the leak report; the leaked memory was allocated on line 11 of `ch15-badmem1.c`.

Besides giving reports on misuses of dynamic memory, Valgrind can diagnose uses of *uninitialized* memory. Consider the following program, `ch15-badmem3.c`:
