+   - Single-line `if` statements are acceptable:
+   
+   `if (!strcmp(str, "ttya")) strcpy(name, "ttySO";n`e ifs are quite OK:

+   - Kernel source, since the earliest times, has always contained a lot of gotos. Linux is no exception. It contains a goto for about every 80 lines of code. This is not because of sloppy programming style, but rather a requirement dictated by the craving for speedy code. In a next`ed` while statement, it is just much easier to use goto to get out of the code rather than break.

# Architecture Dependencies

Linux runs on a wide variety of processor platforms. Almost every month, you can read about a new successful porting to another architecture. Just remember that Linux originated on the i386 processor. This is clearly visible everywhere in the kernel code.

Table 2.2 illustrates the ports achieved so far:

**TABLE 2.2**
Ports achieved so far

| Processor Type | Bite size | Maintainer |

Intelx86 | 32 | Linus Torvalds
---|---|---
Crusoe | 32 | Linus Torvalds
MIPS | 32/64 | Alan Cox
IA64 | 64 | The Trillian Project
PA-RISC | 64 | The Puffin Group
Alpha | 64 | Richard Henderson
ARM | 32 | Russell King
Sparc | 32/64 | David S. Miller
PPc | 32 | Cort Dougan
M68000 | 32 | Jes Sorensen