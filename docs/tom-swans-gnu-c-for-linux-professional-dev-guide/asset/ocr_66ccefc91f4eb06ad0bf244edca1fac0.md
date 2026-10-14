# LISTING 22.4 CSTRING.CPP

```
#include <iostream.h>
#include <string>  // Need string class
#include <string.h>  // Need C-style string functions

#define BUFSIZE 64
char cstring[BUFSIZE];

int main()
{
    // Initialize C-style string
    //
    strcpy(cstring, "Test string");
    cout << "cstring == " << cstring << endl;

    // Convert a C-style string to a string object
    //
    string subject1(cstring);
    cout << "subject1 == " << subject1 << endl;

    // Convert a string object to a C-style string
    //
    string subject2("Test string object");
    int index = subject2.length();
    subject2.copy(cstring, index);
    cstring[index] = '0';
    cout << "cstring == " << cstring << endl;

    // Convert to constant C-style string pointer
    //
    string subject3("String object as const char *");
    const char *sp = subject3.c_str();
    cout << "*sp == " << sp << endl;
    // sp[4] = '#';  // ??? not permitted

    // Convert to C-style string without using copy()
    //
    char buffer[BUFSIZE];
    string subject4("String object copied to buffer");
    strcpy(buffer, subject4.c_str());
    cout << "buffer == " << buffer << endl;

    buffer[4] = '#';  // permitted
    subject4.assign(buffer);
    cout << "buffer == " << buffer << endl;

    return 0;
}
```

For test purposes, the program creates a global C-style string variable and initializes it by calling the strcpy() function:

```
#define BUFSIZE 64
char cstring[BUFSIZE];
...
strcpy(cstring, "Test string");
```