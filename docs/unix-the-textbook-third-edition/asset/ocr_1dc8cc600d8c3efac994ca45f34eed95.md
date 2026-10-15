message is the memory address (0x0000000000400951) of the getchar() function that caused the exception. We can use the x command to display the contents of this memory location. The output of the command shows that the error occurred at the 178th byte in the getchar() function. We still do not know the reason why the program faulted.

```
(gdb) next
19        null_function1 ();
(gdb) next
20        null_function2 ();
(gdb) next
21        get_input (PROMPT, temp);
(gdb) step
get_input (prompt=0x400a76 "Enter a string: ", str=0x0) at
bugged.c:29
29        (void) printf("%s", prompt);
(gdb) step
30        for (*str = getchar(); *str != '\n'; *str = getchar())
(gdb) step
Enter a string: Hello world!
Program received signal SIGSEGV, Segmentation fault.
0x0000000000400951 in get_input (prompt=0x400a76 "Enter a string: ", str=0x0) at bugged.c:30
30        for (*str = getchar(); *str != '\n'; *str = getchar())
(gdb) x 0x0000000000400951
0x400951 <get_input+177>:    0x8b480a88
(gdb)
```

# 17.7.1.8 Accessing Identifiers (Variables and Functions)

You can access the location of an identifier (variable or function) in the program source and view its type, value, and places of use by using various gdb commands. In the following session, we illustrate the use of these commands with examples. The outputs of the commands are fairly self-explanatory. The print s_val and print str commands display the values of the s_vala and str variables as zero each and the whatis str command displays the type declaration of the str variable: char *, as expected.

```
(gdb) delete
Delete all breakpoints? (y or n) y
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /usr/home/sarwar/unix1e/ch17/gdb/bugged
Enter a string: Hello world!
Program received signal SIGSEGV, Segmentation fault.
```