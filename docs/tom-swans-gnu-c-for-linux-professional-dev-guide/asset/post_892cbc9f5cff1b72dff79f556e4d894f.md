
After closing the input file, you then attempt to read the file's contents by constructing an input stream object and using statements such as

```
ifstream ifs("test.dat", ios::in | ios::binary);
if (ifs) {
    double d;
    ifs >> d;  // ???
    cout << "d == " << d << endl;
    ifs >> d;  // ???
    cout << "d * d == " << d << endl;
}
```

The program seems to run smoothly, but the reported results are obviously wrong. Here's what the program displays:

```
$ ./a.out
d == 3.1416
d * d == 0.86959
```

What's wrong? The first value seems okay, but pi squared is hardly equal to 0.86959. Examining the file's data using the Linux hexdump utility provides a clue to solving this mysterious bug. If you compiled and ran the wrong.cpp program, enter the following command to examine the contents of test.dat:

```
$ hexdump -bc test.dat
0000000 063 035 056 061 064 061 065 071 071 056 071 070 066 071 065 071
0000020 3   . 1 4 1 5 9 9 . 8 6 9 5 9
```

The file's contents reveals that the data has been stored as text despite the fact that the file was opened for binary I/O. This is because C++ I/O streams are designed to convert binary values to text, and they do not alter that action in any way based on how a file is opened.

When the program reads the file, the standard input statements perform the reverse task: in this case, reading the first value as 3.141599 and the second as 0.86959. Because the two values were written one after the other, there is no indication in the file that the second value should actually be 9.86959, and the input stream incorrectly "assumes" that the decimal point separates the two values.

This is an interesting problem, but fortunately, as the next section explains, it is not too difficult to solve.

## THE RIGHT SOLUTION

To read and write binary data requires deriving new classes from ifstream and ofstream. Because a char in C++ is the same as a byte, an array of char values can be used as a buffer for holding a series of bytes representing any value in binary form. To write a value in binary, the program copies the value's bytes to the output buffer and then writes that buffer as a series of bytes to disk. Similarly, to read a binary value, the program reads bytes into a char array and then copies those bytes to a variable of an appropriate type.

Actually, the buffer array isn't needed if we simply pretend that a binary value is a collection of bytes—which, of course, describes the nature of all data objects. Listing 20.5, wdouble.cpp, demonstrates the basic method of writing some double values in binary to a disk file.

## Note

When using the binary-file methods in this and the next sections, be aware that other C++ compilers may use different formats for representing binary data. You should not expect to be able to write a file of binary double values and read them correctly on another operating system.

## LISTING 20.5 WDOUBLE.CPP

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>

#define FILENAME "test.dat"

class bofstream: public ofstream {
public:
bofstream(const char *fn)
: ofstream(fn, ios::out , ios::binary) { }
void writeBytes(const void *, int);
bofstream & operator<< (double);
};

bofstream & bofstream::operator<< (double d)
{
writeBytes(&d, sizeof(d));
return *this;
}

int main()
{
bofstream bofs(FILENAME);
if (!bofs) {
cerr << "Error: unable to write to " << FILENAME << endl;
exit(1);
}
cout << "Writing to " << FILENAME << endl;
double d = 3.14159;
bofs << d;
bofs << d * d;
bofs << 9.999999;
d = 4.7E-8;
bofs << d;
return 0;
}

void bofstream::writeBytes(const void *p, int len)
{
if (!p) return;
if (len <= 0) return;
write((char *)p, len);
}
```

Compile and run the wdouble.cpp program using the following commands. Except for a confirmation message, the program displays no other output:

```
$ g++ -o wdouble wdouble.cpp
$ ./wdouble
Writing to test.dat
```

To provide for writing double values in binary, the program derives a new class, bofstream (binary-output-file-stream), from ofstream. The new class provides three member functions.

First is a constructor declared and implemented inline as

```
bofstream(const char *fn):
    ofstream(fn, ios::out | ios::binary) { }
```

The constructor merely calls the ancestor ofstream class constructor with a filename and with the two open_mode constants shown. To use the constructor, a program simply constructs an object of the bofstream class:

```
bofstream bofs(FILENAME);
```

Member function writeBytes() writes a number of bytes to the open file. The function is declared in bofstream as the following:

```
void writeBytes(const void *, int);
```

Function writeBytes() returns no value. Its first parameter is a constant void pointer that addresses the object to write to disk. The second int parameter equals the size of the object in bytes. Examine the function's implementation closely:

```
if (!p) return;
if (len <= 0) return;
write((char *)p, len);
```

If the pointer is NULL, the function merely returns and takes no further action. Similarly, if the specified length is less than or equal to zero, nothing happens. The third statement calls the inherited write() function to write len bytes of data starting at the address held in pointer p as a series of char values—that is, as a stream of bytes.

To provide for writing a specific type of data, the bofstream class declares a third member function:

```
bofstream & operator<< (double);
```

That overloads the output stream operator << for values of type double written to an object of the bofstream class. To carry out that job, the overloaded operator function executes these statements:

```
writeBytes(&d, sizeof(d));
return *this;
```

The parameter d is the double object to write to disk. First, writeBytes() writes to the file sizeof(d) bytes located at the address in d. Finally, the function returns its own object so that cascaded output statements such as the following write to this same destination (assume all variables are doubles):

```
bofs << d1 << d2 << d3;
```
