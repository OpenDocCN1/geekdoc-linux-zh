
The `D` macro can be used throughout a program, and the intent is quite clear, as shown in *Program 17.3*.

## Program 17.3 Defining a D Macro

```c
#include <stdio.h>
#include <stdlib.h>

#define D(x) printf("%d\n", x)

int main(int argc, char *argv[]) {
    if (argc != 3) {
        fprintf(stderr, "Usage: a.out num1 num2\n");
        return 1;
    }
    int a = atoi(argv[1]);
    int b = atoi(argv[2]);
    D(a);
    D(b);
    return 0;
}
```

## Program 17.3 Output

```bash
$ gcc pre3.c
$ ./a.out 8 12
8
12
```

As you can see, the program is much more readable in this form. When you no longer need debugging output, simply define the macro to be nothing:

```c
#define D(x)
```

This tells the preprocessor to replace calls to the `D` macro with nothing, so all uses of `D` simply turn into null statements.

You can expand on the notion of the `D` macro a little further to allow for both compile-time and execution-time debugging control: Declare a global variable `DBGLVL` that defines a debugging level. All `D` statements less than or equal to this level produce output. `D` now takes at least two arguments; the first is the level:

```c
#define D(x, y) printf("%d: %s\n", (x), (y))
```

If the debugging level is set to 1 or 2, only the first `D` statement produces output; if the debugging level is set to 3 or more, both `D` statements produce output. The debugging level can be set via a command-line option at execution time as follows:

```bash
a.out -d1    # Set debugging level to 1
a.out -d3    # Set debugging level to 3
```

The definition for `D` is straightforward:

```c
#define D(level, msg) if (level <= DBGLVL) printf("%s\n", msg)
```

So

```c
D(1, "Start")
```

becomes

```c
if (1 <= DBGLVL) printf("%s\n", "Start")
```

Again, if `D` is defined to be nothing, the `D` calls become null statements.

The following definition provides all the mentioned features, as well as the ability to control the definition of `D` at compile time.

```c
#ifdef DEBUG
#  define D(level, msg) if (level <= DBGLVL) printf("%s\n", msg)
#else
#  define D(level, msg)
#endif
```

When compiling a program containing the previous definition (which you can conveniently place inside a header file and include in your program), you either define `DEBUG` or not. If you compile `prog.c` as follows:

```bash
$ gcc prog.c
```

it compiles in the null definition for `D` based on the `#else` clause shown in the previous preprocessor statements. On the other hand, if you compile your program like this:

```bash
$ gcc -DDEBUG prog.c
```

the `D` macro that calls `printf` based on the debug level is compiled in with the rest of your code.

At runtime, if you have compiled in the debugging code, you can select the debug level. As noted, this can be done with a command-line option as follows:

```bash
$ a.out -d3
```

Here, the debug level is set to 3. Presumably, you would process this command-line argument in your program and store the debug level in a variable (probably global) called `DBGLVL`. And in this case, only `D` macros that specify a level of 3 or greater cause the `printf` calls to be made.

Note that `-d0` sets the debugging level to zero and no debugging output is generated even though the debugging code is still in there.

To summarize, you have seen here a two-tiered debugging scheme: Debugging code can be compiled in or out of the code, and, when compiled in, different debugging levels can be set to produce varying amounts of debugging output.

## Debugging Programs with gdb

`gdb` is a powerful interactive debugger that is frequently used to debug programs compiled with GNU’s `g++` compiler. It allows you to run your program, stop at a predetermined location, display and/or set variables, and continue execution. It allows you to trace your program’s execution and even execute it one line at a time. `gdb` also has a facility for determining where core dumps occur. A core dump occurs due to some abnormal event, possibly division by zero or attempts to access past the end of an array. This results in the creation of a file named `core` that contains a snapshot of the contents of the process’s memory at the time it terminated.

- Your system might be configured to disable the automatic creation of this core file, often due to the large size of these files. Sometimes, this has to do with the maximum file creation size, which can be changed with the `ulimit` command.

Your C program must be compiled with the `g` compiler using the `-g` option to make full use of `gdb`'s features. The `-g` option causes the C compiler to add extra information to the output file, including variable and structure types, source filenames, and C statement to machine code mappings. Program 17.4 shows a program that attempts to access elements past the end of an array.

## Program 17.4 A Simple Program for Use with gdb

```c
#include <stdio.h>

int main() {
    int data[5] = {1, 2, 3, 4, 5};
    int i;
    int sum = 0;
    for (i = 0; i < 233; i++) {
        sum += data[i];
    }
    printf("Sum: %d\n", sum);
    return 0;
}
```

Here’s what happens when the program is run on a Mac OS X system from a terminal window (on other systems you might get a different message displayed when you run the program):

```bash
$ a.out
Segmentation fault (core dumped)
```

Use `gdb` to try to track down the error. This is certainly a contrived example; nevertheless, it is illustrative.

First, make sure you compile the program with the `-g` option. Then, you can start up `gdb` on the executable file, which is `a.out` by default. This might result in lines of introductory messages being displayed on your system:

![](img/e50cb5e8cc6587186db5746e2ac19394_351_0.png)

```bash
$ gcc -g p17.4.c
$ gdb a.out
(gdb)
```

```
Recompile with debugging information for gdb
Start up gdb on the executable file
```

When `gdb` is ready to accept commands, it displays a `(gdb)` prompt. In our simple example, you're simply telling it to run your program by entering the `run` command. This causes `gdb` to start execution of your program until it finishes or an abnormal event occurs:

![](img/e50cb5e8cc6587186db5746e2ac19394_351_1.png)

```bash
(gdb) run
Starting program: /path/to/a.out
[New process 12345]

Program received signal SIGSEGV, Segmentation fault.
0x0000000108c2a1b0 in main () at p17.4.c:9
9           sum += data[i];
```

```
run
```

So your program receives an error (as it did before), but it still remains under the control of `gdb`. That's the nice part because now you can see what it was doing when the error occurred as well as look at the values of variables at the time of the error.

As you can see from the previous display, the program tried to perform an invalid memory access at line 9 in your program. The actual line in question is automatically displayed from your source file. To gain a little context around that line, you can use the `list` command, which displays a window of 10 lines around the specified line (5 lines before and 4 lines after):

![](img/e50cb5e8cc6587186db5746e2ac19394_351_2.png)

```bash
(gdb) list 9
4           int data[5] = {1, 2, 3, 4, 5};
5           int i;
6           int sum = 0;
7           for (i = 0; i < 233; i++) {
8               sum += data[i];
9           }
10          printf("Sum: %d\n", sum);
11          return 0;
12      }
```

You can look at variables by using the `print` command. Take a look at what the value of `sum` was at the time the program stopped with an error:

```bash
(gdb) print sum
$1 = 10
```

This value for `sum` is obviously out of whack (and on your system might differ from what’s shown here). The `$` notation is used by `gdb` to keep track of the values you’ve previously displayed, so you can easily reference them again later.

Take a look at what the index variable `i` is set to:

```bash
(gdb) print i
$2 = 233
```

Oops! That’s not good. You have only five elements in the array and you tried to access the 233rd element when the error occurred. On your system, the error might occur earlier or later. But eventually, you should get an error.

Before you exit from `gdb`, look at another variable. See how nicely `gdb` deals with variables like arrays and structures:

```bash
(gdb) print data
$3 = {1, 2, 3, 4, 5}
(gdb) print data[0]
$4 = 1
```

You’ll see an example of a structure a little later. To complete this first example with `gdb`, you need to learn how to get out. You can do that with the `quit` command:

```bash
(gdb) quit
Quit anyway? (y or n) y
```

Even though the program had an error, technically speaking, it was still active inside `gdb`; the error merely caused your program’s execution to be suspended, but not terminated. That’s the reason `gdb` asked for confirmation about quitting.

## Working with Variables

`gdb` has two basic commands that allow you to work with variables in your program. One you’ve seen already is `print`. The other allows you to set the value of a variable. This is done with the `set` command. The `set` command actually takes a number of different options, but `var` is the one you want to use to assign a value to a variable:

```bash
(gdb) set var i=5
(gdb) print i
$5 = 5
(gdb) set var i=i*2
(gdb) print i
$6 = 10
(gdb) set var i=$1+20
(gdb) print i
$7 = 30
```

A variable must be accessible by the current function, and the process must be *active*, that is, running. `gdb` maintains an idea of a current line (like an editor), a current file (the source file of the program), and a current function. When `gdb` starts up without a core file, the current function is `main`, the
