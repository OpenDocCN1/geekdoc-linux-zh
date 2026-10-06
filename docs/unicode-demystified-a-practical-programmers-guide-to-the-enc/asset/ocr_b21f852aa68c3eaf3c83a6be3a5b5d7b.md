# select

The Bourne Again Shell's select control structure, based on the one found in the Korn Shell and corresponding to the select control structure in zsh, displays a menu, assigns a value to a variable based on the user's choice of items, and executes a series of commands. The syntax of a select structure is

```
select varname [in arg ... ]
do
  commands
done
```

First, select generates and displays a menu of the arg items. The menu is formatted with numbers before each item. For example, a select structure that begins with select fruit in apple blueberry kiwi orange watermelon STOP

displays the following menu:

+   1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

You can have many items in the list of args. The select structure uses the values of the LINES and COLUMNS variables to determine the size of the display. (LINES has a default value of 24; COLUMNS, a default of 80.) With COLUMNS set to 20, the menu looks like this:

+   1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

After displaying the menu, select displays the value of PS3, the special select prompt. The default value of PS3 is the characters #?, but typically you would set PS3 to a more meaningful value.

If in the preceding menu you enter a value number (one in the range), select sets the value of varname to the argument corresponding to number entered and executes the commands between do and done. The select structure issues the PS3 prompt and waits for another entry, doing this repeatedly until something causes it to exit from the statements between do and done, typically a break, return, or exit statement. The break statement exits from the loop. Within a function return returns control to the program that called the function. The exit statement exits from the current shell. The following script illustrates the use of select: