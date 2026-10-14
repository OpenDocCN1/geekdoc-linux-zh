# LISTING 8.2 UPPER.CPP

```
#include <iostream.h>
#include <ctype.h>  // Need toupper()

char c; // Holds characters in transit

int main()
{
    while (cin.get(c) != 0) {
        c = toupper(c);
        cout.put(c);
    }
    return 0;
}
```

# Tip

> Next to an #include directive, I like to write a comment that indicates what function or other declaration the program needs from a header. (See the second line of upper.cpp.) When I revise a program, the comment helps avoid including header files that are no longer needed.

The toupper() function is declared in the standard library's ctype.h header. Actually, toupper() is implemented as a preprocessor macro, but you use it as you do any other callable function. The while loop calls toupper() to convert each character to uppercase. To convert to lowercase, you can instead call tolower(). I wrote the while loop the "long" way for clarity, but you can shorten it to

```
while (cin.get(c) != 0)
    cout.put(toupper(c));
```

# READING NATIVE TYPES

I/O stream statements can read and write objects of any C++ data type, not only strings and characters. Listing 8.3, getval.cpp, shows how to use I/O stream statements to read integer and floating point values. The program also demonstrates how to detect input errors if the program's user types an illegal character such as a letter when the program expects numerical input.

# LISTING 8.3 GETVAL.CPP

```
#include <iostream.h>
#include <stdlib.h>

void test(void);  // Function prototype

double fp;        // A floating point value
long k;           // A long int value

int main()
{
    cout << "Enter a floating point value: ";
```