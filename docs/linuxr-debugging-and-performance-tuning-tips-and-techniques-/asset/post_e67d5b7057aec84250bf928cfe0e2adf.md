
... runs.) When muntrace() is called, the library closes the file and does not log any further allocations or frees.

The use of separate functions makes it possible to do memory tracing for specific parts of the program; it’s not necessary to trace everything. (We find it most useful to enable logging at the start of the program and be done, but this design provides flexibility, which is nice to have.)

Once the application program exits, you use the mtrace program to analyze the log file. (The log file is ASCII, but the information isn’t directly usable.) For example, gawk turns on tracing if TIDYMEM is defined:

```bash
$ export TIDYMEM=1 MALLOC_TRACE=mtrace.out
$ ./gawk 'BEGIN { print "hello, world" }'
hello, world
$ mtrace ./gawk mtrace.out
```

- Export environment variables
- Run the program
- Generate report

```
Memory not freed:
=============
Address    Size   Caller
0x08085858   0x20   at /home/arnold/Gnu/gawk/gawk-3.1.3/main.c:1102
0x08085880   0x80   at /home/arnold/Gnu/gawk/gawk-3.1.3/node.c:398
0x08086508   0x2    at /home/arnold/Gnu/gawk/gawk-3.1.3/node.c:337
0x08086518   0x6    at /home/arnold/Gnu/gawk/gawk-3.1.3/node.c:327
0x08086528   0x10   at /home/arnold/Gnu/gawk/gawk-3.1.3/eval.c:2082
0x08086550   0x3    at /home/arnold/Gnu/gawk/gawk-3.1.3/node.c:337
0x08086560   0x3    at /home/arnold/Gnu/gawk/gawk-3.1.3/node.c:337
0x080865e0   0x4    at /home/arnold/Gnu/gawk/gawk-3.1.3/field.c:76
0x08086670   0x78   at /home/arnold/Gnu/gawk/gawk-3.1.3/awkgram.c:1369
0x08086700   0xe    at /home/arnold/Gnu/gawk/gawk-3.1.3/node.c:337
0x08086718   0x1f   at /home/arnold/Gnu/gawk/gawk-3.1.3/awkgram.y:1259
```

The output is a list of locations at which gawk allocates memory that is never freed. Note that permanently hanging onto dynamic memory is fine if it’s done on purpose. All the cases shown here are allocations of that sort.

### 15.5.2.2 Electric Fence

In Section 3.1, “Linux/Unix Address Space,” page 52, we described how dynamic memory comes from the heap, which can be made to grow and shrink (with the brk() or sbrk() calls, described in Section 3.2.3, “System Calls: brk() and sbrk(),” page 75).

Well, the picture we presented there is a simplified version of reality. More advanced system calls (not covered in this volume) make it possible to add additional, not necessarily contiguous, segments of memory into a process’s address space. Many malloc() debuggers work by using these system calls to add a new piece of address space for *every* allocation. The advantage of this scheme is that the operating system and the computer’s memory-protection hardware cooperate to make access to memory outside these disconnected segments invalid, generating a `SIGSEGV` signal. The scheme is depicted in Figure 15.1.

![](img/766b5597246d532412fad21b1c59ccec_647_0.png)

**FIGURE 15.1**  
*Linux/Unix process address space, including special areas*

The first debugging package to implement this scheme was Electric Fence. Electric Fence is a drop-in replacement for `malloc()` et al. It works on many Unix systems and GNU/Linux; it is available from its author's FTP archive.[^17] Many GNU/Linux distributions supply it, although you may have to choose it explicitly when you install your system.

[^17]: http://ftp.pereens.com/pub/ElectricFence

Once a program is linked with Electric Fence, any access that is out of bounds generates a SIGSEGV. Electric Fence also catches attempts to use memory that has already been freed. Here is a simple program that illustrates both problems:

```c
1 /* ch15-badmem1.c --- do bad things with memory */
2
3 #include <stdio.h>
4 #include <stdlib.h>
5
6 int main(int argc, char **argv)
7 {
8     char *p;
9     int i;
10
11     p = malloc(30);
12
13     strcpy(p, "not 30 bytes");
14     printf("p = <&s>\n", p);
15
16     if (argc == 2)
17         if (strcmp(argv[1], "-b") == 0)
18             p[42] = 'a';    /* touch outside the bounds */
19         else if (strcmp(argv[1], "-f") == 0) {
20             free(p);        /* free memory and then use it */
21             p[0] = 'b';
22         }
23     }
24
25     /* free(p); */
26
27     return 0;
28 }
```

This program does simple command-line option checking to decide how to misbehave: -b touches memory out of bounds, and -f attempts to use freed memory. (Lines 18 and 21 are the dangerous ones, respectively.) Note that with no options, the pointer is never freed (line 25); Electric Fence doesn't catch this case.

One way to use Electric Fence, a way that is guaranteed to work across Unix and GNU/Linux systems, is to statically link your program with it. The program should then be run from the debugger. (The Electric Fence documentation is explicit that Electric Fence should not be linked with a production binary.) The following session demonstrates this procedure and shows what happens for both command-line options:

```bash
$ cc -g ch15-badmem1.c -lefence -o ch15-badmem1     # Compile; link statically
$ gdb ch15-badmem1                                    # Run it from the debugger
gdb (gdb) 5.3
...  # Try -b option
(gdb) run -b
Starting program:  /home/arnold/progex/code/ch15/ch15-badmem1 -b
[New Thread 8192 (LWP 28021)]

   Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

 Program received signal SIGSEGV, Segmentation fault.   # SIGSEGV: GDB prints where
 (Switching to Thread 8192 (LWP 28021))
 0x080485b6 in main (argc=2, argv=0xbffffffa4) at ch15-badmem1.c:18
                                                    p[42] = 'a';       /* touch outside the bounds */
(gdb) run -f                                       # Now try the -f option
The program being debugged has been started already.
Start it from the beginning? (y or n) y            # Yes, really

Starting program:  /home/arnold/progex/code/ch15/ch15-badmem1 -f
[New Thread 8192 (LWP 28024)]

   Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

 Program received signal SIGSEGV, Segmentation fault.          # SIGSEGV again
 (Switching to Thread 8192 (LWP 28024))
 0x080485e8 in main (argc=2, argv=0xbffffffa4) at ch15-badmem1.c:21
                                                    p[0] = 'b';
```

On systems that support shared libraries and the LD_PRELOAD environment variable (including GNU/Linux), you don’t need to explicitly link in the efence library. Instead, the ef shell script arranges to run the program with the proper setup.

Although we haven’t described the mechanisms in detail, GNU/Linux (and other Unix systems) support shared libraries, special versions of the library routines that are kept in a single file on disk instead of copied into every single executable program’s binary file. Shared libraries save some space on disk and can save system memory, since all programs using a shared library share the same in-memory copy of the library. The cost is that program startup is slower because the program and the shared library have to be hooked together before the program can start running. (This is usually transparent to you, the user.)

The `LD_PRELOAD` environment variable causes the system’s program loader (which brings executable files into memory) to link in a special library *before* the standard libraries. The `ef` script uses this feature to link in Electric Fence’s version of the `malloc()` suite. Thus, relinking isn’t even necessary. This example demonstrates `ef`:

```bash
$ cc -g ch15-badmem1.c -o ch15-badmem1            # Compile normally
$ ef ch15-badmem1 -b                                 # Run using ef, dumps core

Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>
/usr/bin/ef: line 20: 28005 Segmentation fault     (core dumped)
( export LD_PRELOAD=libefence.so.0.0.0; exec $* )

$ ef ch15-badmem1 -f                                 # Run using ef, dumps core again

Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>
/usr/bin/ef: line 20: 28007 Segmentation fault     (core dumped)
( export LD_PRELOAD=libefence.so.0.0.0; exec $* )

$ ls -l core*                                        # Linux gives us separate core files
-rw------- 1 arnold devel 217088 Aug 28 15:40 core.28005
-rw------- 1 arnold devel 212992 Aug 28 15:40 core.28007
```

GNU/Linux creates core files that include the process ID number in the file name. In this instance this behavior is useful because we can debug each core file separately:

```bash
$ gdb ch15-badmem1 core.28005                        # From the -b option
GNU gdb 5.3
...
Core was generated by `ch15-badmem1 -b`.
Program terminated with signal 11, Segmentation fault.
#0  0x08048466 in main (argc=1, argv=0xbffff8c4) at ch15-badmem1.c:18
18)
      p[42] = 'a';      /* touch outside the bounds */
(gdb) quit

$ gdb ch15-badmem1 core.28007                        # From the -f option
GNU gdb 5.3
...
Core was generated by `ch15-badmem1 -f`.
Program terminated with signal 11, Segmentation fault.
#0  0x08048498 in main (argc=2, argv=0xbffff8c4) at ch15-badmem1.c:21
21)
      p[0] = 'b';
```

The `efence(3)` manpage describes several environment variables that can be set to tailor Electric Fence’s behavior. The following three are the most notable.

`EF_PROTECT_BELOW`

Setting this variable to 1 causes Electric Fence to look for *underruns* instead of overruns. An overrun, accessing memory beyond the allocated area, was demon-
