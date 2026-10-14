# READING AND WRITING BINARY VALUES

Listing 20.9 demonstrates how to use the `bofstream` and `bifstream` classes to read and write values of type `double` in a file.

```
```cpp
#include <iostream>
#include <cstdlib.h>      // Need exit()
#include <fstream.h>

#define FILENAME "tbdouble.dat"

int main()
{
    // Construct binary output file
    bofstream bofs(FILENAME);
    if (!bofs) {
        cerr << "Error: unable to write to " << FILENAME << endl;
        exit(1);
    }

    // Write values and close file
    double d = 3.14159;
    bofs << d << d << d << d;
    bofs.close();

    // Construct binary input file
    bifstream bifs(FILENAME);
    if (!bifs) {
        cerr << "Error: unable to open " << FILENAME << endl;
        exit(2);
    }

    // Read and display values from file
    int count = 0;
    cout.precision(8);
    bifs >> d;
    while (!bifs.eof()) {
        cout << ++count << ": " << d << endl;
        bifs >> d;
    }

    return 0;
}
```
```

Compile and run the sample program with the following commands (skip the first command if you already compiled bstream.cpp):

```
```shell
$ g++ -c bstream.cpp
$ g++ -o tbdoubIe tbdouble.cpp bstream.o
$ ./tbdouble
1: 3.14159
2: 9.8695877
3: 31.006198
```
```