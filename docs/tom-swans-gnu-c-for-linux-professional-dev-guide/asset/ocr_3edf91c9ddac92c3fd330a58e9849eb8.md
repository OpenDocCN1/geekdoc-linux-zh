```
exit(1);
}
ifstream ifs(argv[1], ios::in);
if (!ifs) {
    cerr << "Error: unable to open " << argv[1] << endl;
    exit(2);
}

while (ifs.good()) {
    getline(ifs, s, '\n');
    cout << s << endl;
}

ifs.close();
return 0;
}
```

Compile the program to the output file rstrings, and then run it as follows to read and display the program's own source text:
$ g++ -o rstrings rstrings.cpp
$ ./rstrings rstrings.cpp

To read from a file, the program creates an object, ifs, of the ifstream class. While that class's good() member function returns true, there is more input waiting to be read. To do that, the program calls getline() passing ifs as an argument:

```
getline(ifs, s, '\n');
```

# GETTING string FACTS

The string class provides several member functions that report various aspects about a string object such as its length and capacity. Table 22.1 lists the string member functions you can call to obtain facts about any string object.

TABLE 22.1 THE string CLASS FACT-FINDING FUNCTIONS
| Function | Returns | Description |
|---|---|---|
| capacity() | size_type | Capacity of string in bytes |
| empty() | bool | True if string has no characters |
| length() | size_type | Length of string in characters |
| max_size() | size_type | Capacity of string in characters |
| size() | size_type | Same as length() |

Most functions in Table 22.1 return a value of type size_type, equated in the string class to size_t, and in GNU C++, equivalent to type long. The size() and length() functions return the same value, equal to the number of characters in a string object. A string's capacity() indicates how much memory is reserved for the string. This differs from max_size(), which takes into account the size of an individual character. For this reason, it's