
Table 26.1 describes the commands that you need to get up and debugging with gdb. To get a description of all of the gdb commands, refer to the *gdb* manual page.

## TABLE 26.1. BASIC gdb COMMANDS.

| Command | Description |
| :--- | :--- |
| file | Loads the executable file that is to be debugged. |
| kill | Terminates the program that you are currently debugging. |
| list | Lists sections of the source code used to generate the executable file. |
| next | Advances one line of source code in the current function, without stepping into other functions. |
| step | Advances one line of source code in the current function and does step into other functions. |
| run | Executes the program that is currently being debugged. |
| quit | Terminates gdb. |
| watch | Enables you to examine the value of a program variable whenever the value changes. |
| break | Sets a breakpoint in the code; this causes the execution of the program to be suspended whenever this point is reached. |
| make | Enables you to remake the executable program without quitting gdb or using another window. |
| shell | Enables you to execute UNIX shell commands without leaving gdb. |

The *gdb* environment supports many of the same command-editing features as do the UNIX shell programs. You can tell *gdb* to complete unique commands by pressing the Tab key just as you do when you are using *bash* or *tcsh*. If what you type is not unique, you can make *gdb* print a list of all the commands that match what you have entered so far by pressing the Tab key again. You can also scroll up and down through the commands that you have entered previously by pressing the up- and down-arrow keys.

## Sample gdb Session

This section goes step by step through a sample *gdb* session. The sample program that is being debugged is quite simple, but it is sufficient to illustrate how *gdb* is typically used.

We will start by showing a listing of the program that is to be debugged. The program is called *greeting* and is supposed to display a simple greeting followed by the greeting printed in reverse order.

```c
#include <stdio.h>

main ()
{
    char my_string[] = "hello there";

    my_print (my_string);
    my_print2 (my_string);
}

void my_print (char *string)
{
    printf ("The string is %s\n", string);
}

void my_print2 (char *string)
{
    char *string2;
    int size, i;

    size = strlen (string);
    string2 = (char *) malloc (size + 1);
    for (i = 0; i < size; i++)
        string2[size - i] = string[i];
    string2[size+1] = '\0';
    printf ("The string printed backward is %s\n", string2);
}
```

To compile the preceding program, use the gcc command followed by the filename. To rename the generated binary (instead of using the default a.out filename), use the -o option followed by the binary name, such as

```bash
gcc -o test test.c
```

The program, when executed, displays the following output:

The string is hello there
The string printed backward is

The first line of output displays correctly, but the second line prints something that is unexpected. The second line of output was supposed to be

The string printed backward is ereht olleh

For some reason the my_print2 function is not working properly. Let's take a look at the problem using gdb. First we need to start gdb, specifying the greeting program as the one to debug. Do this by entering the following command:

```bash
gdb greeting
```

> **Note:** Remember that you must compile the greeting program with the compiler debug options turned on.

If you forget to pass the program to debug as a parameter to gdb, load it in after gdb is started by using the file command at the gdb prompt:

```bash
(gdb) file greeting
```

This command loads the greeting executable just as if you had told gdb to load it on the command line.

Next, let's run greeting by entering the gdb run command. When the program is executed from within gdb, the result should resemble the following:

```bash
(gdb) run
Starting program: /root/greeting
The string is hello there
The string printed backward is
Program exited with code 041
```

The output of the greeting program is the same as when we executed the program outside of gdb. The question is, why is the backward print not working? To find the problem, let's set a breakpoint at the line after the for statement in the my_print2 function. To do this, list the source file by entering the list command three times at the gdb prompt:

```bash
(gdb) list
(gdb) list
```

> **Note:** Pressing Enter by itself at the gdb prompt will repeat the last command that was entered.

```bash
(gdb) list
```

Enter the list command for the first time and the output resembles the following:

```text
1    #include <stdio.h>
2
3    main ()
4    {
5      char my_string[] = "hello there";
6
7      my_print (my_string);
8      my_print2 (my_string);
9   }
10
```

Press Enter and gdb executes the list command again, displaying the following output:

```text
11   my_print (char *string)
12   {
13      printf ("The string is %s\n", string);
14   }
15
16   my_print2 (char *string)
17   {
18      char *string2;
19      int size, i;
20
```

Pressing Enter one more time lists the rest of the greeting program:

```text
21   size = strlen (string);
22   string2 = (char *) malloc (size + 1);
23   for (i = 0; i < size; i++)
24      string2[size - i] = string[i];
25   string2[size+1] = '\0';
26   printf ("The string printed backward is %s\n", string2);
27   }
```

By listing the file, we can see that the place where we want to set the breakpoint is line 24. Now, to set the breakpoint, enter the following command at the gdb command prompt:

```bash
(gdb) break 24
```

gdb should now print a response resembling the following:

```text
Breakpoint 1 at 0x139: file greeting.c, line 24
(gdb)
```

Now let’s run the program again by typing the run command. This command generates the following output:

```text
Starting program: /root/greeting
The string is hello there

Breakpoint 1, my_print2 (string = 0xbffffdc4 "hello there") at greeting.c
==>24
24    string2[size-i]=string[i]
```

We can see what is actually going wrong with the program by setting a watch which tells the value of the string2[size - i] variable expression.

To do this, type

```bash
(gdb) watch string2[size - i]
```

gdb returns the following acknowledgment:

Watchpoint 2: string2[size - i]

The version of gdb included on the CD-ROM accompanying this book changes the prompt to Hardware Watchpoint, but this is simply a change in the naming convention used by gdb. Now we can step through the execution of the for loop using the next command:

```bash
(gdb) next
```

After the first time through the loop, gdb tells us that string2[size - i] is 'h' by displaying the following message on the screen:

```text
Watchpoint 2, string2[size - i]
Old value = 0 '\000'
New value = 104 'h'
my_printf(string = 0xbffffdc4 "hello there") at greeting.c:23
23	for (i=0; i<size; i++)
```

This is the value that we expected. Stepping through the loop several more times reveals similar results. Everything appears to be functioning normally. When we get to the point where i=10, the value of the string2[size - i] expression is equal to 'e', the value of the size - i expression is equal to 1, and the program is at the last character that is to be copied over into the new string.

Step through the loop one more time and it’s clear that there is no value assigned to string2[0], which is the first character of the string. Because the malloc function initializes the memory it assigns to null, the first character in string2 is the null character. This explains why nothing is printed when we tried to print string2.

Now that we’ve found the problem, it should be quite easy to fix. We must write the code so that the first character going into string2 is being put into string2 at offset size - 1 instead of string2 at offset size. This is because the size of string2 is 12, but it starts numbering at offset zero. The characters in the string should start at offset 0 and go to offset 10, with offset 11 being reserved for the null character.

There are many ways to modify this code so that it will work. One way is to keep a separate size variable that is one smaller than the real size of the original string. This solution is shown in the following code:

```c
#include <stdio.h>

main ()
```
