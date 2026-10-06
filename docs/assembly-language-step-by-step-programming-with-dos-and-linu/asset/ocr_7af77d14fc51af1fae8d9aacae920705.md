values. I will treat this separately a little later, as you'll see it a lot in .s files and you should be able to understand it.

There are a handful of other issues that would be involved in programs more complex than we will take up in this book. These mostly involve near versus for calls and jumps and their associated return instructions.

# # Examining gas Source Files Created by gcc

The best way to get a sense for the AT&T assembly syntax is to look at an actual AT&T-style .s file produced by gcc. Doing this actually has two benefits: First of all, it will help you become familiar with the AT&T mnemonics and formatting conventions. In addition, you may find it useful, struggling to figure out how to call a C library function from assembly, to create a short C program that calls the function of interest and then examines the .s file gcc produces when it compiles your C program. dateis.c program which follows was part of my early research, and I used it to get a sense for how ctime() was called at the assembly level. Obviously, for this trick to work you must have at least a journeyman understanding of the AT&T mnemonics. (I discuss ctime() and other time-related C library calls in detail in the next chapter.)

You don't automatically get a .s file every time you compile a C program. The .s file is created, but once gas assembles the .s file to a binary object code file (typically a .o file), it deletes the .s file. If you want to examine a .s file created by gcc, you must compile with the -S option (Note that this is an uppercase S. Case matters big time in the Unix world!) The command would like this:

```
gcc dateis.c -S
```

Note that the output of this command is the assembly source file only. If you specify the -S option, gcc understands that you want to generate assembly source rather than an executable program file, so all it will generate is the .s file. To compile a C program to an executable program file, you must compile it again without the -S option.

Here's dateis.c. It does nothing than print out the date and time as returned by the standard C library function ctime():

```
#include <time.h>
#include <stdio.h>
```