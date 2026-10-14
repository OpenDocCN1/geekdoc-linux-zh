
programmers add a break after each case so that a newly added case does not accidentally create a fall-through.

Listing 9.10, menu.cpp, demonstrates a good use for a switch statement. The program prompts users to select from a menu of commands. It uses a switch statement to execute different statements based on the character entered. The program also demonstrates a practical use for a Do-Forever for loop.

## LISTING 9.10 MENU.CPP

```
#include <iostream.h>
#include <ctype.h>   // Need toupper()
#include <stdlib.h>  // Need exit()

char choice; // User command character

int main()
{
    for (;;) { // Do following switch statement "forever."
        cout << "Menu: A(dd D(elete S(ort Q(uit: ";
        cin >> choice; // Get user command
        switch ( toupper(choice) ) {
            case 'A':
                cout << "You selected Add" << endl;
                break;
            case 'D':
                cout << "You selected Delete" << endl;
                break;
            case 'S':
                cout << "You selected Sort" << endl;
                break;
            case 'Q':
                cout << "You selected Quit. Good bye!" << endl;
                exit(0);   // End program
            default:
                cout << "*** No such command!" << endl;
                break;
        } // switch
    } // for
    return 0; // Unreachable as currently written
}
```

The main() function in menu.cpp consists mostly of one Do-Forever for loop. Inside that loop, the program first displays a menu of commands. Compile and run the program to see this prompt:

```
$ g++ menu.cpp
$ ./a.out
Menu: A(dd D(elete S(ort Q(uit:
```

Enter a letter in upper- or lowercase to select a command (all are just for show, of course). The program's switch statement confirms your selection:

If you enter an unknown command letter, the program displays an error message:
Menu: A(dd D(elete S(ort Q(uit): x
*** No such command!

To respond to command entries, the program uses a switch statement that begins as follows:

```
switch ( toupper(choice) ) {
```

The toupper() function, declared in the ctype.h standard header, returns the choice char variable converted if necessary to uppercase. Each case in the switch statement compares this value with a literal character to select from among the program's statements. For example, the first case detects the A(dd command:

```
case 'A':
    cout << "You selected Add" << endl;
    break;
```

After displaying the confirming message, break ends the switch. However, because the switch is encased inside a Do-Forever for loop, after the switch statement ends, the program again displays the menu and waits for another command. When you type q to quit, the following case ends the program by calling the standard exit() function declared in stdlib.h:

```
case 'Q':
    cout << "You selected Quit. Good bye!" << endl;
    exit(0);  // End program
```

> Note
> The return statement in menu.cpp never executes. However, it's good form to include it in the event a change causes the program to reach the statement. Some compilers warn about "unreachable" statements such as this, but GNU C++ doesn't notice the condition. In all fairness, unreachable statements are not necessarily errors—they just don't do anything.

## for LOOP SCOPING

Finally in this chapter, some further words about declaring control variables in for statements such as this:

```
for (int i = 1; i <= 10; i++)
    cout << "i == " << i << endl;
```

```
// LISTING 9.11  FORSCOPE.CPP
#include <iostream.h>

int main()
{
    for (int i = 1; i <= 10; i++)
        cout << "i = " << i << endl;
    cout << "Final value of i == " << i << endl;   // ???
    return 0;
}
```

Compiling the forscope.cpp test program with GNU C++ using the following commands produces two warning messages:

```
$ g++ forscope.cpp
forscope.cpp: In function 'int main()':
forscope.cpp:7: warning: name lookup of 'i' changed for new ANSI 'for' scoping
forscope.cpp:5: warning: using obsolete binding at 'i'
```

The compiler issues the warnings because the program's for loop declares an i inside the loop, and the new ANSI C++ rules state that in such cases i is available only to statements inside the loop itself. However, the test program refers to i outside the loop as was permitted in past ANSI C++ drafts. To accommodate older programs that rely on the obsolete specifications, GNU C++ treats the condition as a warning rather than an error, and it completes the compilation. Other C++ compilers might refuse to compile this program at all.

To limit the scope of variables to the for loop that declares them, in GNU C++, compile with the option **-ffor-scope**. With this option, forscope.cpp does not compile. To use the older specification that places the for loop variable in the outer scope, use the **-fno-for-scope** option. Do that only if you are compiling older programs that assume the nonstandard rule. With that option, forscope.cpp compiles without any warnings or errors.

## SUMMARY

Without intervention, a C or C++ program's statements execute one after the other like water flowing down a river. C and C++ provide conditional and repetitive flow-control statements that alter this normal path. Conditional statements include if, if-else, switch, and conditional expressions. Repetitive statements include while, do-while, and for. In addition, this chapter explained how to use break, continue, and goto statements, and it explained the controversial subject of declaring control variables inside for loops.

For more information on subjects introduced in this chapter, turn to the following chapters:

- Chapter 6, “Creating Data Objects”
- Chapter 7, “Applying Fundamental Operators”
- Chapter 10, “Creating and Calling Functions”
