and "show warranty" for details.
This GDB was configured as "i486-linux-gnu"...
(gdb)

At the (gdb) command prompt you can enter debugging commands. An extensive number of commands can be used. Some of the more useful ones are shown in Table 27-4.

# Table 27-4: The gdb Commands

| Command | Description |
|---|---|
| break | Set a breakpoint in the source code to stop execution |
| watch | Set a watchpoint to stop execution when a variable reaches a specific value |
| info | Observe system elements, such as registers, the stack, and memory |
| x | Examine memory location |
| print | Display variable values |
| run | Start execution of the program within the debugger |
| list | List specified functions or lines |
| next | Step to the next instruction in the program |
| until | Run the program until it reaches the specified source code line (or greater) |

Here's a short example of a gdb session:

```
(gdb) list
1 #include <stdio.h>
2 int main()
3 {
4 printf("My first C program!\n");
5 return(0);
6 }
(gdb) break main
Breakpoint 1 at 0x80483d5: file ctest.c, line 4.
(gdb) run
Starting program: /home/rich/ctest

Breakpoint 1, main () at ctest.c:4
4 printf("My first C program!\n");
(gdb) next
My first C program!
5 return(0);
(gdb) next
6 }
(gdb) next
0xb7e2268b in __libc_start_main () from /lib/tls/i686/cmov/libc.so.6
(gdb) next
Single stepping until exit from function __libc_start_main.
```