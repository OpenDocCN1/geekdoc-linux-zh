# # GNU C++ Class Libraries

GNU C++ comes packaged with an extensive class library. A class library is a reusable set of classes that can be used to perform a specified set of functions. Some typical examples of class libraries are class libraries that handle database access, class libraries that handle graphical user interface programming, and class libraries that implement data structures.

Other examples of graphical user interface class libraries are the Microsoft Foundation Classes and Borland’s Object Windows Library, both of which are class libraries used for developing Windows applications.

This section introduces several of the features that are offered by the GNU C++ class library.

# ## Streams

The GNU iostream library, called `libio`, implements GNU C++’s standard input and output facilities. This library is similar to the I/O libraries that are supplied by other C++ compilers. The main parts of the iostream library are the input, output, and error streams. These correspond to the standard input, output, and error streams that are found in C and are called `cin`, `cout`, and `cerr`, respectively. The streams can be written to and read from using the `<<` operator for output and the `>>` operator for input.

The following program uses the iostream library to perform its input and output:

```
```
#include <iostream.h>
int main()
{
char name[10];
cout << "Please enter your name.\n";
cin >> name;
cout << "Hello " << name << " how is it going?\n";
}
```
```

# ## Strings

The GNU string class extends GNU C++’s string manipulation capabilities. The string class essentially replaces the character array definitions that existed in C and all the string functions that go along with the character arrays.