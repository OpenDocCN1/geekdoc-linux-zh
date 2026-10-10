# Finding bugs by using gdb

To understand how you can find bugs by using gdb, you need to see an example. The procedure is easiest to show with a simple example, so I start with a rather contrived program that contains a typical bug.

The following is the contrived program, which I store in the file dbgstst.c:

```
#include <stdio.h>
static char buf[256];
void read_input(char *s);
int main(void)
{
  char *input = NULL; /* Just a pointer, no storage for string */
  read_input(input);
/* Process command. */
  printf("You typed: %s\n", input);
/* ... */
  return 0;
}
void read_input(char *s)
{
  printf("Command: ");
  gets(s);
}
```

This program's main function calls the read_input function to get a line of input from the user. The read_input function expects a character array in which it returns what the user types. In this example, however, main calls read_input with an uninitialized pointer—that's the bug in this simple program.

Build the program by using gcc with the -g option:

```
gcc -g -o dbgstst dbgstst.c
```

Ignore the warning message about the gets function being dangerous; I'm trying to use the shortcoming of that function to show how you can use gdb to track down errors.

To see the problem with this program, run it and type test at the Command: prompt:

```
./dbgstst
Command: test
Segmentation fault
```

The program dies after displaying the Segmentation fault message. For such a small program as this one, you can probably find the cause by examining the source code. In a real-world application, however, you may not