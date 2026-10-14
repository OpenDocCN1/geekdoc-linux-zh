
Tip
Using the Emacs editor, press M-a to move backward and M-e to move forward one statement at a time in C and C++ source code files. M stands for meta-key. On most PC keyboards, the meta-key is Alt.

The second and last statement in main() (notice that it too ends with a semicolon) returns a value to the function's caller:

```
return 0;
```

A return value of 0 indicates that the program ran and finished successfully. A nonzero value, which must be in the range of 1 to 255, indicates that an error occurred. See “Program Entry and Exit” later in this chapter for more information on main() return statements.

## MORE ABOUT SEMICOLONS

Semicolon placement in C and C++ programming confuses everyone at first. Always remember that semicolons terminate statements, not lines of text. Semicolons also terminate some other elements such as variable definitions, but more on that in Chapter 6, “Creating Data Objects.”

The best way to learn where to type semicolons is to understand that the compiler needs them to locate the ends of statements and declarations. This is because the compiler ignores whitespace, or more specifically, extraneous blank lines, spaces, and tabs. Programmers write most statements on separate lines and use indentation to make source code readable, but the compiler is no literary connoisseur, and it doesn’t care how the text looks. The following rearranged welcome.cpp compiles correctly because the compiler understands its syntax perfectly well (notice the locations of the semicolons):

```
#include <iostream.h>
void main(){cout<<"Welcome to GNU C++ for Linux programming!"
<<endl;return 0;}
```

If you write code like that, you will incur the wrath of all who have to read your programs. You’ll deserve it too.

## CALLING C LIBRARY FUNCTIONS

Because the C++ programming language is based on C, anything you can do in C, you can do in C++. The same is generally true with most C++ compilers, but GNU C++ makes it particularly easy to switch between the two languages. You can also combine C and C++ programming methods in the same program.

Those capabilities are important to C++ programmers for several reasons. For one, numerous Linux programs are written in C. To understand the source code statements in those programs, you need to know C programming techniques. For another, GNU C++ provides an extensive standard library of C functions that perform all sorts of services such as working with dates and times, performing mathematical calculations, and manipulating character

Chapter 8, “Controlling Input and Output,” in the section “Formatting Output with the sprint() Family.” As with puts(), calling printf() as follows is another perfectly acceptable way to print a string to the standard output:
printf("A string written by printf()\n");

Look closely at the end of the quoted string. The double-character symbol \n is called an escape code. A backslash begins the code, which is followed in this case by a lowercase n. Together, the two characters represent the “new line” character. Written to the standard output, this starts a new line on the display. To write a backslash, type two of them like this:
printf("Write a backslash \\ and start a new line\n");

Some other escape codes are \t, which prints a tab, \e for <esc> (this might be specific to GNU C++), and \a, which is supposed to “alert” the user by ringing a bell, but don’t count on it. You can use escape codes in any literal string. For example, the following C++ statement writes a string to the standard output followed by two new lines:

```
cout << "Give me some space!\n\n";
```

It is clearer, although not necessarily better, to use the endl object in place of \n. The technically correct way to write the preceding line in C++ is

```
cout << "Give me some space!" << endl << endl;
```

Note
See Chapter 6, “Creating Data Objects,” in the section “Character Escape Codes” for a complete list of escape codes you can insert into strings.

You might wonder which C or C++ output method to use. All work perfectly well, but I favor the C++ method for several reasons. As explained in this book’s more advanced chapters, in C++ you can create customized output objects for use in I/O stream statements (see for example Chapter 20, “Customizing I/O Streams”). You can also use the << operator to write file data along with >> to read input, and you can even reprogram those operators to recognize other types of objects. C is not as flexible. In the standard C library, the puts() function is strictly limited to writing string data. Other functions in the C library are similarly restricted to using data of a specific type. That’s not bad, but in practice, the inflexibility of standard C library functions creates barriers to writing easily maintained code.

Another good reason to favor C++ over C output techniques is that C++ uses exceptions for error handling. Because the C language does not implement exceptions, standard C library functions can’t use them to report errors. Chapter 16, “Handling Exceptions,” explains how to use exceptions for creating robust programs that safely handle even the trickiest error conditions.
