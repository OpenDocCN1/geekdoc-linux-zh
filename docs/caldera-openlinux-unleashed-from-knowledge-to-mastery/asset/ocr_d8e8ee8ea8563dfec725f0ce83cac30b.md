Here is a sample project. Create the following files:

```
File hello.c:
```c
/* hello.c */
#include <stdio.h>
#include "hello.h"
void hello(char *who)
{
    printf("Hello, %s\n", who);
}
```
```

```
File hello.h:
```c
/* hello.h */
void hello(char *who);
```
```

```
File main.c:
```c
/* main.c */
#include "hello.h"
int main()
{
    hello("World");
    return 0;
}
```
```

To build the program (call it prog), you need to compile each of the C source files and link them, like this:

```
```bash
$ gcc -c -o hello.o hello.c
$ gcc -c -o main.o main.c
$ gcc -o prog main.o hello.o
$ ./prog
Hello, World!
```
```

Now, suppose you want to change the exclamation mark in the message to a period. You have to edit hello.c to make the change. You must them recompile hello.c, but you do not have to recompile main.c. You only need to perform the final linking step.

Let’s create a makefile for this project. Create a file called Makefile (note the capitalization) with the following contents:

```
```makefile
# Makefile for sample project
# NOTE: Use 'tab' for indented lines, NOT spaces!
# Also leave blank lines exactly as shown.

prog: main.o hello.o
	gcc -o prog main.o hello.o

main.o: main.c hello.h
```
```

![](bbox=[0.85, 0.08, 0.95, 0.25])