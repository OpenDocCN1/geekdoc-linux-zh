# LISTING 20.13 BFSTREAM.H

```
#include <iostream.h>
#include <fstream.h>

// Binary input and output file stream

class bfstream: public fstream {
public:
    bfstream(const char *fn)
        : fstream(fn, ios::in | ios::out | ios::binary) {}
    void writeBytes(const void *, int);
    void readBytes(void * , int);
    template <class T>
    bfstream & operator<< (const T & data);
    template <class T>
    bfstream & operator>> (T & data);
};

template <class T>
bfstream & bfstream::operator<< (const T & data)
{
    writeBytes(&data, sizeof(data));
    return *this;
}

template <class T>
bfstream & bfstream::operator>> (T & data)
{
    readBytes(&data, sizeof(data));
    return *this;
}
```

The bfstream class is derived from fstream, which provides low-level file stream operations. The bfstream constructor merely calls its ancestor constructor, passing a filename string and three open_mode constants as arguments:

```
bfstream(const char *fn)
    : fstream(fn, ios::in | ios::out | ios::binary) {}
```

Constructing a bfstream object opens the file if it exists, or creates a new file if not, for input and output in binary mode. It is still necessary, however, to provide overloaded input and output operator functions that perform the actual binary I/O. As in the bofstream and bfstream classes, the overloaded operators are written as templates. That way, the compiler generates actual functions based on the type of data involved, and in that way, the bfstream class can handle data of any type. Its readBytes() and writeBytes() member functions are the same as already described and are not listed here (see file src/c20/bfstream.cpp on the CID-ROM). Compile the module with the following command:

```
$ g++ -c bfstream.cpp
```

You now have a class that can read and write binary data of any type in the same file. Program bfstest.cpp in Listing 20.14 demonstrates how to use the new class.