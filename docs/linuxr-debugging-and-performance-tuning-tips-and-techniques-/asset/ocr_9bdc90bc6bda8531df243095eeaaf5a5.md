Electric Fence should not be linked with a production binary.) The following session demonstrates this procedure and shows what happens for both command-line options:

```
```
$ cc -g ch15-badmem1.c -lefence -o ch15-badmem1     Compile; link statically
$ gdb ch15-badmem1                                    Run it from the debugger
gdb (gdb) 5.3
...  Try -b option
(gdb) run -b
Starting program:  /home/arnold/progex/code/ch15/ch15-badmem1 -b
[New Thread 8192 (LWP 28021)]

   Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

 Program received signal SIGSEGV, Segmentation fault.   SIGSEGV: GDB prints where
 (Switching to Thread 8192 (LWP 28021))
 0x080485b6 in main (argc=2, argv=0xbffffffa4) at ch15-badmem1.c:18
                                                    p[42] = 'a';       /* touch outside the bounds */
(gdb) run -f                                               Now try the -f option
The program being debugged has been started already.
Start it from the beginning? (y or n) y                       Yes, really

Starting program:  /home/arnold/progex/code/ch15/ch15-badmem1 -f
[New Thread 8192 (LWP 28024)]

   Electric Fence 2.2.0 Copyright (C) 1987-1999 Bruce Perens <bruce@perens.com>
p = <not 30 bytes>

 Program received signal SIGSEGV, Segmentation fault.          SIGSEGV again
 (Switching to Thread 8192 (LWP 28024))
 0x080485e8 in main (argc=2, argv=0xbffffffa4) at ch15-badmem1.c:21
                                                    p[0] = 'b';
```
```

On systems that support shared libraries and the LD_PRELOAD environment variable (including GNU/Linux), you don’t need to explicitly link in the efence library. Instead, the ef shell script arranges to run the program with the proper setup.

Although we haven’t described the mechanisms in detail, GNU/Linux (and other Unix systems) support shared libraries, special versions of the library routines that are kept in a single file on disk instead of copied into every single executable program’s binary file. Shared libraries save some space on disk and can save system memory, since all programs using a shared library share the same in-memory copy of the library. The cost is that program startup is slower because the program and the shared library have to be hooked together before the program can start running. (This is usually transparent to you, the user.)