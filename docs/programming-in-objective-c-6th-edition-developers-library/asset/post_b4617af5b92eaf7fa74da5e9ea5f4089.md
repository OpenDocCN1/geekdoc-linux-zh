
current file is the one that contains `m`, and the current line is the first executable line in `m`; otherwise, the current line, file, and procedure are set to the location where the program aborted.

If a local variable with the specified name doesn't exist, gdb looks for an external variable of the same name. In the previous example, the function executing at the time the invalid access occurred was `m`, and `i` was a variable local to `m`.

A function can be specified as part of the variable name in the form *function*::*variable* to reference a variable local to a specific routine, for example,

```
print main::i           Display contents of i in main
set var main::i=0       Set value of i in main
```

Note that attempting to set a variable in an inactive function (that is, a function that is not either currently executing or waiting for another function to return to continue its own execution) is an error and results in the following message:

```
N
```

Global variables can be directly referenced as '*file*::*var*'. This forces gdb to access an external variable as defined in the file *file* and ignore any local variable of the same name in the current function.

Structure and union members can be accessed using standard C syntax. If d is a pointer to a struct, p prints the year member of the structure pointed to by d.

Referencing a structure or union without a member causes the contents of the entire structure or union to be displayed.

You can force gdb to display a variable in a different format, for example hexadecimal, by following the p command with a `/` and a letter that specifies the format to use. Many gdb commands can be abbreviated with a single letter. In the following example, the abbreviation for the p command, which is p, is used:

```
set var i=35           Set i to 3
p / x i                 Display i in hexadecimal
```

# Source File Display

gdb provides several commands that give you access to the source files. This enables you to debug the program without having to reference a source listing or open your source files in other windows. As mentioned earlier, gdb maintains an idea of what the current line and file are. You've seen how you can display the area around the current line with the `l` command, which can be abbreviated as `l`. Each time you subsequently type the `l` command (or more simply, just press the Enter or Return key), the next 10 lines from the file are displayed. This value of 10 is the default and can be set to any value by using the `l` command.

If you want to display a range of lines, you can specify the starting and ending line numbers, separated by a comma, as follows:

```
list 10,15        List lines 10 through 15
```

Lines from a function can be listed by specifying the function’s name to the `l` command:

```
list foo          Display lines for function foo
```

If the function is in another source file, gdb automatically switches to that file. You can find the name of the current source file being displayed with gdb by typing in the command `i`.

Typing a `+` after the `l` command causes the next 10 lines from the current file to be displayed, which is the same action that occurs if just `l` is typed. Typing a `-` causes the previous 10 lines to be displayed. Both the `+` and `-` options can also be followed by a number to specify a relative offset to be added or subtracted from the current line.

## Controlling Program Execution

Displaying lines from a file doesn’t modify the way a program is executed. You must use other commands for that. You’ve seen two commands that control the execution of a program in gdb: `r`, which runs the program from the beginning, and `q`, which terminates execution of the current program.

The `r` command can be followed by command-line arguments and/or redirection (`<` or `>`), and gdb handles them properly. Subsequent use of the `r` command without any arguments reuses the previous arguments and redirection. You can display the current arguments with the command `args`.

## Inserting Breakpoints

The `b` command can be used to set breakpoints in your program. A breakpoint is just as its name implies—a point in your program that, when reached during execution, causes the program to “break” or pause. The program’s execution is suspended, which allows you to do things such as look at variables and determine precisely what’s going on at the point.

A breakpoint can be set at any line in your program by simply specifying the line number to the command. If you specify a line number but no function or filename, the breakpoint is set on that line in the current file; if you specify a function, the breakpoint is set on the first executable line in that function.

```
break 12          Set breakpoint on line 12
break main        Set breakpoint at start of main
break mod2.c:foo  Breakpoint in function foo in file mod2.c
```

When a breakpoint is reached during program execution, gdb suspends execution of your program, returns control to you, and identifies the breakpoint and the line of your program at which it stopped. You can do anything you want at that point: You can display or set variables, set or unset breakpoints, and so on. To resume execution of the program, you can simply use the `c` command, which can be abbreviated as simply `c`.

## Single Stepping

Another useful command for controlling program execution is the `s` command, which can be abbreviated as `s`. This command single steps your program, meaning that one line of C code in your program is executed for each `s` command you enter. If you follow the `s` command with a number, then that many lines are executed. Note that a line might contain several C statements; however, gdb is line oriented, and executes all statements on a line as a single step. If a statement spans several lines, single stepping the first line of the statement causes all the lines of the statement to be executed. You can single step your program at any time that a `c` is appropriate (after a signal or breakpoint).

If the statement contains a function call and you `s`, gdb takes you into the function (provided it’s not a system library function; these are typically not entered). If you use the `n` command instead of `s`, gdb makes the function call and does not step you into it.

Try some of gdb’s features on Program 17.5, which otherwise serves no useful purpose.

**Program 17.5 Working with gdb**

```c
#include <stdio.h>
#include <stdlib.h>

struct date {
    int year;
    int month;
    int day;
};

struct date newdate;
int array[10];
char string[20];
struct date today;

void foo() {
    int x;
    x = 10;
    today.year = 2023;
    today.month = 10;
    today.day = 5;
    printf("foo called\n");
}

int main() {
    int i;
    i = 3;
    array[i] = 42;
    strcpy(string, "hello");
    foo();
    printf("today: %d-%d-%d\n", today.year, today.month, today.day);
    return 0;
}
```

In the sample session for Program 17.5, your output might be slightly different, depending on which version and on what system you are running gdb.

**Program 17.5 gdb Session**

```
$ gcc -g p18-5.c
gdb a.out
(gdb) list main
1    #include <stdio.h>
2    #include <stdlib.h>
3    
4    struct date {
5        int year;
6        int month;
7        int day;
8    };
9    
10   struct date newdate;
(gdb) break main
(gdb) run
(gdb) step
(gdb) print today
(gdb) print array
(gdb) step
(gdb) print array
(gdb) list 23,28
23     i = 3;
24     array[i] = 42;
25     strcpy(string, "hello");
26     foo();
27     printf("today: %d-%d-%d\n", today.year, today.month, today.day);
28     return 0;
(gdb) step 5
(gdb) print string
(gdb) print string[1]
(gdb) print array[i]
(gdb) print newdate
(gdb) print newdate->month
(gdb) print newdate->day + i
(gdb) print $1
(gdb) info locals
(gdb) break foo
(gdb) continue
(gdb) print today
(gdb) print main::today
(gdb) step
(gdb) print x.day
(gdb) continue
```

Note one feature of gdb: After a breakpoint is reached or after single stepping, it lists the line that will be executed next when you resume execution of your program, and not the last executed line. That’s why `array` was still not initialized the first time it was displayed. Single stepping one line caused it to be initialized. Also note that declarations that initialize automatic variables are considered executable lines (they actually do cause the compiler to produce executable code).

### Listing and Deleting Breakpoints

Once set, breakpoints remain in a program until gdb exits or until you delete them. You can see all the breakpoints that you have set by using the `info break` command, as follows:

```
(gdb) info break
```

You can delete a breakpoint at a particular line with the `clear` command followed by the line number. You can delete a breakpoint at the start of a function by specifying the function’s name to the `clear` command instead:

```
(gdb) clear 20        Remove breakpoint from line 20
(gdb) info break
(gdb) clear foo       Remove breakpoint on entry into foo
(gdb) info break
```
