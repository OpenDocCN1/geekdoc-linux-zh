after displaying an error message. Because the example is contrived, I have
an extra buffer named buf defined in the dbgtst program, as follows:

```
static char buf[256];
```

I can fix the problem of the uninitialized pointer by setting the variable
input to buf. The following session with gdb corrects the problem of the
uninitialized pointer (this example picks up immediately after the program
runs and dies, due to the segmentation fault):

```
(gdb) file dbgtst
A program is being debugged already. Kill it? (y or n) y
Load new symbol table from "dbgtst"? (y or n) y
Reading symbols from dbgtst...
done.
(gdb) list
1  #include <stdio.h>
2
3  static char buf[256];
4  void read_input(char *s);
6  int main(void)
7 {
      char *input = NULL; /* Just a pointer, no storage
      for string */
9
10     read_input(input);
(gdb) break 9
Breakpoint 1 at 0x8048393: file dbgtst.c, line 9.
(gdb) run
Starting program: /home/nado/code/dbgtst
Breakpoint 1, main () at dbgtst.c:10
10     read_input(input);
(gdb) set var input=buf
(gdb) cont
Continuing.
Command: test
You typed: test
Program exited normally.
(gdb)q
```

As the previous listing shows, if I stop the program before read_input
is called and set the variable input to buf (which is a valid array of
characters), the rest of the program runs fine.

After finding a fix that works in gdb, you can make the necessary changes to
the source files and make it permanent.