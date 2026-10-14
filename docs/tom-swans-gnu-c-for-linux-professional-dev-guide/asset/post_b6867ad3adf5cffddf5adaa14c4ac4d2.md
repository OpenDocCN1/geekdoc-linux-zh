
And this writes a single character:
ofs.put('2');

Or, you could use the following statement to do the same:
ofs << '2'; // Same as preceding

By the way, because the put() member function returns ostream & (a reference to an object of the ostream class, an ancestor of ios), you can string together multiple put() function calls in an odd-looking construction such as this:
ofs.put('A').put('B').put('C');

I dislike cryptic and tricky statements such as that, but I mention it here because I've seen this technique in C++ programs. The following is clearer, produces the same results, and is not so unusual-looking:
cout << 'A' << 'B' << 'C';

## READING TEXT A LINE AT A TIME

Many if not most text files are organized into variable-length lines, punctuated by newline control characters. Use the technique in this section to read text files a line at a time. As a bonus, this is usually faster than reading files one character at a time, although a disadvantage is the need to assume a maximum line length from the start. Listing 20.3, rline.cpp, is similar to rchar.cpp, but it reads a specified text file a line at a time and reports the number of characters and lines in the file:

## LISTING 20.3 RLINE.CPP

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>
#include <string.h>

#define BUFLEN 128

int main(int argc, char *argv[])
{
    if (argc <= 1) {
        cerr << "Error: filename missing" << endl;
        exit(1);
    }
    ifstream ifs(argv[1], ios::in);
    if (!ifs) {
        cerr << "Error: unable to open " << argv[1] << endl;
        exit(2);
    }
    char buffer[BUFLEN];
    long nc = 0, nl = 0;
    while (!ifs.eof()) {
ifs.getline(buffer, sizeof(buffer), '\n');
if (!ifs.eof() && strlen(buffer) == 0) {
    nc += strlen(buffer);
    nl++;
    cout << buffer << endl;
}
cout << endl << endl << "Total characters: " << nc;
cout << endl << "Number of lines: " << nl << endl;
return 0;
}
```
```

Compile and run the program using the following commands. You can specify the name of any text file to read and display—here, the second command displays the program’s own source code file:

```
$ g++ -o rline rline.cpp
$ ./rline rline.cpp
```

The program opens a file using the same technique as for reading text a character at a time. To read lines of text, the program calls the getline() member function using the following statement:

```
ifs.getline(buffer, sizeof(buffer), '\n');
```

The buffer is an array of char. Calling getline() and specifying the destination, buffer size, and line-ending character ensures that the entire line is read. The following statement reads only the next word (text separated by whitespace):

```
ifs >> buffer; // ???
```

Instead of that, it’s a good idea to preset the buffer size with the setw() manipulator. For example, to read a file a word at a time, include the iomanip.h header file and use a statement such as in the following fragment:

```
#include <iomanip.h>
...
ifs >> setw(BUFLEN) >> buffer;
```

This also ensures that the statement does not overwrite the end of the buffer, although GNU C++ apparently won’t do that, anyway.

The sample rline.cpp program also demonstrates one way to detect the end of a file by calling the eof() member function in reference to a file stream object. This function makes it easy to write a simple while loop that ends after processing every last smidgen of data in the file:

```
while (!ifs.eof()) {
    ifs.getline(buffer, sizeof(buffer), '\n');
    // Process line in buffer
}
```

## WRITING TEXT A LINE AT A TIME

The last of the four fundamental text-file techniques in this section explains how to write a text file a line at a time. Listing 20.4, wine.cpp, demonstrates the method.

```
#include <iostream.h>
#include <fstream.h>
#include <stdlib.h>
#include <string.h>
#include <string>

#define STR "2: Another literal string"

int main(int argc, char *argv[])
{
    if (argc <= 1) {
        cerr << "Error: filename missing" << endl;
        exit(1);
    }
    ifstream ifs(argv[1], ios::in);
    if (!ifs) {
        cerr << "Error: " << argv[1] << " already exists" << endl;
        cerr << "        Specify a different filename" << endl;
        exit(2);
    }
    ofstream ofs(argv[1], ios::out);
    if (!ofs) {
        cerr << "Error: unable to write to " << argv[1] << endl;
        exit(3);
    }

    ofs << "1: A literal string" << endl;
    ofs.write(STR, strlen(STR));
    ofs << endl;
    char *c = "String addressed by pointer";
    ofs << "3: " << c << endl;
    string string_object("4: A string object");
    ofs << string_object << endl;
    return 0;
}
```

Compile and run the program with these commands:

```
$ g++ -o wine wine.cpp
$ ./wine wine.txt
```

Check the contents of the new file by typing the following:

```
$ cat newfile.txt
1: A literal string
2: Another literal string
3: String addressed by pointer
4: A string object
```
