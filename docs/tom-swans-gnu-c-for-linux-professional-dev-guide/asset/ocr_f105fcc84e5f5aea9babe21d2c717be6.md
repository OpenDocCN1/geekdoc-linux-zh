This is the same function as in the original program. However, kilos.cpp is a separate module that does not have a main() function. It is common, and usually wise, to name the header and separate modules files the same—kilos.h and kilos.cpp, in this case. This isn’t required, but helps you keep track of modules and their related header files. To finish the program requires writing another module with a main() function. Listing 10.14, kilotab.cpp, completes the picture.

# LISTING 10.14 KILOTAB.CPP

```
#include <iostream.h>
#include <iomanip.h>   // Need setw() manipulator
#include "kilos.h"     // Need kilos() function

int main()
{
    cout << "Miles    Kilometers" << endl;
    cout << "===========" << endl;
    for (int miles = 0; miles <= 200; miles += 20) {
        cout << setw(5) << miles << "   m   ";
        cout << kilos( miles ) << endl;
    }
    return 0;
}
```

The finished program includes the separately compiled kilos() function with this directive:
#include "kilos.h"

The quotes tell the compiler that kilos.h is in the current directory, or in one specified by the option -I (see Chapter 5, "Compiling and Debugging C++ Programs"). Including the header file declares the kilos() prototype, and that’s all that’s needed for the program to compile. During the final steps of compilation, the GNU linker searches for an object-code module that contains the implementation for the prototyped function. The linker must find implementations for all declared functions, or it ends with an error. To compile the separate kilos.cpp module and the kilotab program, and to link their separate object-code files, enter these commands:

```
$ g++ -c kilos.cpp
$ g++ kilotab.cpp kilos.o
$ ./a.out
```

# DEBUGGING FUNCTIONS

Finally in this chapter, some words about debugging functions and parameters. As the following sections explain, the GNU debugger offers several commands that are especially valuable for tracing through function statements.