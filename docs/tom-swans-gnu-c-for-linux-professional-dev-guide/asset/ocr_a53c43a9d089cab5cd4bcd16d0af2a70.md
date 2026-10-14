```
char buffer[BUFSIZE];  // Holds user input
int value;             // Holds input converted to an integer

int main()
{
    cout << "Enter an integer value: ";
    cin.getline(buffer, BUFSIZE);  // Read input from user
    value = atoi(buffer);          // Convert to integer
    cout
        << " Decimal==" << dec << value
        << " Hexadecimal==0x" << hex << value
        << " Octal==0" << oct << value << endl;
    return 0;
}
```

For simplicity, the convert.cpp program calls getline() as described in this chapter to read the user's input. After that statement, the standard library function atoi() (ASCII to integer) declared in stdlib.h converts the contents of the character buffer to an integer value.

Near the end of main(), an output stream statement writes the converted value in decimal, hexadecimal, and octal, as shown in this sample run:

```
$ g++ convert.cpp
$ ./a.out
Enter an integer value: 123
Decimal==123 Hexadecimal==0x7B Octal==0173
```

Output is formatted three ways by using the I/O stream manipulators dec, hex, and oct. Writing these predefined symbols to cout affects the format of subsequent output. Carefully examine the program's output statement:

```
cout
    << " Decimal==" << dec << value
    << " Hexadecimal==0x" << hex << value
    << " Octal==0" << oct << value << endl;
```

Tip
It might be easier to debug individual output statements than a long, cascaded one as listed here. Consider this when writing your code.

# USING I/O STREAM MANIPULATORS

GNU C++ provides several other manipulators in addition to dec, hex, and oct introduced in the preceding section. These are useful for formatting output, and also for reading input in a specific format. Table 8.1 lists the manipulators you can use in I/O stream statements. The middle column indicates whether the manipulator is appropriate in input (I), output (O), or both (I/O) types of statements.

Tip
Include the iomanip.h header file when using manipulators. This isn't required for endl, hex, dec, and oct, but is needed for others such as setprecision() that are implemented as functions.