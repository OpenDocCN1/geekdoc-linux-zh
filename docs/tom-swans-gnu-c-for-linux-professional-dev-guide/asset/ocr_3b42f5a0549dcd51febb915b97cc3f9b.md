# C-STYLE main() FUNCTIONS

While browsing C source code files, you might see main() declared this way:

```
int main(void)
{
    return 0;
}
```

The word void in parentheses is an ANSI C technique for indicating that a function receives no input parameters. GNU C++ doesn't seem to mind this type of declaration, but other C++ compilers might complain, so it's best not to use this form of main() in C++ programs.

C programmers also seem to favor writing the function return type on a separate line. You will often see a C program's main() function (and others) written like this:

```
int
main(void)
{
    return 0;
}
```

Placing the return type on its own line is purely a matter of style. C++ programmers tend to place the data type ahead of the function name.

# RETURNING VALUES FROM main()

You can use a shell script to run a program and examine its return value. This is often a simple, but effective, way to indicate whether a program succeeded or failed. Listing 4.4, error.cpp, combines what you know so far about C++ to display a message and return an error result code. No real error occurs, of course.

# LISTING 4.4 ERROR.CPP

```
#include <iostream.h>

int main()
{
    cout << "This program simulates an error" << endl;
    return 12;
}
```

Listing 4.5, runerror, is a sample bash (Bourne Again Shell) script that intercepts a program's return code. Script programming is too far afield from this book's subject matter, so I won't go into it here. Use the info command or consult a Linux reference for help with writing scripts for the shell of your choice.